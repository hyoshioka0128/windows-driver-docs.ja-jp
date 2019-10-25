---
title: オフロード データ転送
description: コンピューター間または同じコンピューター内でのデータ転送は、ファイルシステムの頻繁な動作です。
ms.assetid: 66006CC0-8902-47CD-8E7C-187FE5BA71EF
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 961cddf10dd475a6005178a924b202295984c45a
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841057"
---
# <a name="offloaded-data-transfers"></a>オフロード データ転送


コンピューター間または同じコンピューター内でのデータ転送は、ファイルシステムの頻繁な動作です。 標準の**ReadFile**関数と**WriteFile**関数を使用することは、機能的な観点からは適切に機能しますが、システムのあらゆるレベルでの大量のデータ移動と、ネットワーク経由の可能性があります。 これは、転送に関係するシステムとシステムを接続するネットワークの可用性に影響を与える可能性があります。 多くのストレージサブシステムで利用できる高度な機能を使用すると、データ移動タスクをより効率的に実行できます。

Windows 8 以降では、アプリケーションはこれらの機能を利用して、記憶域サブシステムへのデータ移動プロセスをオフロードすることができます。 通常、ファイルシステムフィルターは、ボリュームに対する読み取りおよび書き込み要求をインターセプトすることによって、これらのアクションを監視できます。 フィルターでオフロードデータ転送を認識するには、追加のアクションが必要です。

## <a name="span-idtypical_data_transfersspanspan-idtypical_data_transfersspanspan-idtypical_data_transfersspantypical-data-transfers"></a><span id="Typical_Data_Transfers"></span><span id="typical_data_transfers"></span><span id="TYPICAL_DATA_TRANSFERS"></span>標準的なデータ転送


現在、アプリケーションのシナリオでデータを移動するのは非常に簡単です。 ローカルメモリにデータを読み取ってから、新しい場所に書き戻す必要があります。 次の図は、このシナリオを示しています。

このシナリオでは、2つの異なるファイルサーバー上の2つの場所の間でファイルをコピーします。それぞれのファイルサーバーには、インテリジェントストレージアレイ (ISA) を介して公開される独自の仮想ディスクが含まれます。 開始システムは、まず、ソース仮想ディスクからローカルバッファーにデータを読み取る必要があります。 次に、何らかのトランスポートとプロトコル (1 Gbe を超える SMB など) を使用してデータをパッケージ化し、2番目のシステムに送信します。このシステムは、データを受信してローカルバッファーに出力します。 次に、ターゲットシステムによって、データが宛先仮想ディスクに書き込まれます。 このシナリオでは、毎日多くの異なるアプリケーションによって複数回実行されるデータ転送の非常に一般的な読み取り/書き込み方法について説明します。

![標準的なデータ転送](images/odx-scenario-1.png)

標準的な読み取りと書き込みは、ほとんどのシナリオで適切に動作しますが、コピーされるデータは、同じインテリジェントストレージアレイによって管理される仮想ディスクに配置される場合があります。 これは、データが配列からサーバーに移動され、ネットワークトランスポート経由で別のサーバーに移動し、もう一度同じ配列に戻されることを意味します。 サーバー内およびネットワークトランスポート間でデータを移動することは、これらのシステムの可用性に大きな影響を与える可能性があります。データ移動のスループットは、ネットワークのスループットと可用性によって制限されるという事実には触れません。

## <a name="span-idoffloaded_data_transfers__odx_spanspan-idoffloaded_data_transfers__odx_spanspan-idoffloaded_data_transfers__odx_spanoffloaded-data-transfers-odx"></a><span id="Offloaded_Data_Transfers__ODX_"></span><span id="offloaded_data_transfers__odx_"></span><span id="OFFLOADED_DATA_TRANSFERS__ODX_"></span>オフロードデータ転送 (ODX)


### <a name="span-idoffloading_the_data_transferspanspan-idoffloading_the_data_transferspanspan-idoffloading_the_data_transferspanoffloading-the-data-transfer"></a><span id="Offloading_the_Data_Transfer"></span><span id="offloading_the_data_transfer"></span><span id="OFFLOADING_THE_DATA_TRANSFER"></span>データ転送のオフロード

Windows 8 では、データ転送のオフロード方法を容易にする2つの新しい FSCTLs が導入されています。 これにより、サーバーからのビット移動の負担が、記憶域サブシステム内でインテリジェントに発生するように変化します。 コマンドのセマンティクスを視覚化する最良の方法は、バッファーなしの読み取りとバッファーなしの書き込みに似ていると考えることです。

<span id="FSCTL_OFFLOAD_READ"></span><span id="fsctl_offload_read"></span>[**FSCTL\_オフロード\_読み取り**](https://docs.microsoft.com/windows-hardware/drivers/ifs/fsctl-offload-read)  
このコントロール要求は、読み取り対象のファイル内のオフセットと、 [**FSCTL\_オフロード\_読み取り\_入力**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_fsctl_offload_read_input)構造体の必要な長さを受け取ります。 サポートされている場合、ファイルをホストする記憶域サブシステムは、関連付けられているオフロード読み取りストレージコマンドを受け取り、トークンを生成します。これは、オフロード読み取りコマンドの時点で読み取られることを意図したデータの論理表現です。 このトークン文字列は、 [**FSCTL\_オフロード\_読み取り\_出力**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_fsctl_offload_read_output)構造で呼び出し元に返されます。

<span id="FSCTL_OFFLOAD_WRITE"></span><span id="fsctl_offload_write"></span>[**FSCTL\_オフロード\_書き込み**](https://docs.microsoft.com/windows-hardware/drivers/ifs/fsctl-offload-write)  
この制御要求では、書き込み先のファイル内のオフセット、書き込みに必要な長さ、および書き込まれるデータの論理的な表現であるトークンが使用されます。 サポートされている場合、書き込まれるファイルをホストする記憶域サブシステムは、関連付けられているオフロード書き込みストレージコマンドを受け取ります。 まず、指定されたトークンを認識し、次に可能な場合は書き込み操作を実行します。 書き込み操作は Windows の下で完了します。そのため、ファイルシステムとストレージスタック上のコンポーネントにデータ移動は表示されません。 データの移動が完了すると、書き込まれたバイト数が呼び出し元に返されます。

![オフロードデータ転送](images/odx-scenario-2.png)

最初の図と同様に、2つの異なるサーバー上の2つの仮想ディスク間の単純なファイルコピーが示されています。 通常の読み取りと書き込みを行うのではなく、ストレージアレイへのビット移動の大量の処理をオフロードします。 最初のシステムはオフロード読み取り操作を実行し、配列は、最初の仮想ディスクの領域内で読み取るデータの特定の時点のビューを表すトークンを生成するように要求します。 その後、最初のシステムはトークンを2番目のシステムに送信します。その後、トークンを使用して2番目の仮想ディスクにオフロード書き込み操作が発行されます。 次に、配列はトークンを解釈し、仮想ディスク間のデータ移動を実行しようとします。 実際のデータ転送はインテリジェントストレージアレイ内で行われ、2つのホスト間では発生しないことがわかります。 これにより、システム間のネットワークトラフィックを実質的に排除しながら、2つのシステムの可用性を大幅に向上させることができます。

### <a name="span-idintegration_with_the_copy_enginespanspan-idintegration_with_the_copy_enginespanspan-idintegration_with_the_copy_enginespanintegration-with-the-copy-engine"></a><span id="Integration_with_the_Copy_Engine"></span><span id="integration_with_the_copy_engine"></span><span id="INTEGRATION_WITH_THE_COPY_ENGINE"></span>コピーエンジンとの統合

Windows のコアコピーエンジンは、 **CopyFile**および関連する関数によって使用されます。 Windows 8 以降では、コピーエンジンは、従来のコピーファイルコードパスの前に、オフロードデータ転送を透過的に使用しようとします。 コピー Api はほとんどのアプリケーション、ユーティリティ、およびシェルによって使用されるため、これらの呼び出し元は、既定でオフロードデータ転送機能を使用することができます (コードの変更やユーザーの介入はほとんどありません)。

次の手順は、コピーエンジンがオフロードデータ転送を試行する方法をまとめたものです。

1.  コピーエンジンは、読み取りトークンを取得するために、ソースファイルに対する[**読み取り\_FSCTL\_オフロード**](https://docs.microsoft.com/windows-hardware/drivers/ifs/fsctl-offload-read)を発行します。
2.  読み取りトークンの取得でエラーが発生した場合、コピーエンジンは従来の読み取りと書き込み (従来のコピーファイルのコードパス) にフォールバックします。 障害が、ソースボリュームがオフロードをサポートしていないことを示している場合、コピーエンジンは、プロセスごとのキャッシュのボリュームをマークします。 コピーエンジンは、プロセスごとのキャッシュ内のボリュームに対して、オフロードを試行しません。
3.  トークンが正常に取得された場合、コピーエンジンは[**FSCTL\_OFFLOAD\_** ](https://docs.microsoft.com/windows-hardware/drivers/ifs/fsctl-offload-write)を発行しようとします。これは、トークンによって論理的に表されるすべてのデータがオフロードされるまで、サイズが大きいチャンクのターゲットファイルに対して書き込みコマンドを実行します。
4.  オフロードの読み取りまたは書き込みを実行中にエラーが発生した場合は、コピーエンジンが読み取りと書き込みの従来のコードパスに戻り、オフロードコードパスが終了した場所から開始されます (読み取りまたは書き込みが切り捨てられた場所)。 移行先ボリュームがオフロードをサポートしていないか、ソースボリュームがターゲットボリュームに接続できないことがエラーによって示された場合、コピーエンジンは同じプロセスごとのキャッシュを更新し、これらのボリュームでオフロードを試行しないようにします。 このプロセスごとのキャッシュは定期的にリセットされます。

次の関数は、オフロードデータ転送をサポートしています。

-   **CopyFile**
-   **CopyFileEx**
-   **My.computer.filesystem.movefile**
-   **MoveFileEx**
-   **CopyFile2**

オフロードデータ転送は、次の関数ではサポートされていません。

-   **CopyFileTransacted**
-   **MoveFileTransacted**

### <a name="span-idsupported_offload_data_transfer_scenariosspanspan-idsupported_offload_data_transfer_scenariosspanspan-idsupported_offload_data_transfer_scenariosspansupported-offload-data-transfer-scenarios"></a><span id="Supported_Offload_Data_Transfer_Scenarios"></span><span id="supported_offload_data_transfer_scenarios"></span><span id="SUPPORTED_OFFLOAD_DATA_TRANSFER_SCENARIOS"></span>サポートされているオフロードデータ転送シナリオ

オフロード操作のサポートは、Hyper-v 記憶域スタックと Windows SMB ファイルサーバーに用意されています。 バッキング物理記憶域が ODX 操作をサポートする場合、呼び出し元は[**FSCTL\_オフロード\_** ](https://docs.microsoft.com/windows-hardware/drivers/ifs/fsctl-offload-read)を発行できます。また、読み取りと[**FSCTL\_オフロード\_** ](https://docs.microsoft.com/windows-hardware/drivers/ifs/fsctl-offload-write) vhd またはリモートファイル共有に存在するファイルへの書き込みを、仮想マシン内から実行することもできます。コンピューターまたは物理ハードウェア上。 次の図は、オフロードデータ転送のために最も基本的にサポートされているソースとターゲットを示しています。

![オフロードデータ転送のシナリオ](images/odx-scenario-3.png)

## <a name="span-idfile_system_filter_opt-in_model_and_impact_to_applicationsspanspan-idfile_system_filter_opt-in_model_and_impact_to_applicationsspanspan-idfile_system_filter_opt-in_model_and_impact_to_applicationsspanfile-system-filter-opt-in-model-and-impact-to-applications"></a><span id="File_System_Filter_Opt-In_Model_and_Impact_to_Applications"></span><span id="file_system_filter_opt-in_model_and_impact_to_applications"></span><span id="FILE_SYSTEM_FILTER_OPT-IN_MODEL_AND_IMPACT_TO_APPLICATIONS"></span>ファイルシステムフィルターのオプトインモデルとアプリケーションへの影響


Windows 8 以降では、フィルターマネージャーを使用して、サポートされている機能としてオフロード機能を指定できます。 ボリュームにアタッチされたファイルシステムフィルターは、特定のオフロード操作がサポートされているかどうかをまとめて判断できます。そうでない場合は、適切なエラーコードで操作が失敗します。

フィルターは、 [**FSCTL\_オフロード\_読み取り**](https://docs.microsoft.com/windows-hardware/drivers/ifs/fsctl-offload-read)と[**FSCTL\_オフ\_ロード**](https://docs.microsoft.com/windows-hardware/drivers/ifs/fsctl-offload-write)をサポートしていることを示す必要があります。また、driver Service 定義にある**Supportedfeatures**というレジストリ**DWORD**値を使用して書き込みを行います。レジストリの HKEY\_LOCAL\_MACHINE\\System\\CurrentControlSet\\Services\\&lt;フィルタードライバー名&gt;\\ます。 この値にはビットフィールドが含まれており、どの機能がオプトインされているかは、フィルターのインストール時に設定する必要があります。

現在、定義されているビットは次のとおりです。

| Flag                                               | 意味                               |
|----------------------------------------------------|---------------------------------------|
| サポートされている\_FS\_機能\_オフロード\_読み取り0x00000001  | フィルターは、FSCTL\_オフロード\_読み取りをサポートします  |
| サポートされている\_FS\_機能\_オフロード\_書き込み0x00000002 | フィルターでは、FSCTL\_オフロード\_書き込みがサポートされています |

 

フィルターオプトインモデルを有効または無効にするには、HKEY\_LOCAL\_MACHINE\\System\\CurrentControlSet\\Control\\FileSystem\\Filtersupported機能モードレジストリに存在する値に基づいて有効または無効にします。キー。次の値が含まれます。

| Filtersupportedのモード値 | 意味                                                                             |
|-----------------------------------|-------------------------------------------------------------------------------------|
| 0 (既定値)                       | 通常のオプトイン処理を実行します。                                                        |
| 1                                 | オプトインしない (すべてのフィルターがアタッチされている場合に SupportedFeatures を0に設定することに相当) |

 

### <a name="span-idtestingspanspan-idtestingspanspan-idtestingspantesting"></a><span id="Testing"></span><span id="testing"></span><span id="TESTING"></span>調べる

スタックのサポートされている機能を確認するには、fltmc ユーティリティ内に更新されたコマンドがあります。 **Fltmc instances – v \[volume\]:** 管理者特権を持つユーザーとして実行し、 *SprtFtrs*列を確認します。 フィルターの*SprtFtrs*値が0に設定されている場合は、フィルターがこのボリュームのオフロードをブロックしていることを意味します。 *SprtFtrs*フィールドが3に設定されている場合は、オフロード操作の両方がサポートされます。

### <a name="span-idchecking_feature_support_in_irp__processingspanspan-idchecking_feature_support_in_irp__processingspanspan-idchecking_feature_support_in_irp__processingspanchecking-feature-support-in-irp-processing"></a><span id="Checking_Feature_Support_in_IRP__Processing"></span><span id="checking_feature_support_in_irp__processing"></span><span id="CHECKING_FEATURE_SUPPORT_IN_IRP__PROCESSING"></span>IRP 処理で機能のサポートを確認しています

IRP 処理の一部として、 [**Fsrtlgetsupportedfeatures**](https://msdn.microsoft.com/library/windows/hardware/hh920378)ルーチンは、特定のボリュームスタックにアタッチされているすべてのフィルターについて、集計された**supportedfeatures**の状態を取得します。 I/o マネージャーや SRV (SMB) などのコンポーネントは、このルーチンを呼び出して、スタック上のすべてのフィルターについて**Supportedfeatures**の状態を検証します。 独自のオフロード Irp をロールするコンポーネントは、その操作のオプトインサポートを検証するために、この関数を呼び出す必要があります。

### <a name="span-idconsiderations_for_filter_driversspanspan-idconsiderations_for_filter_driversspanspan-idconsiderations_for_filter_driversspanconsiderations-for-filter-drivers"></a><span id="Considerations_for_Filter_Drivers"></span><span id="considerations_for_filter_drivers"></span><span id="CONSIDERATIONS_FOR_FILTER_DRIVERS"></span>フィルタードライバーに関する考慮事項

オフロードデータ転送は、データセンター内でデータを移動する新しい方法です。 コアコピーエンジンにはオフロードロジックが統合されているため、既定では、多くのアプリケーションは、明示的にオプトインせずにオフロードデータ移動を実行できます。 そのため、フィルター開発者は、これらの新しい操作がフィルターに与える影響を理解する必要があります。 これらの操作を十分に理解していない場合、または新しいデータフローを評価しない場合、データが不整合になったり破損したりする可能性があります。 次の一覧は、フィルター開発者がオフロードでメモする一連のアクション項目をまとめたものです。

-   新しいデータフロー、フィルターへの影響、およびこれらのオフロード操作をサポートするフィルターの機能について理解します。
-   フィルターインストーラーを更新して、 **Supportedfeatures**の REG\_DWORD 値を HKLM\\システム\\CurrentControlSet\\Services\\\[filter\] サブキーに追加します。 これを初期化してオフロード機能を指定します。
-   オフロード操作に対処するフィルターについては、登録を**IRP\_MJ\_ファイル\_システム\_制御**に更新して、 [**FSCTL\_オフロード\_読み取り**](https://docs.microsoft.com/windows-hardware/drivers/ifs/fsctl-offload-read)と[**FSCTL\_オフロードを処理\_書き込み**](https://docs.microsoft.com/windows-hardware/drivers/ifs/fsctl-offload-write)。
-   オフロード操作をブロックする必要があるフィルターの場合は、ステータスコードの状態を返します。フィルター内からサポートされていない状態\_\_サポートされていません。 エンドユーザーが変更できるように、ブロッキングオフロード操作を強制するためにレジストリ値に依存しないでください。 フィルターでは、オフロード操作を明示的に許可または禁止する必要があります。

## <a name="span-idcopy_tokensspanspan-idcopy_tokensspanspan-idcopy_tokensspancopy-tokens"></a><span id="Copy_Tokens"></span><span id="copy_tokens"></span><span id="COPY_TOKENS"></span>トークンのコピー


オフロード操作では、ファイルデータは i/o スタックに表示されません。 代わりに、データの論理プロキシである512バイトのトークンとして表示されます。 このトークンは、ストレージサブシステムによって生成されるベンダー固有の形式の非透過的で一意の文字列であるか、またはデータのパターンを表す既知の型 (論理的にはゼロに相当するデータ範囲) であることができます。 トークンがプロキシになっているデータを変更すると、トークンが無効になるか、またはストレージサブシステムがベンダー固有の手段 (スナップショットメカニズムなど) によって元のデータを保持するようになります。 ファイル内の指定された範囲に対するその後のオフロード要求では、一意のトークンが生成されます。

明確に定義されたデータのパターンを表すトークンのクラスがあります。 よく知られている最も一般的なトークンは、ゼロに相当するゼロトークンです。 トークンが既知のトークンとして定義されている場合、**ストレージ\_オフロード\_トークン**構造内の**TokenType**メンバーは、\_既知\_既知の種類\_\_\_オフロードトークンに設定されます。 このフィールドが設定されている場合、 **WellKnownPattern**メンバーによって、トークンが持つデータのパターンが決まります。

-   **WellKnownPattern**フィールドが 記憶域\_オフロード\_パターン\_0 またはストレージ\_オフロード\_ゼロ\_\_保護\_情報に設定されている場合は、ゼロトークンを示します。 このトークンが[**FSCTL\_オフロード\_読み取り**](https://docs.microsoft.com/windows-hardware/drivers/ifs/fsctl-offload-read)操作によって返された場合は、目的のファイル範囲に含まれるデータが論理的に0と等しいことを示します。 このトークンが[**FSCTL\_オフロード\_書き込み**](https://docs.microsoft.com/windows-hardware/drivers/ifs/fsctl-offload-write)操作に提供された場合、書き込まれるファイルの目的の範囲を論理的にゼロにする必要があることを示します。
-   ゼロトークン以外に、現在定義されている他の既知のトークンパターンはありません。 ユーザーが独自の既知のトークンパターンを定義することは推奨されません。

## <a name="span-idtruncationspanspan-idtruncationspanspan-idtruncationspantruncation"></a><span id="Truncation"></span><span id="truncation"></span><span id="TRUNCATION"></span>示さ


Windows が通信する基になる記憶域サブシステムでは、オフロード操作で必要だったデータを処理することができません。 これを切り捨てと呼びます。 オフロード読み取りでは、返されたトークンが、要求されたデータの範囲を下回ることを意味します。 これは、 [**FSCTL\_オフロード\_読み取り\_出力**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_fsctl_offload_read_output)構造の**transferlength**メンバーによって示されます。これは、読み取るファイルの範囲の先頭からのバイト数です。 オフロード書き込みの場合、切り捨ては、意図したよりも少ないデータが書き込まれたことを示します。 この値は **、書き込まれる**ファイルの範囲の先頭からのバイト数である、 [**FSCTL\_OFFLOAD\_の書き込み\_出力**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_fsctl_offload_write_output)構造体によって示されます。 コマンド処理のエラー、または大きな範囲のスタック内の制限により、切り捨てが発生します。

次の2つのシナリオでは、読み取りまたは書き込みのオフロードする範囲が NTFS によって切り捨てられます。

1.  VDL がファイルの末尾 (EOF) より前にある場合、コピー範囲は有効なデータ長 (VDL) に切り捨てられます。 これは、VDL が論理セクターの境界に合わせて調整されていることを前提としています。

    ![eof の前に発生した vdl](images/odx-vdl-1.png)

    [**FSCTL\_オフロード\_読み取り**](https://docs.microsoft.com/windows-hardware/drivers/ifs/fsctl-offload-read)操作の実行中は、フラグオフロード\_\_フラグの読み取りフラグ\_現在の\_の範囲を超える\_0\_すべての\_は、 [**FSCTL\_オフロードで設定され\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_fsctl_offload_read_output)ファイルの残りの部分にゼロが含まれており、 **transferlength**メンバーが VDL に切り捨てられていることを示す読み取り\_出力構造体。

2.  シナリオ1に似ていますが、VDL が論理セクターの境界に揃っていない場合、必要な範囲は NTFS によって次の論理セクターの境界に切り捨てられます。

    ![セクター境界での vdl の不整合](images/odx-vdl-2.png)

## <a name="span-idlimitationsspanspan-idlimitationsspanspan-idlimitationsspanlimitations"></a><span id="Limitations"></span><span id="limitations"></span><span id="LIMITATIONS"></span>制限事項


-   オフロード操作は、NTFS ボリュームでのみサポートされます。
-   リモート共有が NTFS ボリュームであり、サーバーで Windows Server 2012 が実行されている場合は、リモートファイルサーバーを使用してオフロード操作がサポートされます (リモートスタックでオフロード操作もサポートされている場合)。
-   NTFS は、Bitlocker または NTFS 暗号化 (EFS) で暗号化されたファイル、重複しないファイル、圧縮ファイル、常駐ファイル、スパースファイル、または TxF トランザクションに参加しているファイルに対して実行されるオフロード FSCTLs をサポートしていません。
-   NTFS では、volsnap スナップショット内のファイルに対して実行されるオフロード FSCTLs はサポートされていません。
-   目的のファイル範囲がソースデバイスの論理セクターサイズに固定されていない場合、または目的のファイル範囲がターゲットデバイスの論理セクターサイズに固定されていない場合、NTFS はオフロード FSCTL を失敗させます。 これは、キャッシュされていない IO と同じセマンティクスに従います。
-   [**FSCTL\_オフロード\_書き込み**](https://docs.microsoft.com/windows-hardware/drivers/ifs/fsctl-offload-write)の前に、コピー先のファイルが事前に割り当てられている (**setendoffile**と**setallocation**ではない) 必要があります。
-   負荷分散の読み取りとオフロードの書き込みでは、NTFS はまず[**CcCoherencyFlushAndPurgeCache**](https://msdn.microsoft.com/library/windows/hardware/ff539032)を呼び出して、変更されたデータをシステムキャッシュにコミットします。 これは、非キャッシュ IO と同じセマンティクスです。

 

 





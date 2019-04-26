---
title: オフロード データ転送
description: 頻繁にファイル システムの利用状況は、コンピューター間または同じコンピューター内でデータを転送します。
ms.assetid: 66006CC0-8902-47CD-8E7C-187FE5BA71EF
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 455c3728e7184f2ecd8093836b27492c5f49cdec
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63352816"
---
# <a name="offloaded-data-transfers"></a>オフロード データ転送


頻繁にファイル システムの利用状況は、コンピューター間または同じコンピューター内でデータを転送します。 標準を使用して**ReadFile**と**WriteFile**関数が機能の観点からも機能しますが、大量のデータの移動が伴いますのレベルを すべてのシステムと、ネットワーク経由で可能性があります。 転送と、システムを接続するネットワークに関連するシステムの可用性に影響を与えることができます。 多くの記憶域サブシステムで利用できる高度な機能は、データ移動の '面倒' タスクを実行するより効率的な手段を提供します。

Windows 8 以降、アプリケーションを利用、記憶域サブシステムへのデータ移動の処理をオフロードするこれらの機能できます。 通常、ファイル システム フィルターは読み取りをインターセプトすることでこれらのアクションを監視し、ボリュームへの書き込み要求。 その他のアクションは、フィルター オフロード データ転送を意識する必要があります。

## <a name="span-idtypicaldatatransfersspanspan-idtypicaldatatransfersspanspan-idtypicaldatatransfersspantypical-data-transfers"></a><span id="Typical_Data_Transfers"></span><span id="typical_data_transfers"></span><span id="TYPICAL_DATA_TRANSFERS"></span>一般的なデータ転送


データの移動、アプリケーションのシナリオで今日は簡単です。 読み取り作成し、ローカル メモリにデータ新しい場所にバックアップにはが含まれます。 次の図は、このシナリオを示します。

このシナリオでは、インテリジェントな記憶域配列 (ISA) を通じて公開される、独自の仮想ディスクで 2 つの別々 のファイル サーバー上の 2 つの場所の間でファイルをコピーする必要があります。 発信側のシステムは、まず、ソース仮想ディスクからデータをローカル バッファーに読み取る必要があります。 その後は、パッケージ化し、いくつかのトランスポートとプロトコル (SMB over 1 gbe) のようなデータを受信すると、ローカル バッファーに出力し、2 つ目のシステム データを送信します。 次に、ターゲット システムでは、変換先の仮想ディスクにデータを書き込みます。 このシナリオでは、実行される複数回さまざまなアプリケーションで毎日データ転送の非常に典型的な読み取り/書き込みメソッドについて説明します。

![一般的なデータ転送](images/odx-scenario-1.png)

標準では、読み取りし、ほとんどのシナリオでも作業を書き込み、中には、同じインテリジェントな記憶域配列によって管理される仮想ディスクにコピーする目的でデータを配置する可能性があります。 これは、データが移動される、サーバー上に、配列外間でのネットワーク トランスポートには、別のサーバーに、同じ配列に、もう一度を意味します。 サーバー内やネットワーク トランスポートのデータの移動の機能が大幅にこれらのシステムの可用性に影響を与えるデータ移動のスループットがスループットとネットワークの可用性によって制限されることは言うまでもありません。

## <a name="span-idoffloadeddatatransfersodxspanspan-idoffloadeddatatransfersodxspanspan-idoffloadeddatatransfersodxspanoffloaded-data-transfers-odx"></a><span id="Offloaded_Data_Transfers__ODX_"></span><span id="offloaded_data_transfers__odx_"></span><span id="OFFLOADED_DATA_TRANSFERS__ODX_"></span>オフロード データ転送 (ODX)


### <a name="span-idoffloadingthedatatransferspanspan-idoffloadingthedatatransferspanspan-idoffloadingthedatatransferspanoffloading-the-data-transfer"></a><span id="Offloading_the_Data_Transfer"></span><span id="offloading_the_data_transfer"></span><span id="OFFLOADING_THE_DATA_TRANSFER"></span>データ転送のオフロード

Windows 8 のオフロード データ転送メソッドを容易にするには、2 つの新しい FSCTLs が導入されました。 これは、サーバー記憶域サブシステム内で適切に行われる移動をビットにビットの移行の負担を移動します。 コマンドのセマンティクスを視覚化する最善の方法では、バッファーの読み取りとバッファーの書き込みに似ていますとして捉えることです。

<span id="FSCTL_OFFLOAD_READ"></span><span id="fsctl_offload_read"></span>[**FSCTL\_オフロード\_読み取り**](https://msdn.microsoft.com/library/windows/hardware/hh451101)  
このコントロールの要求で必要な長さおよび読み取るファイル内でオフセットを取得する、 [ **FSCTL\_オフロード\_読み取り\_入力**](https://msdn.microsoft.com/library/windows/hardware/hh451104)構造体。 でサポートされている場合、ファイルをホストする記憶域サブシステムがストレージ コマンドを読み取り、関連付けられているオフロードを受信し、読み取りコマンド オフロードの時に読み取られるデータの論理表現であるトークンを生成します。 呼び出し元にこのトークン文字列が返されます、 [ **FSCTL\_オフロード\_読み取り\_出力**](https://msdn.microsoft.com/library/windows/hardware/hh451109)構造体。

<span id="FSCTL_OFFLOAD_WRITE"></span><span id="fsctl_offload_write"></span>[**FSCTL\_オフロード\_書き込み**](https://msdn.microsoft.com/library/windows/hardware/hh451122)  
この制御要求の内に書き込まれるファイル、希望の長さ、書き込みと書き込まれるデータの論理表現であるトークンのオフセットを取得します。 、サポートされている場合、書き込まれるファイルをホストしている記憶域サブシステムは、関連付けられているオフロード書き込みストレージ コマンドを受け取ります。 最初に指定されたトークンを認識しようし、可能であれば、書き込み操作を実行します。 Windows では、下に、書き込み操作が完了し、そのため、ファイル システムと記憶域スタック上のコンポーネントには、データ移動表示されません。 データ移動が完了すると、呼び出し元に書き込まれたバイト数が返されます。

![オフロード データ転送](images/odx-scenario-2.png)

最初の図と同様に、2 台のサーバー上の 2 つの仮想ディスクの間の単純なファイル コピーが表示されます。 通常の読み取りと書き込みを行うと、代わりには、記憶域配列への移行をビットの面倒をオフロードします。 最初のシステムでは、読み取り、配列の最初の仮想ディスクのリージョン内で読み取られるデータの特定の時点のビューを表すトークンを生成する要求操作オフロードを発行します。 最初のシステムは、2 番目のシステムは、さらにオフロードする問題への書き込み操作、トークンを使用して 2 つ目の仮想ディスクにトークンを送信します。 配列は、トークンを解釈し、仮想ディスク間のデータ移動を実行しようとしています。 インテリジェントな記憶域配列内で、2 つのホスト間ではなく、実際のデータ転送が発生することがわかります。 これによって、事実上、システム間のネットワーク トラフィックを排除しながら、2 つのシステムの可用性が大幅に向上します。

### <a name="span-idintegrationwiththecopyenginespanspan-idintegrationwiththecopyenginespanspan-idintegrationwiththecopyenginespanintegration-with-the-copy-engine"></a><span id="Integration_with_the_Copy_Engine"></span><span id="integration_with_the_copy_engine"></span><span id="INTEGRATION_WITH_THE_COPY_ENGINE"></span>コピー エンジンとの統合

Windows のコア コピー エンジンを使って**CopyFile**および関連する関数。 Windows 8 以降では、コピー エンジンに透過的にしようと従来のコピーのファイルのコード パスの前にデータ転送のオフロードを使用します。 コピー Api が、ユーティリティ、ほとんどのアプリケーションで使用される、シェルによってこれらの呼び出し元が存在する場合、既定では、ほとんど使用オフロード データ転送の機能することが後で、変更、またはユーザーの介入をコードします。

次の手順では、コピー エンジンが、オフロード データ転送を試行する方法をまとめてください。

1.  コピー エンジンの問題、 [ **FSCTL\_オフロード\_読み取り**](https://msdn.microsoft.com/library/windows/hardware/hh451101)読み取りトークンを取得するソース ファイル。
2.  読み取り、トークンの取得中にエラーがあった場合、コピー エンジンは従来の読み取りにフォールバックし、(従来のコピー ファイルのコード パス) を書き込みます。 エラーは、ソース ボリュームがオフロードをサポートしていないことを示します、コピー エンジンも、プロセスごとのキャッシュのボリュームをマークします。 コピー エンジンでは、プロセスごとのキャッシュのボリュームに対して以上の負荷を軽減することは試みません。
3.  コピー エンジンが発行しようとした場合は、トークンが正常に取得すると、 [ **FSCTL\_オフロード\_書き込み**](https://msdn.microsoft.com/library/windows/hardware/hh451122)であるすべてのデータの大きなチャンクでターゲット ファイルをコマンド書き込まれるオフロードされたトークンによって表される論理的にします。
4.  オフロードを実行するときにエラーで読み取りまたは書き込みの結果の読み取りと書き込み、従来のコード パスにコピー エンジンは、オフロードがパスをコードからオフ (場所、読み取りまたは書き込みが切り捨てられました) が終了しました。 エラーには、移行先ボリュームがオフロードをサポートしていないか、ソース ボリュームが回復先ボリュームに到達できないことが示されている場合、コピー エンジンは、これらのボリュームでオフロードを試行しませんので同じのプロセスごとのキャッシュを更新します。 このプロセスごとのキャッシュを定期的にリセットされます。

次の関数は、オフロード データ転送をサポートします。

-   **CopyFile**
-   **CopyFileEx**
-   **MoveFile**
-   **MoveFileEx**
-   **CopyFile2**

次の関数は、サポートのオフロード データ転送しないを実行します。

-   **CopyFileTransacted**
-   **MoveFileTransacted**

### <a name="span-idsupportedoffloaddatatransferscenariosspanspan-idsupportedoffloaddatatransferscenariosspanspan-idsupportedoffloaddatatransferscenariosspansupported-offload-data-transfer-scenarios"></a><span id="Supported_Offload_Data_Transfer_Scenarios"></span><span id="supported_offload_data_transfer_scenarios"></span><span id="SUPPORTED_OFFLOAD_DATA_TRANSFER_SCENARIOS"></span>サポートされているオフロード データ転送のシナリオ

HYPER-V の記憶域スタックと、Windows の SMB ファイル サーバー、オフロード操作のサポートが提供されます。 呼び出し元が発行できるバッキング物理記憶域は、ODX 操作をサポートする、 [ **FSCTL\_オフロード\_読み取り**](https://msdn.microsoft.com/library/windows/hardware/hh451101)と[ **FSCTL\_オフロード\_書き込み**](https://msdn.microsoft.com/library/windows/hardware/hh451122) Vhd 上またはリモート ファイル共有上に存在するファイルをかどうかの仮想マシンまたは物理ハードウェア上でします。 次の図は、オフロード データ転送の最も基本的なサポートされているソースと宛先ターゲットを示します。

![オフロード データ転送のシナリオ](images/odx-scenario-3.png)

## <a name="span-idfilesystemfilteropt-inmodelandimpacttoapplicationsspanspan-idfilesystemfilteropt-inmodelandimpacttoapplicationsspanspan-idfilesystemfilteropt-inmodelandimpacttoapplicationsspanfile-system-filter-opt-in-model-and-impact-to-applications"></a><span id="File_System_Filter_Opt-In_Model_and_Impact_to_Applications"></span><span id="file_system_filter_opt-in_model_and_impact_to_applications"></span><span id="FILE_SYSTEM_FILTER_OPT-IN_MODEL_AND_IMPACT_TO_APPLICATIONS"></span>ファイル システム フィルター オプトイン モデルとアプリケーションへの影響


フィルター マネージャー、Windows 8 では、以降では、サポートされている機能としてオフロード機能を指定するフィルターできます。 ボリュームに接続されているファイル システム フィルターまとめてを調べることはありません。 または、オフロードされた特定の操作はサポートされている場合そうでない場合は、適切なエラー コードで、操作が失敗します。

フィルターはサポートしていることを示す必要があります[ **FSCTL\_オフロード\_読み取り**](https://msdn.microsoft.com/library/windows/hardware/hh451101)と[ **FSCTL\_オフロード\_書き込み** ](https://msdn.microsoft.com/library/windows/hardware/hh451122)レジストリを通じて**DWORD**という名前の値**SupportedFeatures**、レジストリの HKEY にドライバー サービス定義にある\_ローカル\_マシン\\システム\\CurrentControlSet\\サービス\\&lt;フィルター ドライバー名&gt;\\します。 この値には、ビットがどの機能がオプトイン、およびフィルターのインストール時に設定する必要がありますを決定するビット フィールドが含まれています。

現時点では、定義済みのビットには。

| Flag                                               | 説明                               |
|----------------------------------------------------|---------------------------------------|
| サポートされている\_FS\_機能\_オフロード\_読み取り 0x00000001  | フィルターが FSCTL をサポートする\_オフロード\_読み取り  |
| サポートされている\_FS\_機能\_オフロード\_書き込み 0x00000002 | フィルターが FSCTL をサポートする\_オフロード\_書き込み |

 

フィルター オプトイン モデルを有効にすることができます、または無効になっていますが、HKEY に存在する値に基づく\_ローカル\_マシン\\システム\\CurrentControlSet\\コントロール\\FileSystem\\FilterSupportedFeaturesMode レジストリ キーは、次の値があります。

| FilterSupportedFeaturesMode 値 | 説明                                                                             |
|-----------------------------------|-------------------------------------------------------------------------------------|
| 0 (既定)                       | 通常のオプトイン処理の操作を行います。                                                        |
| 1                                 | 決してオプトイン (と等しい設定をすべてフィルターで 0 に SupportedFeatures 接続) |

 

### <a name="span-idtestingspanspan-idtestingspanspan-idtestingspantesting"></a><span id="Testing"></span><span id="testing"></span><span id="TESTING"></span>テスト

スタックのサポートされる機能を確認するには、fltmc ユーティリティ内でコマンドを更新します。 実行**fltmc インスタンス – v\[ボリューム\]:** 、管理者特権でのユーザーとチェックとして、 *SprtFtrs*列。 場合、 *SprtFtrs*フィルターの値が 0 に設定されて、このボリュームでオフロード フィルターによってブロックされていることを意味します。 場合、 *SprtFtrs*フィールド 3 に設定されて、両方のオフロード操作がサポートされます。

### <a name="span-idcheckingfeaturesupportinirpprocessingspanspan-idcheckingfeaturesupportinirpprocessingspanspan-idcheckingfeaturesupportinirpprocessingspanchecking-feature-support-in-irp-processing"></a><span id="Checking_Feature_Support_in_IRP__Processing"></span><span id="checking_feature_support_in_irp__processing"></span><span id="CHECKING_FEATURE_SUPPORT_IN_IRP__PROCESSING"></span>IRP の処理でサポートされる機能のチェック

IRP の処理の一環として、 [ **FsRtlGetSupportedFeatures** ](https://msdn.microsoft.com/library/windows/hardware/hh920378)ルーチンを取得、集計された**SupportedFeatures**特定のボリュームに接続されているすべてのフィルターの状態スタックです。 I/O マネージャーや SRV (SMB) などのコンポーネントが検証するには、このルーチンを呼び出し、 **SupportedFeatures**スタック上のすべてのフィルターの状態。 自分をロール コンポーネント Irp をオフロードする操作のためのオプトイン サポートを検証するには、この関数を呼び出す必要があります。

### <a name="span-idconsiderationsforfilterdriversspanspan-idconsiderationsforfilterdriversspanspan-idconsiderationsforfilterdriversspanconsiderations-for-filter-drivers"></a><span id="Considerations_for_Filter_Drivers"></span><span id="considerations_for_filter_drivers"></span><span id="CONSIDERATIONS_FOR_FILTER_DRIVERS"></span>フィルター ドライバーに関する考慮事項

オフロード データ転送は、データ センターでデータを移動する新しい方法です。 既定では多くのアプリケーションはコア コピー エンジンのオフロード ロジックの統合が原因で明示的に停止せずにオフロードされたデータの移動を実行する機能があります。 その結果、フィルター開発者は、これらの新しい操作がフィルターに与える影響を理解する必要があります。 これらの操作を完全に理解していないか、新しいデータが評価されていないフローできるデータになる不整合や破損のシナリオで発生する可能性があります。 次の一覧は、一連の項目にメモしてを実行するフィルター開発者向けの負荷を軽減するアクションをまとめたものです。

-   新しいデータ フロー、フィルター、およびこれらのオフロードされた操作をサポートするために、フィルターの機能への影響について説明します。
-   更新、フィルターのインストーラー、レジストリを追加する\_の DWORD 値**SupportedFeatures** HKLM に\\システム\\CurrentControlSet\\サービス\\\[フィルター\]サブキー。 オフロード機能を指定することを初期化します。
-   対象とするフィルターは、操作をオフロード、更新する登録**IRP\_MJ\_ファイル\_システム\_コントロール**を処理する[ **FSCTL\_オフロード\_読み取り**](https://msdn.microsoft.com/library/windows/hardware/hh451101)と[ **FSCTL\_オフロード\_書き込み**](https://msdn.microsoft.com/library/windows/hardware/hh451122)します。
-   オフロードの操作をブロックする必要があるフィルターは、状態コードの状態を返すの\_いない\_フィルター内からサポートされています。 エンドユーザーによって変更できるため、ブロックのオフロード操作を適用するレジストリ値に依存しないでください。 フィルターは、明示的に許可またはオフロード操作を許可しないようにする必要があります。

## <a name="span-idcopytokensspanspan-idcopytokensspanspan-idcopytokensspancopy-tokens"></a><span id="Copy_Tokens"></span><span id="copy_tokens"></span><span id="COPY_TOKENS"></span>トークンをコピーします。


オフロードされた操作は、ファイル データは、I/O スタックには表示されません。 代わりに、データの論理プロキシである 512 バイトのトークンとして、これは見られます。 このトークンは不透明な直線および一意文字列であるか、記憶域サブシステムによって生成されたベンダー固有の書式のかを (0 に論理的に相当するデータの範囲) などのデータのパターンを表すよく知られている型であることができます。 トークンのプロキシは、データへの変更は、トークンが無効のいずれかの結果または一部のベンダー固有で、元のデータを保持する記憶域サブシステムの意味 (など、スナップショット メカニズムを使用)。 後続のオフロードは、ファイルで指定した範囲に要求の一意のトークンでの結果を読み取ります。

適切に定義されているデータのパターンを表すトークンのクラスがあります。 最も一般的なよく知られたトークンは、ゼロと同等である 0 トークン。 トークンが、Well Known トークンとして定義されている場合、 **TokenType**内のメンバー、**ストレージ\_オフロード\_トークン**構造体のセットをストレージ\_オフロード\_トークン\_型\_も\_呼ばれます。 このフィールドが設定されている場合、 **WellKnownPattern**トークンは、データのパターンはどのメンバーを決定します。

-   ときに、 **WellKnownPattern**フィールドのセットをストレージ\_オフロード\_パターン\_0 またはストレージ\_オフロード\_パターン\_0\_\_保護\_については、0 トークン示します。 このトークンがによって返されるときに、 [ **FSCTL\_オフロード\_読み取り**](https://msdn.microsoft.com/library/windows/hardware/hh451101)操作、目的のファイルの範囲内に含まれるデータが 0 に論理的に等価なであることを示します。 このトークンを指定する場合、 [ **FSCTL\_オフロード\_書き込み**](https://msdn.microsoft.com/library/windows/hardware/hh451122)操作に書き込まれるファイルの必要な範囲を論理的にゼロをことを示します。
-   0 トークン以外は、現在定義されているその他の既知のトークンのパターンはありません。 ユーザーが独自の Well Known トークン パターンを定義しないでください。

## <a name="span-idtruncationspanspan-idtruncationspanspan-idtruncationspantruncation"></a><span id="Truncation"></span><span id="truncation"></span><span id="TRUNCATION"></span>切り捨て


Windows と通信する、基になる記憶域サブシステムでは、オフロード操作に必要な少なくデータを処理できます。 これは切り捨てと呼ばれます。 読み取るオフロード、返されたトークンを表すさまざまなデータをよりも小さいが要求されたこのを意味します。 これにより、表示、 **TransferLength**内のメンバー、 [ **FSCTL\_オフロード\_読み取り\_出力**](https://msdn.microsoft.com/library/windows/hardware/hh451109)構造体は、これは、読み取るファイルの範囲の先頭からのバイト数。 オフロード書き込み、切り捨ては、必要ながよりも低いデータが書き込まれたことを示します。 これにより、表示、 **LengthWritten**内のメンバー、 [ **FSCTL\_オフロード\_書き込み\_出力**](https://msdn.microsoft.com/library/windows/hardware/hh451130)構造体は、これは、書き込まれるファイルの範囲の先頭からのバイト数。 コマンドの処理、または、広範囲のスタックでの制限事項のエラーは、切り捨てが発生します。

読み取りまたは書き込み、NTFS をオフロードする範囲を切り捨てます 2 つのシナリオがあります。

1.  コピーの範囲は場合、VDL をファイル (EOF) の終了前に有効なデータの長さ (VDL) に切り捨てられます。 これは VDL を論理セクター境界に配置されていることを前提としています、それ以外の場合のシナリオを参照してください。

    ![vdl eof する前に発生します。](images/odx-vdl-1.png)

    中に、 [ **FSCTL\_オフロード\_読み取り**](https://msdn.microsoft.com/library/windows/hardware/hh451101)操作、フラグ オフロード\_読み取り\_フラグ\_すべて\_ゼロ\_超える\_現在\_範囲を設定、 [ **FSCTL\_オフロード\_読み取り\_出力**](https://msdn.microsoft.com/library/windows/hardware/hh451109)構造を示すファイルの残りの部分にゼロが含まれていると、 **TransferLength** VDL にメンバーが切り捨てられます。

2.  類似していますが VDL が論理セクターの境界では、必要な範囲に固定されていないときにシナリオの 1 には、NTFS によって、次の論理セクター境界に切り捨てられます。

    ![セクターの境界に揃っていない vdl](images/odx-vdl-2.png)

## <a name="span-idlimitationsspanspan-idlimitationsspanspan-idlimitationsspanlimitations"></a><span id="Limitations"></span><span id="limitations"></span><span id="LIMITATIONS"></span>制限事項


-   オフロード操作は、NTFS ボリュームでのみサポートされます。
-   オフロード場合、そのリモート共有は NTFS ボリュームと、サーバーは (リモートのスタックは、オフロード操作もサポートしています。 と仮定)、Windows Server 2012 を実行している場合、リモート ファイル サーバーで操作がサポートされます。
-   NTFS は Bitlocker または NTFS 暗号化 (EFS)、重複除去ファイル、圧縮されたファイル、ファイル、スパース ファイルは、暗号化されたファイルに対して FSCTLs オフロードをサポートしていないか、TxF のトランザクションに参加しているファイルします。
-   NTFS は volsnap スナップショット内のファイルに対して FSCTLs オフロードをサポートしていません。
-   目的のファイルの範囲は、ソース デバイス上の論理セクター サイズに整列されていない場合、または目的のファイルの範囲は先デバイス上の論理セクター サイズに整列されていない場合、NTFS ではオフロード FSCTL は失敗します。 これは、非キャッシュの IO と同じセマンティクスに従います。
-   リンク先のファイルは、割り当て済みである必要があります (**SetEndOfFile**なく**SetAllocation**) する前に[ **FSCTL\_オフロード\_書き込み**](https://msdn.microsoft.com/library/windows/hardware/hh451122).
-   NTFS の最初の呼び出しでオフロードの読み取りと書き込みのオフロード処理、 [ **CcCoherencyFlushAndPurgeCache** ](https://msdn.microsoft.com/library/windows/hardware/ff539032)をコミットするいずれかのシステム キャッシュ内のデータを変更します。 これは、同じ IO の非キャッシュとしてセマンティックです。

 

 





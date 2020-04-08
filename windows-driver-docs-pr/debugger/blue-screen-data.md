---
title: ブルー スクリーンのデータ
description: Microsoft Windows が安全なシステム操作を侵害する状態を検出すると、システムは停止します。 この状態は、バグチェックまたは停止エラーと呼ばれます。
ms.assetid: 8cc42643-e231-49dd-96b0-6cb528d5d7a9
keywords:
- ブルースクリーンデータ Windows デバッグ
ms.date: 03/30/2020
topic_type:
- apiref
api_name:
- Blue Screen Data
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 78254c231218357d21daac30063fc578b02bd8c3
ms.sourcegitcommit: 071200c3366dbb26985dd7077bd6c4cb96e969c2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/07/2020
ms.locfileid: "80812516"
---
# <a name="blue-screen-data"></a>ブルー スクリーンのデータ

> [!NOTE]
> このトピックはプログラマーを対象としています。 カスタマーのシステムでブルー スクリーンとバグ チェック コードが表示された場合は、「[ブルー スクリーン エラーのトラブルシューティング](https://go.microsoft.com/fwlink/p/?linkid=183646)」を参照してください。

**注**   IT プロフェッショナルまたはサポートエージェントの場合は、 [Microsoft サポートに問い合わせる前に、この記事の「ブルースクリーンのトラブルシューティング」または「エラーの停止」](https://support.microsoft.com/help/3106831/)を参照してください。

Microsoft Windows が安全なシステム操作を侵害する状態を検出すると、システムは停止します。 この状態は*バグチェック*と呼ばれます。 また、一般に、*システムクラッシュ*、*カーネルエラー*、または*停止エラー*とも呼ばれます。

オペレーティングシステムの整合性が損なわれた後も OS の実行を継続できる場合、データが破損したり、システムのセキュリティが侵害されたりする可能性があります。

クラッシュダンプがシステムで有効になっている場合は、クラッシュダンプファイルが作成されます。

カーネルデバッガーがアタッチされ、アクティブになっている場合は、デバッガーを使用してクラッシュを調査できるように、システムによって中断が発生します。

デバッガーがアタッチされていない場合は、エラーに関する情報を含む青いテキスト画面が表示されます。 この画面は、*青い画面*、*バグチェック画面*、または*停止画面*と呼ばれます。

Windows の insider ビルドを使用している場合は、テキストが緑色の背景に表示されます。

ブルースクリーンの正確な外観は、エラーの原因によって異なります。

ブルースクリーンの1つの例を次に示します。

![バグチェックの例 qr コードを使用した windows 10 ブルースクリーンの例](images/bug-check-example-blue-screen-page-fault.png)

[[**ページ\_のエラー\_] など、\_のない\_領域に**](bug-check-0x50--page-fault-in-nonpaged-area.md)停止コードが表示されます。 使用可能な場合は、実行されていたコードのモジュール名も表示されます。たとえば、AcmeVideo. sys のようになります。

[カーネルモードのダンプファイル](kernel-mode-dump-files.md)が作成されている場合は、ダンプが書き込まれている間、このファイルにはパーセンテージが表示されます。

「[バグチェックコードリファレンス](bug-check-code-reference2.md)」に記載されている各ストップコードに関連付けられたストップコードの16進値があります。

## <span id="ddk_blue_screen_data_dbg"></span><span id="DDK_BLUE_SCREEN_DATA_DBG"></span>


### <a name="span-idgathering_the_stop_code_parametersspanspan-idgathering_the_stop_code_parametersspanspan-idgathering_the_stop_code_parametersspangathering-the-stop-code-parameters"></a><span id="Gathering_the_Stop_Code_Parameters"></span><span id="gathering_the_stop_code_parameters"></span><span id="GATHERING_THE_STOP_CODE_PARAMETERS"></span>ストップコードパラメーターを収集しています

各バグチェックコードには、追加情報を提供する4つのパラメーターが関連付けられています。 これらのパラメーターについては、「[バグチェックコードリファレンス](bug-check-code-reference2.md)(各ストップコード)」を参照してください。

4つの stop コードパラメーターを収集するには、複数の方法があります。

-   イベントビューアーで Windows システムログを確認します。 バグチェックのイベントプロパティには、4つの stop コードパラメーターが一覧表示されます。 詳しくは、[イベント ビューアーの使用](https://support.microsoft.com/hub/4338813/windows-help#1TC=windows-7)に関するページをご覧ください。

-   生成されたダンプファイルを読み込み、 [ **! analyze**](-analyze.md)コマンドとデバッガーをアタッチして使用します。 詳細については、「 [WinDbg を使用したカーネルモードダンプファイルの分析](analyzing-a-kernel-mode-dump-file-with-windbg.md)」を参照してください。

-   障害が発生した PC にカーネルデバッガーをアタッチします。 停止コードが発生すると、デバッガーの出力には、stop code の16進数値の後に4つのパラメーターが含まれます。

    ```dbgcmd
    *******************************************************************************
    *                                                                             *
    *                        Bugcheck Analysis                                    *
    *                                                                             *
    *******************************************************************************

    Use !analyze -v to get detailed debugging information.

    BugCheck 9F, {3, ffffe000f38c06a0, fffff803c596cad0, ffffe000f46a1010}

    Implicit thread is now ffffe000`f4ca3040
    Probably caused by : hidusb.sys
    ```

### <a name="span-idbug_check_symbolic_namesspanspan-idbug_check_symbolic_namesspanbug-check-symbolic-names"></a><span id="bug_check_symbolic_names"></span><span id="BUG_CHECK_SYMBOLIC_NAMES"></span>バグチェックのシンボル名

[**ドライバー\_POWER\_STATE\_FAILURE**](bug-check-0x9f--driver-power-state-failure.md)はバグチェックのシンボリック名であり、バグチェックコード9F が関連付けられています。 バグチェックのシンボル名に関連付けられている stop コードの16進値は、[バグチェックコードリファレンス](bug-check-code-reference2.md)に記載されています。

### <a name="span-idreading_bug_check_information_from_the_debuggerspanspan-idreading_bug_check_information_from_the_debuggerspanreading-bug-check-information-from-the-debugger"></a><span id="reading_bug_check_information_from_the_debugger"></span><span id="READING_BUG_CHECK_INFORMATION_FROM_THE_DEBUGGER"></span>デバッガーからバグチェック情報を読み取っています

デバッガーがアタッチされている場合は、バグチェックによって対象のコンピューターがデバッガーによって中断されます。 この場合、青い画面がすぐに表示されないことがあります。このクラッシュの詳細がデバッガーに送信され、デバッガーウィンドウに表示されます。 この情報をもう一度確認するには、 [ **. バグチェック (バグチェックデータの表示)** ](-bugcheck--display-bug-check-data-.md)コマンドまたは! [拡張機能の[**分析**](-analyze.md)] コマンドを使用します。

**カーネルデバッグとクラッシュダンプ分析**

カーネルデバッグは、他のトラブルシューティング手法が失敗した場合や、繰り返し発生する場合に特に役立ちます。 エラーメッセージのバグチェック情報セクションでは、正確なテキストを必ずキャプチャしてください。 複雑な問題を特定し、実行可能な回避策を作成するには、エラーにつながる正確なアクションを記録すると便利です。

[ **!analyze**](-analyze.md) デバッグ拡張機能は、バグ チェックに関する情報を表示し、根本原因の特定に役立ちます。

また、コード内でこの停止コードまでのブレークポイントを設定し、エラーが発生したコードへのシングルステップフォワードを試行することもできます。

詳細については、以下のトピックを参照してください。

[Windows デバッガー (WinDbg) を使用したクラッシュダンプ分析](crash-dump-files.md)

[WinDbg を使用したカーネルモードのダンプファイルの分析](analyzing-a-kernel-mode-dump-file-with-windbg.md)

[! Analyze 拡張機能](using-the--analyze-extension.md)と[! Analyze](-analyze.md)を使用する

Channel 9 でのデフラグツールの表示-<https://channel9.msdn.com/Shows/Defrag-Tools>

### <a name="span-idusing_driver_verifier_to_gather_informationspanspan-idusing_driver_verifier_to_gather_informationspanspan-idusing_driver_verifier_to_gather_informationspanusing-driver-verifier-to-gather-information"></a><span id="Using_Driver_Verifier_to_Gather_Information"></span><span id="using_driver_verifier_to_gather_information"></span><span id="USING_DRIVER_VERIFIER_TO_GATHER_INFORMATION"></span>ドライバーの検証機能を使用して情報を収集する

ブルースクリーンの約3分のうち、エラーが発生したドライバーが原因であると推定されます。 ドライバーの検証ツールは、リアルタイムで実行してドライバーの動作を調べるためのツールです。 たとえば、ドライバーの検証ツールでは、メモリ プールなどのメモリ リソースの使用がチェックされます。 ドライバーコードの実行中にエラーが発生した場合は、ドライバーコードのその部分をさらに詳しく調べることを許可する例外が事前に作成されています。 ドライバーの検証ツール マネージャーは、Windows に組み込まれており、すべての Windows PC で使用できます。 ドライバーの検証ツール マネージャーを起動するには、コマンド プロンプトで「*Verifier*」と入力します。 どのドライバーを検証するかを構成できます。 ドライバーを検証するコードが実行されるとオーバーヘッドが増えるので、可能な限り少ない数のドライバーで試してみてください。 詳細については、「[ドライバーの検証ツール](https://docs.microsoft.com/windows-hardware/drivers/devtest/driver-verifier)」を参照してください。

## <a name="span-idtips_for_software_engineersspanspan-idtips_for_software_engineersspanspan-idtips_for_software_engineersspantips-for-software-engineers"></a><span id="Tips_for_Software_Engineers"></span><span id="tips_for_software_engineers"></span><span id="TIPS_FOR_SOFTWARE_ENGINEERS"></span>ソフトウェアエンジニア向けのヒント


記述したコードの結果としてバグチェックが発生した場合は、カーネルデバッガーを使用して問題を分析し、コード内のバグを修正する必要があります。 詳細については、「[バグチェックコードリファレンス](bug-check-code-reference2.md)」セクションの個々のバグチェックコードを参照してください。

ただし、独自のコードが原因ではないバグチェックが発生する場合もあります。 この場合、問題の実際の原因を解決することはできません。そのため、問題を回避し、可能であれば、障害が発生しているハードウェアまたはソフトウェアコンポーネントを特定して削除することをお勧めします。

手順の確認、キーコンポーネントの再インストール、ファイルの日付の検証などの基本的なトラブルシューティング手順によって、多くの問題を解決できます。 また、イベントビューアー、Sysinternals 診断ツールおよびネットワーク監視ツールは、これらの問題を特定して解決することがあります。

Windows バグ チェック コードの一般的なトラブルシューティングについては、次の推奨事項に従ってください。

-   最近システムにハードウェアを追加した場合は、削除または交換してみてください。 または、利用可能なパッチがないか、製造元に確認します。

-   新しいデバイス ドライバーまたはシステム サービスが最近追加された場合は、それらを削除または更新してみてください。 新しいバグ チェック コードが表示される原因となったシステムの変更内容を確認します。

-   **デバイスマネージャー**を検索して、感嘆符 (!) でマークされているデバイスがあるかどうかを確認します。 [ドライバーのプロパティ] に表示されている、エラーが発生しているドライバーのイベントログを確認します。 関連するドライバーを更新してみてください。

-   イベント ビューアーを使用してシステム ログで追加のエラー メッセージを確認すると、エラーの原因になっているデバイスやドライバーを特定できる可能性があります。 詳しくは、[イベント ビューアーの使用](https://support.microsoft.com/hub/4338813/windows-help#1TC=windows-7)に関するページをご覧ください。 ブルー スクリーンと同じ時間帯に発生した重大なエラーをシステム ログで探します。

-   システムの製造元から提供されているハードウェア診断を実行できます。

-   Windows メモリ診断ツールを実行して、メモリをテストします。 コントロールパネルの検索ボックスに「Memory」と入力し、 **[コンピューターのメモリの問題を診断する]** をクリックします。テストの実行後、イベントビューアーを使用して、システムログの下に結果を表示します。 *MemoryDiagnostics-Results* エントリを探して、結果を表示します。

-   インストールされている新しいハードウェアに、インストールされている Windows のバージョンとの互換性があることを確認します。 たとえば、 [Windows 10 の仕様](https://www.microsoft.com/windows/windows-10-specifications)では、必要なハードウェアに関する情報を取得できます。

-   ウイルス検出プログラムを実行します。 ウイルスは、Windows 用にフォーマットされたすべての種類のハードディスクに感染し、ディスクの破損によってシステムのバグチェックコードが生成される可能性があります。 ウイルス検出プログラムがマスタブートレコードの感染を確認していることを確認します。

-   ディスクのスキャンユーティリティを使用して、ファイルシステムエラーがないことを確認します。 スキャンするドライブを右クリックし、 **[プロパティ]** を選択します。 **[ツール]** をクリックします。 **[今すぐチェック]** ボタンをクリックします。
-   システムファイルチェッカーツールを使用して、システムファイルが見つからないか破損しているかを修復します。 システムファイルチェッカーは、windows のユーティリティであり、ユーザーが Windows システムファイルの破損をスキャンし、破損したファイルを復元できるようにします。 次のコマンドを使用して、システムファイルチェッカーツール (SFC.EXE) を実行します。

    ```console
    SFC /scannow
    ```

    詳細については、「[システムファイルチェッカーツールを使用したシステムファイルの不足または破損の修復」を](https://support.microsoft.com/help/929833/use-the-system-file-checker-tool-to-repair-missing-or-corrupted-system)参照してください。

-   ハードドライブに十分な空き領域があることを確認します。 オペレーティングシステムとアプリケーションによっては、スワップファイルやその他の機能を作成するのに十分な空き領域が必要です。 システムの構成に基づいて、正確な要件は異なりますが、通常は 10% ~ 15% の空き領域を確保することをお勧めします。

-   システムに最新のサービスパックがインストールされていることを確認します。 システムにインストールされているサービスパックを検出するには、 **[スタート]** ボタンをクリックし、 **[実行]** をクリックして「 **winver**」と入力し、enter キーを押します。 [バージョン**情報**] ダイアログボックスには、サービスパックがインストールされている場合は、windows のバージョン番号とバージョン番号が表示されます。

-   製造元に確認して、更新されたシステム BIOS またはファームウェアが使用可能かどうかを確認してください。

-   キャッシュやシャドウ処理などの BIOS メモリオプションを無効にします。

-   Pc の場合は、すべての拡張ボードが適切に取り付けられ、すべてのケーブルが完全に接続されていることを確認します。

**セーフモードの使用**

コンポーネントを削除または無効にするときは、セーフモードの使用を検討してください。 セーフモードを使用すると、Windows の起動時に最小限必要なドライバーとシステムサービスのみが読み込まれます。 セーフモードに移行するには、設定 で **更新とセキュリティ** を使用します。 **回復**- を選択して、メンテナンスモードで起動する &gt;**詳細なスタートアップ** を選択します。 生成されたメニューで **トラブルシューティング** を選択し、-&gt;**詳細オプション** -&gt;**スタートアップ設定** -&gt;**再起動** を選択します。 Windows が**起動設定**画面に再起動したら、オプション、4、5、または6を選択してセーフモードで起動します。

セーフモードは、起動時にファンクションキーを押すと (例 F8)、使用できる場合があります。 特定のスタートアップオプションについては、製造元の情報を参照してください。

## <a name="span-idforced_kebugcheckspanspan-idforced_kebugcheckspanspan-idforced_kebugcheckspanforced-kebugcheck"></a><span id="Forced_KeBugCheck"></span><span id="forced_kebugcheck"></span><span id="FORCED_KEBUGCHECK"></span>強制 KeBugCheck チェック


カーネルモードドライバーから意図的にバグチェックを行うには、バグチェックのシンボリック名を**Kebugcheck**チェック関数または**Kebugcheck checkex**関数に渡す必要があります。 これは、他のオプションが使用できない場合にのみ実行してください。 これらの関数の詳細については、「Windows Driver Kit」を参照してください。

 

 






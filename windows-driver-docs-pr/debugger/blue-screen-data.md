---
title: ブルー スクリーン データ
description: Microsoft Windows には、その妥協安全なシステム操作の条件が検出されると、システムを停止します。 この条件は、バグと呼ばれるまたは stop エラーを確認してください。
ms.assetid: 8cc42643-e231-49dd-96b0-6cb528d5d7a9
keywords:
- ブルー スクリーン データの Windows デバッグ
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- Blue Screen Data
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: a018491fc0491ba2d084a45baa9c523ca4bdc2ba
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56552578"
---
# <a name="blue-screen-data"></a>ブルー スクリーン データ


**注**  プログラマ向けのトピックです。 コンピューターを使用しているときに、エラー コードがブルー スクリーンが受信した顧客の場合を参照してください。[トラブルシューティング ブルー スクリーン エラー](https://go.microsoft.com/fwlink/p/?linkid=183646)します。

 

**注**   IT プロフェッショナルやサポート エージェントの場合は、追加の情報は、この記事を参照してください。 [Microsoft サポートに連絡する前に、"ブルー スクリーン"または Stop エラーの問題のトラブルシューティング](https://support.microsoft.com/help/3106831/troubleshoot-blue-screen-or-stop-error-problems-before-you-contact-microsoft-support)します。

 

Microsoft Windows には、その妥協安全なシステム操作の条件が検出されると、システムを停止します。 この条件と呼ばれる、*バグ チェック*します。 としても一般的に指す、*システム クラッシュ*、*カーネル エラー*、または*停止エラー*します。

OS のオペレーティング システムの整合性が損なわれた後に実行する継続が許可された場合、データの破損でした。 システムのセキュリティを損なうか。

システムのクラッシュ ダンプが有効な場合は、クラッシュ ダンプ ファイルが作成されます。

カーネル デバッガーがアタッチされ、アクティブな場合は、システムは、クラッシュを調査するデバッガーを使用できるように、中断をされます。

デバッガーがアタッチされていない場合、エラーに関する情報を青色のテキスト画面が表示されます。 この画面と呼ばれる、*ブルー スクリーン*、*バグ チェック画面*、または*停止画面*します。

Windows insider ビルドを使用している場合は、緑の背景にテキストが表示されます。

ブルー スクリーンの正確な外観は、エラーの原因によって異なります。

考えられるブルー スクリーンが 1 つの例を次に示します。

![バグ チェックの例の windows 10 ブルー スクリーンに qr コード](images/bug-check-example-blue-screen-page-fault.png)

停止コードの表示など[**ページ\_フォールト\_IN\_非ページ\_領域**](bug-check-0x50--page-fault-in-nonpaged-area.md)します。 使用可能なとき、実行されていたコードのモジュール名も表示されます、AcmeVideo.sys など。

場合、[カーネル モードのダンプ ファイル](kernel-mode-dump-files.md)書き込まれた、示されるも割合の完全なカウント ダウンのダンプが書き込まれるとします。

16 進値に関連付けられている各停止コードに記載されている終了コードが[バグ チェック コード参照](bug-check-code-reference2.md)します。

## <span id="ddk_blue_screen_data_dbg"></span><span id="DDK_BLUE_SCREEN_DATA_DBG"></span>


### <a name="span-idgatheringthestopcodeparametersspanspan-idgatheringthestopcodeparametersspanspan-idgatheringthestopcodeparametersspangathering-the-stop-code-parameters"></a><span id="Gathering_the_Stop_Code_Parameters"></span><span id="gathering_the_stop_code_parameters"></span><span id="GATHERING_THE_STOP_CODE_PARAMETERS"></span>停止コード パラメーターの収集

各バグ チェックのコードでは、追加の情報を提供する 4 つの関連するパラメーターを持っています。 パラメーターが記載されて[バグ チェック コード参照](bug-check-code-reference2.md)停止コードごとにします。

4 つの停止コード パラメーターを収集するために複数の方法はあります。

-   イベント ビューアーの Windows システム ログを調べます。 バグチェックのイベント プロパティは、4 つの停止コード パラメーターを一覧表示されます。 詳細については、[イベント ビューアーを開く](https://windows.microsoft.com/windows/what-information-event-logs-event-viewer#1TC=windows-7)を参照してください。

-   生成されたダンプ ファイルをロードして、 [ **! 分析**](-analyze.md)コマンドと、デバッガーをアタッチします。 詳細については、[WinDbg にカーネル モードのダンプ ファイルの分析](analyzing-a-kernel-mode-dump-file-with-windbg.md)を参照してください。

-   エラー状態の PC にカーネル デバッガーをアタッチします。 停止コードが発生したときにデバッガーの出力は停止コードの 16 進値の後に 4 つのパラメーターが含まれます。

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

### <a name="span-idbugchecksymbolicnamesspanspan-idbugchecksymbolicnamesspanbug-check-symbolic-names"></a><span id="bug_check_symbolic_names"></span><span id="BUG_CHECK_SYMBOLIC_NAMES"></span>バグ チェックのシンボル名

[**ドライバー\_POWER\_状態\_エラー** ](bug-check-0x9f--driver-power-state-failure.md)バグ チェック シンボリック名、関連付けられているバグ チェック 9F のコードでは、します。 バグ チェックのシンボリック名に関連付けられた 16 進数の値が記載されて停止コード、[バグ チェック コード参照](bug-check-code-reference2.md)します。

### <a name="span-idreadingbugcheckinformationfromthedebuggerspanspan-idreadingbugcheckinformationfromthedebuggerspanreading-bug-check-information-from-the-debugger"></a><span id="reading_bug_check_information_from_the_debugger"></span><span id="READING_BUG_CHECK_INFORMATION_FROM_THE_DEBUGGER"></span>デバッガーからのバグ チェック情報の読み取り

デバッガーがアタッチされているバグ チェックが、デバッガーを中断する対象のコンピュータに発生します。 この場合は、ブルー スクリーンが、すぐに表示されない場合がありますこのクラッシュの完全な詳細情報は、デバッガーに送信され、デバッガー ウィンドウに表示されます。 この情報を 2 回目を表示する、 [ **.bugcheck (表示バグ データを確認する)** ](-bugcheck--display-bug-check-data-.md)コマンドまたは[ **! 分析**](-analyze.md)拡張コマンド.

**カーネル デバッグとクラッシュ ダンプ分析**

カーネル デバッグは、その他のトラブルシューティングの手法が失敗したときに特に便利です、または定期的な問題です。 エラー メッセージのバグ チェック情報のセクションでは正確なテキストをキャプチャしてください。 複雑な問題を特定し、実行可能な回避策を開発、エラーが発生する正確なアクションを記録すると便利です。

[ **! 分析**](-analyze.md)バグ チェックに関する情報を表示拡張機能をデバッグおよび根本原因を突き止めるには非常に役に立ちます。

また、この停止コードに至るまで、コードにブレークポイントを設定、エラーが発生したコードをシングル ステップ転送しようし、することができますも。

詳細については、以下のトピックを参照してください。

[クラッシュ ダンプ分析の Windows デバッガー (WinDbg) の使用方法](crash-dump-files.md)

[WinDbg をカーネル モードのダンプ ファイルの分析](analyzing-a-kernel-mode-dump-file-with-windbg.md)

[使用して、! 拡張機能を分析](using-the--analyze-extension.md)と[! 分析](-analyze.md)

Channel 9 のデフラグ ツールを表示します。 <https://channel9.msdn.com/Shows/Defrag-Tools>

### <a name="span-idusingdriververifiertogatherinformationspanspan-idusingdriververifiertogatherinformationspanspan-idusingdriververifiertogatherinformationspanusing-driver-verifier-to-gather-information"></a><span id="Using_Driver_Verifier_to_Gather_Information"></span><span id="using_driver_verifier_to_gather_information"></span><span id="USING_DRIVER_VERIFIER_TO_GATHER_INFORMATION"></span>Driver Verifier を使用して情報を収集するには

ブルー スクリーンの約 3 四半期が原因であるドライバーのエラーと推定されます。 Driver Verifier は、ドライバーの動作を確認するのにはリアルタイムで実行されているツールです。 たとえば、Driver Verifier は、メモリ プールなどのメモリ リソースの使用を確認します。 ドライバー コードの実行でエラーが参照してください、さらに細かく検証するドライバー コードの部分を許可する例外が事前に作成されます。 ドライバー検証マネージャーは、Windows に組み込まれているしはすべての Windows Pc で使用できます。 ドライバー検証マネージャーを起動する入力*Verifier*コマンド プロンプトでします。 確認するにはどのドライバーを構成することができます。 ドライバーを検証するコードは実行時にオーバーヘッドを追加、のでお試しくださいし、可能なドライバーの最小数を確認します。 詳細については、[Driver Verifier](https://msdn.microsoft.com/library/windows/hardware/ff545448)を参照してください。

## <a name="span-idtipsforsoftwareengineersspanspan-idtipsforsoftwareengineersspanspan-idtipsforsoftwareengineersspantips-for-software-engineers"></a><span id="Tips_for_Software_Engineers"></span><span id="tips_for_software_engineers"></span><span id="TIPS_FOR_SOFTWARE_ENGINEERS"></span>ソフトウェア エンジニア向けのヒント


バグ チェックが記述したコードの結果として発生したときに、カーネル デバッガーを使用して、問題を分析して、コードでバグを修正する必要があります。 完全な詳細については、コードをチェックインする個々 のバグを参照してください、[バグ チェック コード参照](bug-check-code-reference2.md)セクション。

ただし、独自のコードの原因ではないバグ チェックを生じる可能性があります。 この場合、する可能性がありますされません目標は、問題を回避し、可能であれば分離し、問題なのでは、ハードウェアまたはソフトウェア コンポーネントを削除するために、問題の実際の原因を解決できません。

多くの問題は、手順を確認する、主要なコンポーネントを再インストール ファイルの日付を確認するなどの基本的なトラブルシューティング手順で解決できます。 また、イベント ビューアー、Sysinternals の診断ツール、およびネットワーク監視ツールがありますの分離し、解決これらの問題。

Windows のバグの一般的なトラブルシューティングのコードを確認、これらの推奨事項に従ってください。

-   最近削除または置換することをお試し、システムにハードウェアを追加した場合 または、更新プログラムが利用可能な製造元に確認します。

-   新しいデバイス ドライバまたはシステム サービスを最近では、追加されている場合を削除するか、それらを更新してみてください。 表示する新しいチェック コードをバグの原因となったシステムで変更内容を調べてください。

-   検索対象**デバイス マネージャー**を任意のデバイスの感嘆符 (!) が付いてを参照してください。 任意のエラーが発生したドライバーのドライバーのプロパティに表示されるイベント ログを確認します。 関連するドライバーを更新してみてください。

-   デバイスまたはエラーの原因となっているドライバーの特定に役立つ可能性がある追加のエラー メッセージをイベント ビューアーのシステム ログを確認します。 詳細については、[イベント ビューアーを開く](https://windows.microsoft.com/windows/what-information-event-logs-event-viewer#1TC=windows-7)を参照してください。 ブルー スクリーンに同じ期間に発生したシステム ログの重大なエラーを探します。

-   システム製造元から提供されたハードウェア診断を実行して確認することができます。

-   メモリをテストする、Windows メモリ診断ツールを実行します。 コントロール パネルの検索ボックスには、メモリを入力し、クリックして **、コンピューターのメモリの問題を診断**します。テストの実行後は、イベント ビューアーを使用して、システム ログで結果を表示します。 探して、 *MemoryDiagnostics 結果*結果を表示するエントリ。

-   インストールされている新しいハードウェアが Windows のインストールされているバージョンと互換性があることを確認します。 たとえばに必要なハードウェアに関する情報を取得できます[Windows 10 の仕様](https://www.microsoft.com/windows/windows-10-specifications)します。

-   ウイルス検出プログラムを実行します。 ウイルスに感染する可能性、Windows 用にフォーマットされたハード_ディスクのすべての種類と、結果として得られるディスクの破損は、システムのバグ チェックのコードを生成できます。 ウイルス検出プログラムへの感染マスター ブート レコードのチェックを確認します。

-   ないファイル システムのエラーを確認するのにには、スキャンのディスク ユーティリティを使用します。 スキャンを選択するドライブを右クリックして**プロパティ**します。 をクリックして**ツール**します。 をクリックして、**今すぐチェック**ボタンをクリックします。
-   システム ファイル チェッカー ツールを使用して、欠落または破損システム ファイルを修復します。 システム ファイル チェッカーは、ユーティリティは Windows ユーザーを Windows システム ファイルで破損をスキャンし、復元できるようにするには、ファイルが破損しています。 システム ファイル チェッカー (SFC.exe) ツールを実行するのにには、次のコマンドを使用します。

    ```console
    SFC /scannow
    ```

    詳細については、[システム ファイル チェッカー ツールを使用してシステム ファイルの欠落または破損の修復](https://support.microsoft.com/kb/929833)を参照してください。

-   ハード ドライブに十分な空き領域があることを確認します。 オペレーティング システムと一部のアプリケーションは、スワップ ファイルを作成する十分な空き領域を必要とし、他の機能です。 システム構成に基づきと、正確な要件は異なりますが、通常は 10 ~ 15% 空き領域があることをお勧めします。

-   システムにインストールされている最新の Service Pack があることを確認します。 どのサービス パックを検出する場合は、いずれかがシステムにインストールされている、 をクリックして**開始**、 をクリックして**実行**、型**winver**、し、ENTER キーを押します。 **について Windows**いずれかがインストールされている場合、Windows のバージョン番号と、サービス パックのバージョン番号をダイアログ ボックスが表示されます。

-   製造元に問い合わせて、更新されたシステムの BIOS またはファームウェアが使用できるかどうかを確認します。

-   キャッシュやシャドウ処理などの BIOS メモリオプションを無効にします。

-   Pc で行うすべての拡張ボードであることを確認して、正しく取り付けられているし、すべてのケーブルが完全に接続されています。

**セーフ モードを使用します。**

削除するか、コンポーネントを無効にするときに、セーフ モードを使用してください。 セーフ モードを使用して、Windows の起動中に、最低限必要なドライバーとシステム サービスのみを読み込みます。 セーフ モードを入力するを使用して**更新とセキュリティ**で設定します。 選択**Recovery**-&gt;**スタートアップを高度な**メンテナンス モードで起動します。 結果として得られるメニューでは、次のように選択します**トラブルシューティング**- &gt; **オプションの高度な** - &gt; **スタートアップ設定**。 - &gt; **再起動**します。 Windows を再起動した後、**スタートアップ設定**画面で、セーフ モードで起動するには、4、5 または 6 のオプションを選択します。

ブート、f8 キーなどのファンクション キーを押して、セーフ モードを利用できます。 特定のスタートアップ オプションの製造元から情報を参照してください。

## <a name="span-idforcedkebugcheckspanspan-idforcedkebugcheckspanspan-idforcedkebugcheckspanforced-kebugcheck"></a><span id="Forced_KeBugCheck"></span><span id="forced_kebugcheck"></span><span id="FORCED_KEBUGCHECK"></span>強制 KeBugCheck


カーネル モード ドライバーのバグ チェックが発生する意図的に、するにはバグ チェックのシンボリック名を渡す必要があります、 **KeBugCheck**または**KeBugCheckEx**関数。 これは、その他のオプションが使用可能な状況でのみ実行する必要があります。 これらの関数の詳細については、Windows ドライバー キットを参照してください。

 

 






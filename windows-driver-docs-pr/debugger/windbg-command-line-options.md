---
title: WinDbg のコマンドライン オプション
description: WinDbg の初回使用時のユーザーは、デバッグを使用して WinDbg セクションで始める必要があります。
ms.assetid: bd169c73-0a46-41b5-bd7b-71adf7747069
keywords:
- WinDbg コマンド ライン オプションの Windows デバッグ
ms.date: 08/10/2018
ms.topic: article
ms.prod: windows-hardware
ms.technology: windows-devices
topic_type:
- apiref
api_name:
- WinDbg Command-Line Options
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 19eed1e5fb64ace386790a202ac1542bb231750d
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63325839"
---
# <a name="windbg-command-line-options"></a>WinDbg のコマンドライン オプション


WinDbg の初回使用時のユーザーで始まり、[デバッグを使用して WinDbg](debugging-using-windbg.md)セクション。

WinDbg のコマンドラインは、次の構文を使用します。

```dbgsyntax
windbg [ -server ServerTransport | -remote ClientTransport ] [-lsrcpath ]
   [ -premote SmartClientTransport ] [-?] [-ee {masm|c++}] 
   [-clines lines] [-b] [-d] [-aExtension]  
   [-failinc] [-g] [-G] [-hd] [-j] [-n] [-noshell] [-o] [-openPrivateDumpByHandle Handle]
   [-Q | -QY] [-QS | -QSY] [-robp] [-secure] [-ses] [-sdce] 
   [-sicv] [-sins] [-snc] [-snul] [-sup] [-sflags 0xNumber] 
   [-T Title] [-v] [-log{o|a} LogFile] [-noinh] 
   [-i ImagePath] [-y SymbolPath] [-srcpath SourcePath] 
   [-k [ConnectType] | -kl | -kx ExdiOptions] [-c "command"] 
   [-pb] [-pd] [-pe] [-pr] [-pt Seconds] [-pv]
   [-W Workspace] [-WF Filename] [-WX] [-zp PageFile] 
   [ -p PID | -pn Name | -psn ServiceName | -z DumpFile | executable ] 

windbg -I[S] 

windbg -IU KeyString

windbg -IA[S] 
```

WinDbg コマンド ライン オプションの説明に従ってください。 すべてのコマンド ライン オプションを除く大文字 **-j**します。 最初のハイフンは、フォワード スラッシュ (/) に置き換えることができます。

場合、 **-リモート**または **-サーバー**オプションを使用すると、コマンドラインでその他のオプションの前にする必要があります。 場合、*実行可能ファイル*を指定すると、最後に、コマンドラインに表示する必要がありますの後の任意のテキスト、*実行可能ファイル*名前は、実行可能プログラムに独自のコマンド ライン パラメーターとして渡されます。

## <a name="span-idddkwindbgcommandlineoptionsdbgspanspan-idddkwindbgcommandlineoptionsdbgspanparameters"></a><span id="ddk_windbg_command_line_options_dbg"></span><span id="DDK_WINDBG_COMMAND_LINE_OPTIONS_DBG"></span>パラメーター


<span id="_______-server_______ServerTransport______"></span><span id="_______-server_______servertransport______"></span><span id="_______-SERVER_______SERVERTRANSPORT______"></span> **-server** *ServerTransport*   
その他のデバッガーによってアクセスできるデバッグ サーバーを作成します。 については、使用可能な*サーバトランスポート*値を参照してください[**デバッグ サーバー アクティブ化する**](activating-a-debugging-server.md)します。 このパラメーターを使用すると、コマンドラインで最初のパラメーターがあります。

<span id="_______-remote_______ClientTransport______"></span><span id="_______-remote_______clienttransport______"></span><span id="_______-REMOTE_______CLIENTTRANSPORT______"></span> **-remote** *ClientTransport*   
デバッグ クライアントを作成し、既に実行されているデバッグ サーバーに接続します。 については、使用可能な*ClientTransport*値を参照してください[**デバッグ クライアントをアクティブ化する**](activating-a-debugging-client.md)します。 このパラメーターを使用すると、コマンドラインで最初のパラメーターがあります。

<span id="_______-premote_______SmartClientTransport______"></span><span id="_______-premote_______smartclienttransport______"></span><span id="_______-PREMOTE_______SMARTCLIENTTRANSPORT______"></span> **-premote** *SmartClientTransport*   
スマート クライアントを作成しが既に実行されているプロセス サーバーに接続します。 については、使用可能な*SmartClientTransport*値を参照してください[**スマート クライアントのアクティブ化**](activating-a-smart-client.md)します。

<span id="_______-a________Extension______"></span><span id="_______-a________extension______"></span><span id="_______-A________EXTENSION______"></span> **-** *拡張機能*   
既定の拡張 DLL を設定します。 既定値は kdextx86.dll kdexts.dll します。 後にスペースが必要ない、"a"の .dll ファイル名拡張子を含めることはできません。 詳細、およびこの既定の設定の他のメソッドでは、次を参照してください。[デバッガー拡張 Dll の読み込み](loading-debugger-extension-dlls.md)します。

<span id="_______-b______"></span><span id="_______-B______"></span> **-b**   
このオプションはサポートされなくなりました。

<span id="_______-c_________command______________"></span><span id="_______-C_________COMMAND______________"></span> **-c "** *command* **"**   
起動時に実行する初期のデバッガー コマンドを指定します。 このコマンドは、引用符で囲む必要があります。 複数のコマンドは、セミコロンで区切ることができます。 (長いコマンド リストがあれば、スクリプト内に配置し、使用する方が簡単なる、 **-c**オプションは、 [  **$ &lt;、$&gt;&lt;、$&gt; &lt;、$$&gt; &lt; (スクリプト ファイルを実行)** ](-----------------------a---run-script-file-.md)コマンド)。

デバッグ クライアントを開始すると、このコマンドは必要があります、デバッグ サーバー向けです。 などの特定のクライアントのコマンド **.lsrcpath**、許可されていません。

<span id="_______-clines________lines______"></span><span id="_______-CLINES________LINES______"></span> **-clines** *行*   
リモート デバッグ中にアクセスできるコマンドの履歴には、コマンドのおおよその数を設定します。 詳細については、およびこの数を変更するには、他の方法については、「[デバッガー コマンドを使用して](using-debugger-commands.md)します。

<span id="_______-d______"></span><span id="_______-D______"></span> **-d**   
(カーネル モードのみ)再起動後、デバッガーは、カーネル モジュールが読み込まれるとすぐに目的のコンピュータに中断されます。 (この区切りが以前からの離別、 **-b**オプション)。参照してください[クラッシュし、ターゲット コンピューターを再起動](crashing-and-rebooting-the-target-computer.md)とこの状態を変更するには、他の方法の詳細についてはします。

<span id="_______-ee__masm_c___"></span><span id="_______-EE__MASM_C___"></span> **-ee** {**masm**|**c++**}  
既定の式エバリュエーターを設定します。 場合**masm**指定すると、MASM 式の構文が使用されます。 場合**c++** 指定すると、C++ 式の構文が使用されます。 場合、 **ee**オプションを省略すると、MASM 式の構文は、既定値として使用されます。 参照してください[を評価する式](evaluating-expressions.md)詳細についてはします。

<span id="_______-failinc______"></span><span id="_______-FAILINC______"></span> **-failinc**   
原因の問題のあるシンボルを無視するデバッガー。 ユーザー モードまたはカーネル モードのミニダンプ ファイルをデバッグするには、このオプションは、デバッガーをイメージをマップすることはできませんのすべてのモジュールを読み込むようにも。 詳細については、およびこれを制御するための他の方法については、「 [SYMOPT\_EXACT\_シンボル](symbol-options.md#symopt-exact-symbols)します。

<span id="_______-g______"></span><span id="_______-G______"></span> **-g**   
(ユーザー モードのみ)ターゲット アプリケーションでは、最初のブレークポイントを無視します。 このオプションは、ターゲット アプリケーションが開始されているか、WinDbg が接続すると後の別のブレークポイントが設定されている場合を除き、実行を続行します。 参照してください[最初のブレークポイント](initial-breakpoint.md)詳細についてはします。

<span id="_______-G______"></span><span id="_______-g______"></span> **-G**   
(ユーザー モードのみ)プロセスの終了時の最終的なブレークポイントを無視します。 通常、イメージ run-down プロセス中に、デバッグ セッションを終了します。 このオプションにより、デバッグ セッションを子プロセスの終了時にすぐに終了されます。 これは、コマンドを入力すると同じ効果**sxd epr**します。 詳細については、次を参照してください。[を制御する例外とイベント](controlling-exceptions-and-events.md)します。

<span id="_______-hd______"></span><span id="_______-HD______"></span> **-hd**   
(ユーザー モードのみ)デバッグ ヒープを使用しないことを指定します。

<span id="_______-I_S_"></span><span id="_______-i_s_"></span> **-I**\[**S**\]  
事後分析のデバッガーと WinDbg をインストールします。 詳細については、次を参照してください。[事後のデバッグを有効にする](enabling-postmortem-debugging.md)します。

この操作を試行すると、成功または失敗のメッセージが表示されます。 場合**S**が含まれている場合、この作業が完了したら自動的に成功した場合は、唯一のエラー メッセージが表示されます。

**-は**パラメーターは、その他のパラメーターを使用する必要があります。 このコマンドは実際に開始されません WinDbg を少し見えますが、WinDbg ウィンドウ。

<span id="_______-IA_S_"></span><span id="_______-ia_s_"></span> **-IA**\[**S**\]  
ファイル拡張子 .dmp、.mdmp、およびレジストリの .wew WinDbg に関連付けます。 この操作を試行すると、成功または失敗のメッセージが表示されます。 場合**S**が含まれている場合、この作業が完了したら自動的に成功した場合は、唯一のエラー メッセージが表示されます。 この関連付けが行われた後、これらの拡張機能のいずれかのファイルをダブルクリックすると、WinDbg が開始されます。

**-IA**パラメーターは、その他のパラメーターを使用する必要があります。 このコマンドは実際に開始されません WinDbg を少し見えますが、WinDbg ウィンドウ。

<span id="_______-IU________KeyString______"></span><span id="_______-iu________keystring______"></span><span id="_______-IU________KEYSTRING______"></span> **-IU** *KeyString*   
ユーザーは自動起動 url のデバッガーのリモート クライアントするためには、デバッガーのリモート処理、URL の種類として登録します。 *KeyString*形式`remdbgeng://RemotingOption`します。 *RemotingOption*トピックで定義されているトランスポート プロトコルを定義する文字列は、 [**デバッグ クライアントをアクティブ化する**](activating-a-debugging-client.md)します。 この操作が成功すると、メッセージは表示されません。失敗した場合、エラー メッセージが表示されます。

**-IU**パラメーターは、その他のパラメーターを使用する必要があります。 少し WinDbg ウィンドウが表示されますが、このコマンドの WinDbg は実際に開始されません。

<span id="_______-i_______ImagePath______"></span><span id="_______-i_______imagepath______"></span><span id="_______-I_______IMAGEPATH______"></span> **-i** *ImagePath*   
違反を生成した実行可能ファイルの場所を指定します。 パスにスペースが含まれている場合は、引用符で囲む必要があります。

<span id="_______-j______"></span><span id="_______-J______"></span> **-j**   
ジャーナリングを使用できます。

<span id="_______-k__ConnectType_"></span><span id="_______-k__connecttype_"></span><span id="_______-K__CONNECTTYPE_"></span> **-k** \[*ConnectType*\]  
(カーネル モードのみ)カーネル デバッグ セッションを開始します。 詳細については、次を参照してください。 [Live カーネル モードのデバッグを使用して WinDbg](performing-kernel-mode-debugging-using-windbg.md)します。 場合 **-k**せず使用*ConnectType*オプションの後に、コマンドラインで最終的なエントリがあります。

<span id="_______-kl______"></span><span id="_______-KL______"></span> **-kl**   
(カーネル モードのみ)カーネル デバッガーと同じコンピューター上のセッションのデバッグを開始します。

<span id="_______-kx_______ExdiOptions______"></span><span id="_______-kx_______exdioptions______"></span><span id="_______-KX_______EXDIOPTIONS______"></span> **-kx** *ExdiOptions*   
(カーネル モードのみ)カーネル デバッグ EXDI ドライバーを使用してセッションを開始します。 EXDI ドライバーは、このドキュメントでは説明しません。 場合は、ハードウェアのプローブやハードウェア シミュレーターに EXDI インターフェイスがある場合は、デバッグ情報を Microsoft に問い合わせてください。

<span id="_______-log_o_a__LogFile"></span><span id="_______-log_o_a__logfile"></span><span id="_______-LOG_O_A__LOGFILE"></span> **-log**{**o**|**a**} *LogFile*  
ログ ファイルにログ情報を開始します。 指定されたログ ファイルが既に存在する場合は上書きされる場合 **-ロゴ**使用されます。 場合**loga**が使用すると、出力はファイルに追加する、します。 詳細については、次を参照してください。 [WinDbg にログ ファイルを保持](keeping-a-log-file-in-windbg.md)します。

<span id="_______-lsrcpath______"></span><span id="_______-LSRCPATH______"></span> **-lsrcpath**   
リモート クライアントのローカル ソース パスを設定します。 このオプションが従う必要があります **-リモート**コマンド行にします。

<span id="_______-n______"></span><span id="_______-N______"></span> **-n**   
*ノイズの多いシンボルの読み込み*:シンボル ハンドラーから詳細な出力を有効にします。 詳細については、およびこれを制御するための他の方法については、「 [SYMOPT\_デバッグ](symbol-options.md#symopt-debug)します。

<span id="_______-noinh______"></span><span id="_______-NOINH______"></span> **-noinh**   
(ユーザー モードのみ)デバッガーからハンドルを継承することから、デバッガーによって作成されたプロセスをできないようにします。 これを制御するための他の方法では、次を参照してください。[デバッグ ユーザー モード プロセスを使用して WinDbg](debugging-a-user-mode-process-using-windbg.md)します。

<span id="_______-noprio______"></span><span id="_______-NOPRIO______"></span> **-noprio**   
任意の優先度の変更できないようにします。 このパラメーターは、アクティブなときに CPU 時間を優先度を取得を WinDbg をできなくなります。

<span id="_______-noshell______"></span><span id="_______-NOSHELL______"></span> **-noshell**   
すべてを禁止 **.shell**コマンド。 この禁止は、新しいデバッグ セッションが開始された場合でも、デバッガーが実行されている限り最後されます。 詳細については、および他のシェル コマンドを無効にする方法については、「[シェル コマンドを使用して](using-shell-commands.md)します。

<span id="_______-o______"></span><span id="_______-O______"></span> **-o**   
(ユーザー モードのみ)ターゲット アプリケーション (子プロセス) で起動されたすべてのプロセスをデバッグします。 既定では、作成したプロセスをデバッグする 1 つでは、通常どおり、実行されます。

<span id="_______-openPrivateDumpByHandle______"></span><span id="_______-OPENPRIVATEDUMPBYHANDLE______"></span> **-openPrivateDumpByHandle** *Handle*   
デバッグするクラッシュ ダンプ ファイルのハンドルを指定します。

<span id="_______-p_______PID______"></span><span id="_______-p_______pid______"></span><span id="_______-P_______PID______"></span> **-p** *PID*   
デバッグする 10 進数のプロセス ID を指定します。 これは、既に実行されているプロセスのデバッグに使用されます。

<span id="_______-pb______"></span><span id="_______-PB______"></span> **-pb**   
(ユーザー モードのみ)デバッガーがターゲット プロセスにアタッチするときに、初期の侵入を要求するを防ぎます。 アプリケーションが既に中断されている場合、またはターゲットで侵入スレッドを作成しないようにする場合は便利にできます。

<span id="_______-pd______"></span><span id="_______-PD______"></span> **-pd**   
(ユーザー モードのみ)により、ターゲット アプリケーションは、デバッグ セッションの終了時に終了するのにはしません。 参照してください[WinDbg でデバッグ セッションを終了する](ending-a-debugging-session-in-windbg.md)詳細についてはします。

<span id="_______-pe______"></span><span id="_______-PE______"></span> **-pe**   
(ユーザー モードのみ)対象アプリケーションは既にデバッグされていることを示します。 参照してください[対象アプリケーションを再アタッチ](reattaching-to-the-target-application.md)詳細についてはします。

<span id="_______-pn_______Name______"></span><span id="_______-pn_______name______"></span><span id="_______-PN_______NAME______"></span> **-pn** *名*   
デバッグするプロセスの名前を指定します。 (この名前必要がありますで一意である。)これは、既に実行されているプロセスのデバッグに使用されます。

<span id="_______-pr______"></span><span id="_______-PR______"></span> **-pr**   
(ユーザー モードのみ)原因、デバッガーをアタッチするときに実行されているターゲット プロセスを開始します。 これは、アプリケーションが既に中断されているし、実行を再開することを希望する場合に役立ちます。

<span id="_______-psn_______ServiceName______"></span><span id="_______-psn_______servicename______"></span><span id="_______-PSN_______SERVICENAME______"></span> **-psn** *ServiceName*   
デバッグするプロセスに含まれているサービスの名前を指定します。 これは、既に実行されているプロセスのデバッグに使用されます。

<span id="_______-pt_______Seconds______"></span><span id="_______-pt_______seconds______"></span><span id="_______-PT_______SECONDS______"></span> **pt -** *秒*   
区切りのタイムアウトを秒単位で指定します。 既定値は 30 です。 参照してください[ターゲットを制御する](controlling-the-target.md)詳細についてはします。

<span id="_______-pv______"></span><span id="_______-PV______"></span> **-pv**   
(ユーザー モードのみ)デバッガーがターゲット プロセスに noninvasively アタッチする必要がありますを指定します。 詳細については、次を参照してください。[待合室 (ユーザー モード) のデバッグ](noninvasive-debugging--user-mode-.md)します。

<span id="_______-Q______"></span><span id="_______-q______"></span> **-Q**   
「ワークスペースを保存しますか?」を抑制します。  ダイアログ ボックスでオプションを指定するときは、表を参考にしてください。 ワークスペースは、自動的に保存されません。 参照してください[を使用してワークスペース](using-workspaces.md)詳細についてはします。

<span id="_______-QS______"></span><span id="_______-qs______"></span> **-QS**   
「ソースの再読み込みしますか?」を抑制します。  ダイアログ ボックスでオプションを指定するときは、表を参考にしてください。 ソース ファイルは自動的に再読み込みされません。

<span id="_______-QSY______"></span><span id="_______-qsy______"></span> **-QSY**   
「ソースの再読み込みしますか?」を抑制します。 ダイアログ ボックスと自動的に再読み込みをソース ファイルです。

<span id="_______-QY______"></span><span id="_______-qy______"></span> **-QY**   
「ワークスペースを保存しますか?」を抑制します。 ダイアログ ボックス、自動的にワークスペースを保存します。 参照してください[を使用してワークスペース](using-workspaces.md)詳細についてはします。

<span id="_______-robp______"></span><span id="_______-ROBP______"></span> **-robp**   
これにより、CDB を読み取り専用メモリ ページにブレークポイントを設定できます。 (既定値は、このような操作が失敗するは) です。

<span id="_______-sdce______"></span><span id="_______-SDCE______"></span> **-sdce**   
デバッガー表示が**ファイル アクセス エラー**シンボルの読み込み中のメッセージ。 詳細については、およびこれを制御するための他の方法については、「 [SYMOPT\_失敗\_重大\_エラー](symbol-options.md#symopt-fail-critical-errors)します。

<span id="_______-secure______"></span><span id="_______-SECURE______"></span> **-secure**   
アクティブに[保護モード](secure-mode.md)します。

<span id="_______-ses______"></span><span id="_______-SES______"></span> **-ses**   
原因のデバッガーがすべてのシンボル ファイルの厳密な評価を実行し、問題のある任意の記号を無視します。 詳細については、およびこれを制御するための他の方法については、「 [SYMOPT\_EXACT\_シンボル](symbol-options.md#symopt-exact-symbols)します。

<span id="_______-sflags_0x________Number______"></span><span id="_______-sflags_0x________number______"></span><span id="_______-SFLAGS_0X________NUMBER______"></span> **sflags 0 x** *数*   
一度にすべてのシンボルのハンドラーのオプションを設定します。 *数*付ける必要があります、16 進数**0 x** --、なし 10 進数、 **0 x**は許可されてが、シンボルのオプションはバイナリのフラグ、したがって、16 進数はお勧めします。 このオプションは、すべてのシンボルのハンドラーの既定値は上書きされますので注意して使用する必要があります。 詳細については、次を参照してください。[シンボル オプションを設定](symbol-options.md)します。

<span id="_______-sicv______"></span><span id="_______-SICV______"></span> **-sicv**   
CV レコードを無視するシンボルのハンドラーをによりします。 詳細については、およびこれを制御するための他の方法については、「 [SYMOPT\_無視\_CVREC](symbol-options.md#symopt-ignore-cvrec)します。

<span id="_______-sins______"></span><span id="_______-SINS______"></span> **-sins**   
原因のデバッガーがシンボル パスと実行可能ファイル イメージのパス環境変数を無視します。 詳細については、次を参照してください。 [SYMOPT\_無視\_NT\_SYMPATH](symbol-options.md#symopt-ignore-nt-sympath)します。

<span id="_______-snc______"></span><span id="_______-SNC______"></span> **-snc**   
原因のデバッガーが C++ の変換をオフにします。 詳細については、およびこれを制御するための他の方法については、「 [SYMOPT\_いいえ\_CPP](symbol-options.md#symopt-no-cpp)します。

<span id="_______-snul______"></span><span id="_______-SNUL______"></span> **-snul**   
非修飾名のシンボルの自動読み込みを無効にします。 詳細については、およびこれを制御するための他の方法については、「 [SYMOPT\_いいえ\_UNQUALIFIED\_読み込み](symbol-options.md#symopt-no-unqualified-loads)します。

<span id="_______-srcpath_______SourcePath______"></span><span id="_______-srcpath_______sourcepath______"></span><span id="_______-SRCPATH_______SOURCEPATH______"></span> **-srcpath** *SourcePath*   
ソース ファイルの検索パスを指定します。 複数のパスをセミコロンで区切ります (**;**)。 パスにスペースが含まれている場合は、引用符で囲む必要があります。 詳細については、およびこのパスを変更するには、他の方法については、「[ソース パス](source-path.md)します。

<span id="_______-sup______"></span><span id="_______-SUP______"></span> **-sup**   
すべてのシンボルの検索中に、パブリック シンボル テーブルを検索するシンボルのハンドラーをによりします。 詳細については、およびこれを制御するための他の方法については、「 [SYMOPT\_自動\_PUBLICS](symbol-options.md#symopt-auto-publics)します。

<span id="_______-T_______Title______"></span><span id="_______-t_______title______"></span><span id="_______-T_______TITLE______"></span> **-T** *タイトル*   
WinDbg ウィンドウのタイトルを設定します。

<span id="_______-v______"></span><span id="_______-V______"></span> **-v**   
デバッガーから詳細な出力を有効にします。

<span id="_______-W_______Workspace______"></span><span id="_______-w_______workspace______"></span><span id="_______-W_______WORKSPACE______"></span> **-W** *ワークスペース*   
指定された名前付きのワークスペースを読み込みます。 ワークスペース名にスペースが含まれている場合は、引用符で囲みます。 この名前のワークスペースが存在しない場合のこの名前の新しいワークスペースを作成または読み込み操作を中止するオプションが表示されます。 詳細については、次を参照してください。[を使用してワークスペース](using-workspaces.md)します。

<span id="_______-WF_______Filename______"></span><span id="_______-wf_______filename______"></span><span id="_______-WF_______FILENAME______"></span> **-WF** *ファイル名*   
指定されたファイルからワークスペースを読み込みます。 *ファイル名*ファイルと拡張機能 (通常は .wew) を含める必要があります。 ワークスペース名にスペースが含まれている場合は、引用符で囲みます。 この名前のワークスペースのファイルが存在しない場合のこの名前の新しいワークスペース ファイルを作成または読み込み操作を中止するオプションが表示されます。 詳細については、次を参照してください。[を使用してワークスペース](using-workspaces.md)します。

<span id="_______-WX______"></span><span id="_______-wx______"></span> **-WX**   
ワークスペースの自動読み込みを無効にします。 詳細については、次を参照してください。[を使用してワークスペース](using-workspaces.md)します。

<span id="_______-y_______SymbolPath______"></span><span id="_______-y_______symbolpath______"></span><span id="_______-Y_______SYMBOLPATH______"></span> **-y** *SymbolPath*   
シンボルの検索パスを指定します。 複数のパスをセミコロンで区切ります (**;**)。 パスにスペースが含まれている場合は、引用符で囲む必要があります。 詳細については、およびこのパスを変更するには、他の方法については、「[シンボル パス](symbol-path.md)します。

<span id="_______-z_______DumpFile______"></span><span id="_______-z_______dumpfile______"></span><span id="_______-Z_______DUMPFILE______"></span> **-z** *DumpFile*   
デバッグするクラッシュ ダンプ ファイルの名前を指定します。 パスとファイル名にスペースが含まれている場合、これを引用符で囲む必要があります。 複数を含めることによって、いくつかのダンプ ファイルを一度に開くことは **-z**オプション、各の後に、異なる*DumpFile*値。 詳細については、次を参照してください。[ユーザー モード ダンプ ファイルの分析](analyzing-a-user-mode-dump-file.md)または[WinDbg にカーネル モードのダンプ ファイルの分析](analyzing-a-kernel-mode-dump-file-with-windbg.md)します。

<span id="_______-zp_______PageFile______"></span><span id="_______-zp_______pagefile______"></span><span id="_______-ZP_______PAGEFILE______"></span> **-zp** *PageFile*   
変更されたページのファイルの名前を指定します。 デバッグ ダンプ ファイルを使用する場合に便利ですが、 [ **.pagein (メモリ内のページ)** ](-pagein--page-in-memory-.md)コマンド。 使用することはできません **-zp**標準 Windows ページファイル--ページ ファイルを特別に変更のみを使用できます。

<span id="_______executable______"></span><span id="_______EXECUTABLE______"></span> *実行可能ファイル*   
実行可能ファイルのプロセスのコマンドラインを指定します。 これは、新しいプロセスを起動し、デバッグに使用されます。 コマンドラインで最後の項目をする必要があります。 実行可能ファイル名が渡された後引数の文字列として実行可能ファイルへのすべてのテキスト。 詳細については、次を参照してください。[デバッグ ユーザー モード プロセスを使用して WinDbg](debugging-a-user-mode-process-using-windbg.md)します。

<span id="_______-_______"></span> **-?**   
この HTML ヘルプ ウィンドウが表示されます。

コマンドラインからデバッガーを実行するときは、アプリケーションのファイル名の後にターゲット アプリケーションの引数を指定します。 例:

```dbgcmd
windbg myexe arg1 arg2
```

 

 






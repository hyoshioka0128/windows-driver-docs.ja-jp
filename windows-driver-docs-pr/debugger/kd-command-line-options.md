---
title: KD のコマンドライン オプション
description: KD の初回使用時のユーザーは、デバッグを使用して KD と NTKD セクションで開始する必要があります。
ms.assetid: 76c11b45-8469-4f27-840d-06477d8922b8
keywords:
- KD コマンド ライン オプションの Windows デバッグ
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- KD Command-Line Options
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 30c2ec62ee88c9ae1bfe68388bf9e15016f6fc16
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63367222"
---
# <a name="kd-command-line-options"></a>KD のコマンドライン オプション


KD の初回使用時のユーザーで始まり、[デバッグを使用して KD と NTKD](debugging-using-kd-and-ntkd.md)セクション。

KD コマンドラインは、次の構文を使用します。

```dbgcmd
kd [ -server ServerTransport | -remote ClientTransport ] 
   [-b | -x] [-d] [-bonc] [-m] [-myob] [-lines] [-n] [-r] [-s] 
   [-v] [-clines lines] [-failinc] [-noio] [-noshell] 
   [-secure] [-sdce] [-ses] [-sicv] [-sins] [-snc] [-snul]
   [-sup] [-sflags 0xNumber] [-log{a|au|o|ou} LogFile] 
   [-aExtension] [-zp PageFile] 
   [-i ImagePath] [-y SymbolPath]  [-srcpath SourcePath] 
   [-k ConnectType | -kl | -kqm | -kx ExdiOptions] [-ee {masm|c++}] 
   [-z DumpFile] [-cf "filename"] [-cfr "filename"] [-c "command"] 
   [-t PrintErrorLevel] [-version] 

kd -iu KeyString

kd -QR Server 

kd -wake PID 

kd -?
```

KD コマンド ライン オプションの説明に従ってください。 のみ、 **-リモート**と **-サーバー**オプション小文字が区別されます。 最初のハイフンは、フォワード スラッシュ (/) に置き換えることができます。 その他のパラメーターを取らないオプションを連結できます - ように**kd-r-n-v**として記述できます**kd rnv**します。

場合、 **-リモート**または **-サーバー**オプションを使用すると、コマンドラインでその他のオプションの前にする必要があります。

## <a name="span-idddkkdcommandlineoptionsdbgspanspan-idddkkdcommandlineoptionsdbgspanparameters"></a><span id="ddk_kd_command_line_options_dbg"></span><span id="DDK_KD_COMMAND_LINE_OPTIONS_DBG"></span>パラメーター


<span id="_______-server_______ServerTransport______"></span><span id="_______-server_______servertransport______"></span><span id="_______-SERVER_______SERVERTRANSPORT______"></span> **-server** *ServerTransport*   
その他のデバッガーによってアクセスできるデバッグ サーバーを作成します。 については、使用可能な*サーバトランスポート*を参照してください[**デバッグ サーバー アクティブ化する**](activating-a-debugging-server.md)します。 このパラメーターを使用すると、コマンドラインで最初のパラメーターがあります。

<span id="_______-remote_______ClientTransport______"></span><span id="_______-remote_______clienttransport______"></span><span id="_______-REMOTE_______CLIENTTRANSPORT______"></span> **-remote** *ClientTransport*   
デバッグ クライアントを作成し、既に実行されているデバッグ サーバーに接続します。 については、使用可能な*ClientTransport*値を参照してください[**デバッグ クライアントをアクティブ化する**](activating-a-debugging-client.md)します。 このパラメーターを使用すると、コマンドラインで最初のパラメーターがあります。

<span id="_______-a________Extension______"></span><span id="_______-a________extension______"></span><span id="_______-A________EXTENSION______"></span> **-** *拡張機能*   
既定の拡張 DLL を設定します。 既定値は kdextx86.dll kdexts.dll します。 後にスペースが必要ない、"a"の .dll ファイル名拡張子を含めることはできません。 詳細、およびこの既定の設定の他のメソッドでは、次を参照してください。[デバッガー拡張 Dll の読み込み](loading-debugger-extension-dlls.md)します。

<span id="_______-b______"></span><span id="_______-B______"></span> **-b**   
このオプションはサポートされなくなりました。

<span id="_______-bonc______"></span><span id="_______-BONC______"></span> **-bonc**   
このオプションが指定されている場合は、セッションを開始するとすぐに、ターゲットに、デバッガーが中断されます。 これは、機能は、ターゲットが現在壊れていないデバッグ サーバーに接続するときに特に便利です。

<span id="_______-c__command_______"></span><span id="_______-C__COMMAND_______"></span> **-c "** <em>command</em> **"**    
起動時に実行する初期のデバッガー コマンドを指定します。 このコマンドは、引用符で囲む必要があります。 複数のコマンドは、セミコロンで区切ることができます。 (長いコマンド リストがあれば、スクリプト内に配置し、使用する方が簡単なる、 **-c**オプションは、 [  **$ &lt;、$&gt;&lt;、$&gt; &lt;、$$&gt; &lt; (スクリプト ファイルを実行)** ](-----------------------a---run-script-file-.md)コマンド)。

デバッグ クライアントを開始すると、このコマンドは必要があります、デバッグ サーバー向けです。 などの特定のクライアントのコマンド **.lsrcpath**、許可されていません。

<span id="_______-cf__filename_______"></span><span id="_______-CF__FILENAME_______"></span> **-cf "** <em>filename</em> **"**    
スクリプト ファイルの名前とパスを指定します。 このスクリプト ファイルは、デバッガーを起動するとすぐに実行されます。 場合*filename*引用符で囲む必要があるスペースが含まれています。 パスを省略した場合、現在のディレクトリが使用されます。 Cf オプションを使用しない場合は、現在のディレクトリにファイル ntsd.ini がスクリプト ファイルとして使用されます。 ファイルが存在しない場合は、エラーは発生しません。 詳細については、次を参照してください。[スクリプト ファイルを使用する](using-script-files.md)します。

<span id="_______-cfr__filename_______"></span><span id="_______-CFR__FILENAME_______"></span> **-cfr "** <em>filename</em> **"**    
スクリプト ファイルの名前とパスを指定します。 このスクリプト ファイルは、デバッガーが開始され、いつでも、ターゲットが再起動すると、すぐに実行されます。 場合*filename*引用符で囲む必要があるスペースが含まれています。 パスを省略した場合、現在のディレクトリが使用されます。 ファイルが存在しない場合は、エラーは発生しません。 詳細については、次を参照してください。[スクリプト ファイルを使用する](using-script-files.md)します。

<span id="_______-clines________lines______"></span><span id="_______-CLINES________LINES______"></span> **-clines** *行*   
リモート デバッグ中にアクセスできるコマンドの履歴には、コマンドのおおよその数を設定します。 詳細については、およびこの数を変更するには、他の方法については、「[デバッガー コマンドを使用して](using-debugger-commands.md)します。

<span id="_______-d______"></span><span id="_______-D______"></span> **-d**   
再起動後、デバッガーは、カーネル モジュールが読み込まれるとすぐに目的のコンピュータに中断されます。 (この区切りが以前からの離別、 **-b**オプション)。参照してください[クラッシュし、ターゲット コンピューターを再起動](crashing-and-rebooting-the-target-computer.md)とこの状態を変更するには、他の方法の詳細についてはします。

<span id="_______-ee__masm_c___"></span><span id="_______-EE__MASM_C___"></span> **-ee** {**masm**|**c++** }  
既定の式エバリュエーターを設定します。 場合**masm**指定すると、MASM 式の構文が使用されます。 場合**c++** 指定すると、C++ 式の構文が使用されます。 場合、 **ee**オプションを省略すると、MASM 式の構文は、既定値として使用されます。 参照してください[を評価する式](evaluating-expressions.md)詳細についてはします。

<span id="_______-failinc______"></span><span id="_______-FAILINC______"></span> **-failinc**   
原因の問題のあるシンボルを無視するデバッガー。 ユーザー モードまたはカーネル モードのミニダンプ ファイルをデバッグするには、このオプションは、デバッガーをイメージをマップすることはできませんのすべてのモジュールを読み込むようにも。 詳細については、およびこれを制御するための他の方法については、「 [SYMOPT\_EXACT\_シンボル](symbol-options.md#symopt-exact-symbols)します。

<span id="_______-i_______ImagePath______"></span><span id="_______-i_______imagepath______"></span><span id="_______-I_______IMAGEPATH______"></span> **-i** *ImagePath*   
違反を生成した実行可能ファイルの場所を指定します。 パスにスペースが含まれている場合は、引用符で囲む必要があります。

<span id="_______-iu________KeyString______"></span><span id="_______-iu________keystring______"></span><span id="_______-IU________KEYSTRING______"></span> **-iu** *KeyString*   
ユーザーは自動起動 url のデバッガーのリモート クライアントするためには、デバッガーのリモート処理、URL の種類として登録します。 *KeyString*形式`remdbgeng://RemotingOption`します。 *RemotingOption*トピックで定義されているトランスポート プロトコルを定義する文字列は、 [**デバッグ クライアントをアクティブ化する**](activating-a-debugging-client.md)します。 この操作が成功すると、メッセージは表示されません。失敗した場合、エラー メッセージが表示されます。

**-Iu**パラメーターは、その他のパラメーターを使用する必要があります。 このコマンドは KD を実際に開始されません。

<span id="_______-k_______ConnectType______"></span><span id="_______-k_______connecttype______"></span><span id="_______-K_______CONNECTTYPE______"></span> **-k** *ConnectType*   
デバッガーのターゲットに接続する方法を指示します。 詳細については、次を参照してください。[デバッグを使用して KD と NTKD](debugging-using-kd-and-ntkd.md)します。

<span id="_______-kl______"></span><span id="_______-KL______"></span> **-kl**   
カーネル デバッガーと同じコンピューター上のセッションのデバッグを開始します。

<span id="_______-kqm______"></span><span id="_______-KQM______"></span> **-kqm**   
KD をサイレント モードで起動します。

<span id="_______-kx_______ExdiOptions______"></span><span id="_______-kx_______exdioptions______"></span><span id="_______-KX_______EXDIOPTIONS______"></span> **-kx** *ExdiOptions*   
カーネル デバッグ EXDI ドライバーを使用してセッションを開始します。 EXDI ドライバーは、このドキュメントでは説明しません。 場合は、ハードウェアのプローブやハードウェア シミュレーターに EXDI インターフェイスがある場合は、デバッグ情報を Microsoft に問い合わせてください。

<span id="_______-lines______"></span><span id="_______-LINES______"></span> **-lines**   
ソース行のデバッグを有効にします。 このオプションを省略した場合、 [ **.lines (切り替えのソース行のサポート)** ](-lines--toggle-source-line-support-.md)コマンドがソースのデバッグが許可される前に使用する必要があります。 これを制御するための他の方法では、次を参照してください。 [SYMOPT\_ロード\_行](symbol-options.md#symopt-load-lines)します。

<span id="_______-log_a_au_o_ou__LogFile"></span><span id="_______-log_a_au_o_ou__logfile"></span><span id="_______-LOG_A_AU_O_OU__LOGFILE"></span> **-log**{**a|au|o|ou**} *LogFile*  
ログ ファイルにログ情報を開始します。 場合*ログ ファイル*が既に存在する場合は上書きされます **-ロゴ**を使用する場合にその出力がファイルに追加されますまたは **- loga**使用されます。 **- Logau**と **- logou**オプション操作のような **- loga**と **-ロゴ**それぞれを除き、ログ ファイルが Unicode ファイルであります。 詳細については、次を参照してください。 [KD にログ ファイルを保持](keeping-a-log-file-in-kd.md)します。

<span id="_______-m______"></span><span id="_______-M______"></span> **-m**   
シリアル ポートがモデムに接続されていることを示します。 ウォッチするデバッガーに指示、通信事業者の信号を検出します。

<span id="_______-myob______"></span><span id="_______-MYOB______"></span> **-myob**   
Dbghelp.dll をバージョンの不一致がある場合、デバッガーは実行し続けます。 (なし、 **- myob**スイッチと見なされます、致命的なエラー)。

このオプションのセカンダリの効果は、通常、ターゲット コンピューターに中断するときに表示される警告を抑制することです。

<span id="_______-n______"></span><span id="_______-N______"></span> **-n**   
*ノイズの多いシンボルの読み込み*:シンボル ハンドラーから詳細な出力を有効にします。 詳細については、およびこれを制御するための他の方法については、「 [SYMOPT\_デバッグ](symbol-options.md#symopt-debug)します。

<span id="_______-noio______"></span><span id="_______-NOIO______"></span> **-noio**   
デバッグ サーバーが使用されている入力または出力するを防ぎます。 入力は、デバッグのクライアントからのみ受け付けられます (さらに任意の最初のコマンドやコマンドのスクリプトで指定された、 **-c**コマンド ライン オプション)。

すべての出力は、デバッグのクライアントに転送されます。 詳細については、次を参照してください。 [**デバッグ サーバー アクティブ化する**](activating-a-debugging-server.md)します。

<span id="_______-noshell______"></span><span id="_______-NOSHELL______"></span> **-noshell**   
すべてを禁止 **.shell**コマンド。 この禁止は、新しいデバッグ セッションが開始された場合でも、デバッガーが実行されている限り最後されます。 詳細については、および他のシェル コマンドを無効にする方法については、「[シェル コマンドを使用して](using-shell-commands.md)します。

<span id="_______-QR_______Server______"></span><span id="_______-qr_______server______"></span><span id="_______-QR_______SERVER______"></span> **-QR** *サーバー*   
指定したネットワーク サーバーで実行されているすべてのデバッグ サーバーの一覧を表示します。 二重の円記号 ( **\\\\** ) 前*Server*は省略可能です。 参照してください[**デバッグ サーバーの検索**](searching-for-debugging-servers.md)詳細についてはします。

**-QR**パラメーターは、その他のパラメーターを使用する必要があります。 このコマンドは KD を実際に開始されません。

<span id="_______-r______"></span><span id="_______-R______"></span> **-r**   
レジスタが表示されます。

<span id="_______-s______"></span><span id="_______-S______"></span> **-s**   
シンボルの遅延読み込みを無効にします。 これにより、プロセスの起動速度が低下します。 詳細については、およびこれを制御するための他の方法については、「 [SYMOPT\_遅延\_読み込み](symbol-options.md#symopt-deferred-loads)します。

<span id="_______-sdce______"></span><span id="_______-SDCE______"></span> **-sdce**   
デバッガー表示が**ファイル アクセス エラー**シンボルの読み込み中にダイアログ ボックス。 詳細については、およびこれを制御するための他の方法については、「 [SYMOPT\_失敗\_重大\_エラー](symbol-options.md#symopt-fail-critical-errors)します。

<span id="_______-secure______"></span><span id="_______-SECURE______"></span> **-secure**   
アクティブに[保護モード](secure-mode.md)します。

<span id="_______-ses______"></span><span id="_______-SES______"></span> **-ses**   
原因のデバッガーがすべてのシンボル ファイルの厳密な評価を実行し、問題のある任意の記号を無視します。 詳細については、およびこれを制御するための他の方法については、「 [SYMOPT\_EXACT\_シンボル](symbol-options.md#symopt-exact-symbols)します。

<span id="_______-sflags_0xNumber"></span><span id="_______-sflags_0xnumber"></span><span id="_______-SFLAGS_0XNUMBER"></span> **sflags 0 x * * * 数*  
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
ソース ファイルの検索パスを指定します。 複数のパスをセミコロンで区切ります ( **;** )。 パスにスペースが含まれている場合は、引用符で囲む必要があります。 詳細については、およびこのパスを変更するには、他の方法については、「[ソース パス](source-path.md)します。

<span id="_______-sup______"></span><span id="_______-SUP______"></span> **-sup**   
すべてのシンボルの検索中に、パブリック シンボル テーブルを検索するシンボルのハンドラーをによりします。 詳細については、およびこれを制御するための他の方法については、「 [SYMOPT\_自動\_PUBLICS](symbol-options.md#symopt-auto-publics)します。

<span id="_______-t________PrintErrorLevel______"></span><span id="_______-t________printerrorlevel______"></span><span id="_______-T________PRINTERRORLEVEL______"></span> **-t** *PrintErrorLevel*   
デバッガーはエラー メッセージを表示すると、エラー レベルを指定します。 これは、0、1、2、または 3 と等しい 10 進数です。 値は次のとおりです。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">Value</th>
<th align="left">定数</th>
<th align="left">意味</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>0</p></td>
<td align="left"><p>なし</p></td>
<td align="left"><p>すべてのエラーは表示されません。</p></td>
</tr>
<tr class="even">
<td align="left"><p>1</p></td>
<td align="left"><p>エラー</p></td>
<td align="left"><p>エラー レベルのデバッグ イベントを表示します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>2</p></td>
<td align="left"><p>MINORERROR</p></td>
<td align="left"><p>デバッグ イベント MINORERROR とエラーのレベルを表示します。</p></td>
</tr>
<tr class="even">
<td align="left"><p>3</p></td>
<td align="left"><p>警告</p></td>
<td align="left"><p>デバッグ イベント、警告、MINORERROR、およびエラーのレベルを表示します。</p></td>
</tr>
</tbody>
</table>

 

このエラーのレベルは、Microsoft Windows のチェック ビルドにだけ意味を持ちます。 既定値は 1 です。

<span id="_______-v______"></span><span id="_______-V______"></span> **-v**   
読み込み、遅延読み込みは、詳細メッセージを生成し、アンロードします。

<span id="_______-version______"></span><span id="_______-VERSION______"></span> **-version**   
デバッガーのバージョン文字列を出力します。

<span id="_______-wake_______PID______"></span><span id="_______-wake_______pid______"></span><span id="_______-WAKE_______PID______"></span> **-wake** *PID*   
原因はスリープ モードでプロセス ID が指定されたユーザー モード デバッガーの終了を*PID*します。 このコマンドは、ターゲット コンピューターのスリープ モード中に発行する必要があります。 参照してください[カーネル デバッガーからユーザー モード デバッガーの制御](controlling-the-user-mode-debugger-from-the-kernel-debugger.md)詳細についてはします。

**-Wake**パラメーターは、その他のパラメーターを使用する必要があります。 このコマンドは KD を実際に開始されません。

<span id="_______-x______"></span><span id="_______-X______"></span> **-x**   
デバッガーが対処できるようにすること、アプリケーションや、例外の原因となったモジュールではなく、例外が最初に発生したとき中断を発生します。 (同じ **-b**、初期を除く**eb nt!検査 9; g**コマンド)。

<span id="_______-y_______SymbolPath______"></span><span id="_______-y_______symbolpath______"></span><span id="_______-Y_______SYMBOLPATH______"></span> **-y** *SymbolPath*   
シンボルの検索パスを指定します。 複数のパスをセミコロンで区切ります ( **;** )。 パスにスペースが含まれている場合は、引用符で囲む必要があります。 詳細については、およびこのパスを変更するには、他の方法については、「[シンボル パス](symbol-path.md)します。

<span id="_______-z_______DumpFile______"></span><span id="_______-z_______dumpfile______"></span><span id="_______-Z_______DUMPFILE______"></span> **-z** *DumpFile*   
デバッグするクラッシュ ダンプ ファイルの名前を指定します。 パスとファイル名にスペースが含まれている場合、これを引用符で囲む必要があります。 複数を含めることによって、いくつかのダンプ ファイルを一度に開くことは **-z**オプション、各の後に、異なる*DumpFile*値。 詳細については、次を参照してください。 [KD とカーネル モードのダンプ ファイルの分析](analyzing-a-kernel-mode-dump-file-with-kd.md)します。

<span id="_______-zp_______PageFile______"></span><span id="_______-zp_______pagefile______"></span><span id="_______-ZP_______PAGEFILE______"></span> **-zp** *PageFile*   
変更されたページのファイルの名前を指定します。 デバッグ ダンプ ファイルを使用する場合に便利ですが、 [ **.pagein (メモリ内のページ)** ](-pagein--page-in-memory-.md)コマンド。 使用することはできません **-zp**標準 Windows ページファイルを — のみ特別に変更されたファイルにページを使用できます。

<span id="_______-_______"></span> **-?**    
ヘルプをコマンド ラインを表示します。

KD では、ターゲットが実行されているプラットフォームを自動的に検出されます。 KD コマンドラインでターゲットを指定する必要はありません。 古い構文 (名前を使用して*I386KD*または*IA64KD*) は廃止されています。

 

 






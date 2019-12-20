---
title: KD のコマンドライン オプション
description: KD の最初のユーザーは、KD と NTKD セクションを使用したデバッグを開始する必要があります。
ms.assetid: 76c11b45-8469-4f27-840d-06477d8922b8
keywords:
- KD のコマンドラインオプション Windows のデバッグ
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- KD Command-Line Options
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: ccaaaa3dfd5918262df6410ff966c8579214d1f7
ms.sourcegitcommit: d30691c8276f7dddd3f8333e84744ddeea1e1020
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/19/2019
ms.locfileid: "75209836"
---
# <a name="kd-command-line-options"></a>KD のコマンドライン オプション


KD の最初のユーザーは、 [kd と NTKD セクションを使用](debugging-using-kd-and-ntkd.md)したデバッグを開始する必要があります。

KD コマンドラインでは、次の構文を使用します。

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

KD のコマンドラインオプションの説明は次のようになります。 **-Remote**オプションと **-server**オプションだけでは、大文字と小文字が区別されます。 先頭のハイフンは、スラッシュ (/) に置き換えることができます。 追加のパラメーターを受け取らないオプションは連結できます。したがって、 **kd** - **rnv**として書き込むことができます。

**-Remote**または **-server**オプションを使用する場合は、コマンドラインの他のオプションの前に指定する必要があります。

## <a name="span-idddk_kd_command_line_options_dbgspanspan-idddk_kd_command_line_options_dbgspanparameters"></a><span id="ddk_kd_command_line_options_dbg"></span><span id="DDK_KD_COMMAND_LINE_OPTIONS_DBG"></span>パラメータ


<span id="_______-server_______ServerTransport______"></span><span id="_______-server_______servertransport______"></span><span id="_______-SERVER_______SERVERTRANSPORT______"></span>**-server** *servertransport*   
他のデバッガーからアクセスできるデバッグサーバーを作成します。 使用可能な*Servertransport*の詳細については、「[**デバッグサーバーのアクティブ化**](activating-a-debugging-server.md)」を参照してください。 このパラメーターを使用する場合は、コマンドラインの最初のパラメーターである必要があります。

<span id="_______-remote_______ClientTransport______"></span><span id="_______-remote_______clienttransport______"></span><span id="_______-REMOTE_______CLIENTTRANSPORT______"></span>**-リモート** *clienttransport*   
デバッグクライアントを作成し、既に実行されているデバッグサーバーに接続します。 使用可能な*Clienttransport*値の詳細については、「[**デバッグクライアントのアクティブ化**](activating-a-debugging-client.md)」を参照してください。 このパラメーターを使用する場合は、コマンドラインの最初のパラメーターである必要があります。

<span id="_______-a________Extension______"></span><span id="_______-a________extension______"></span><span id="_______-A________EXTENSION______"></span>**-** *拡張機能*   
既定の拡張 DLL を設定します。 既定値は kdextx86 または kdexts です。 "A" の後にスペースを入れないでください。また、.dll ファイル名拡張子を含めることはできません。 この既定値を設定するその他の方法については、「[デバッガー拡張 dll の読み込み](loading-debugger-extension-dlls.md)」を参照してください。

<span id="_______-b______"></span><span id="_______-B______"></span>**-b**   
このオプションはサポートされなくなりました。

<span id="_______-bonc______"></span><span id="_______-BONC______"></span>**-bonc**   
このオプションを指定した場合、デバッガーはセッションが開始されるとすぐにターゲットに中断します。 これは、現在ターゲットに分割されていない可能性があるデバッグサーバーに接続する場合に特に便利です。

<span id="_______-c__command_______"></span><span id="_______-C__COMMAND_______"></span>**-c "**<em>command</em>**"**   
起動時に実行する初期デバッガーコマンドを指定します。 このコマンドは引用符で囲む必要があります。 複数のコマンドは、セミコロンで区切ることができます。 (長いコマンドリストがある場合は、それをスクリプトに挿入し、 **-c**オプションを[**$&lt;、$&gt;&lt;、$&gt;&lt;、$ $&gt;&lt; (スクリプトファイルの実行)**](-----------------------a---run-script-file-.md)コマンドで使用する方が簡単な場合があります)。

デバッグクライアントを開始する場合、このコマンドはデバッグサーバーを対象としている必要があります。 **Lsrcpath**などのクライアント固有のコマンドは使用できません。

<span id="_______-cf__filename_______"></span><span id="_______-CF__FILENAME_______"></span>**-cf "**<em>filename</em>**"**   
スクリプトファイルのパスと名前を指定します。 このスクリプトファイルは、デバッガーが開始されるとすぐに実行されます。 *Filename*にスペースが含まれている場合は、引用符で囲む必要があります。 パスを省略した場合は、現在のディレクトリと見なされます。 -Cf オプションが使用されていない場合、現在のディレクトリの ntsd ファイルがスクリプトファイルとして使用されます。 ファイルが存在しない場合、エラーは発生しません。 詳細については、「[スクリプトファイルの使用](using-script-files.md)」を参照してください。

<span id="_______-cfr__filename_______"></span><span id="_______-CFR__FILENAME_______"></span>**-cfr "**<em>filename</em>**"**   
スクリプトファイルのパスと名前を指定します。 このスクリプトファイルは、デバッガーが開始されたときと、ターゲットが再起動されるとすぐに実行されます。 *Filename*にスペースが含まれている場合は、引用符で囲む必要があります。 パスを省略した場合は、現在のディレクトリと見なされます。 ファイルが存在しない場合、エラーは発生しません。 詳細については、「[スクリプトファイルの使用](using-script-files.md)」を参照してください。

<span id="_______-clines________lines______"></span><span id="_______-CLINES________LINES______"></span>**-clines** *lines*   
リモートデバッグ中にアクセスできるコマンド履歴のコマンドの概数を設定します。 詳細と、この数を変更するその他の方法については、「[デバッガーコマンドの使用](using-debugger-commands.md)」を参照してください。

<span id="_______-d______"></span><span id="_______-D______"></span>**-d**   
再起動後、カーネルモジュールが読み込まれるとすぐに、デバッガーはターゲットコンピューターを中断します。 (これは、 **-b**オプションの中断よりも前のものです)。詳細およびこの状態を変更するその他の方法については、「[ターゲットコンピューターのクラッシュと再起動](crashing-and-rebooting-the-target-computer.md)」を参照してください。

<span id="_______-ee__masm_c___"></span><span id="_______-EE__MASM_C___"></span>**-ee** {**masm**|**c++**}  
既定の式エバリュエーターを設定します。 **Masm**が指定されている場合は、masm 式の構文が使用されます。 **C++** が指定されC++ている場合は、式の構文が使用されます。 **-Ee**オプションを省略した場合、MASM 式の構文が既定値として使用されます。 詳細については、「[式の評価](evaluating-expressions.md)」をご覧ください。

<span id="_______-failinc______"></span><span id="_______-FAILINC______"></span>**-failinc**   
デバッガーが疑わしいシンボルをすべて無視します。 ユーザーモードまたはカーネルモードのミニダンプファイルをデバッグする場合、このオプションを使用すると、イメージをマップできないモジュールをデバッガーで読み込むことができなくなります。 詳細およびその他の制御方法については、「 [Symopt\_EXACT\_SYMBOLS](symbol-options.md#symopt-exact-symbols)」を参照してください。

<span id="_______-i_______ImagePath______"></span><span id="_______-i_______imagepath______"></span><span id="_______-I_______IMAGEPATH______"></span>**-i** *ImagePath*   
エラーを生成した実行可能ファイルの場所を指定します。 パスにスペースが含まれている場合は、引用符で囲む必要があります。

<span id="_______-iu________KeyString______"></span><span id="_______-iu________keystring______"></span><span id="_______-IU________KEYSTRING______"></span>**-iu** *keystring*   
Url 型としてデバッガーのリモート処理を登録し、ユーザーが URL を使用してデバッガーのリモートクライアントを自動起動できるようにします。 *Keystring*には `remdbgeng://RemotingOption`の形式があります。 *Remotingoption*は、「[**デバッグクライアントをアクティブ化する**](activating-a-debugging-client.md)」で定義されているトランスポートプロトコルを定義する文字列です。 この操作が成功した場合、メッセージは表示されません。失敗した場合は、エラーメッセージが表示されます。

**-Iu**パラメーターは、他のパラメーターと共に使用することはできません。 このコマンドは、実際には KD を開始しません。

<span id="_______-k_______ConnectType______"></span><span id="_______-k_______connecttype______"></span><span id="_______-K_______CONNECTTYPE______"></span>**-k** *connecttype*   
ターゲットに接続する方法をデバッガーに指示します。 詳細については、「 [KD と NTKD を使用](debugging-using-kd-and-ntkd.md)したデバッグ」を参照してください。

<span id="_______-kl______"></span><span id="_______-KL______"></span>**-kl ダイバージェンス**   
デバッガーと同じコンピューター上でカーネルデバッグセッションを開始します。

<span id="_______-kqm______"></span><span id="_______-KQM______"></span>**-kqm**   
非表示モードで KD を開始します。

<span id="_______-kx_______ExdiOptions______"></span><span id="_______-kx_______exdioptions______"></span><span id="_______-KX_______EXDIOPTIONS______"></span>**-kx** *exdioptions*   
EXDI ドライバーを使用して、カーネルデバッグセッションを開始します。 EXDI ドライバーについては、このドキュメントでは説明しません。 ハードウェアプローブまたはハードウェアシミュレーターへの EXDI インターフェイスがある場合は、デバッグ情報について Microsoft にお問い合わせください。

<span id="_______-lines______"></span><span id="_______-LINES______"></span>**-行**   
ソース行のデバッグを有効にします。 このオプションを省略した場合は、ソースのデバッグを許可する前に、 [**. lines (ソースラインサポートの切り替え)**](-lines--toggle-source-line-support-.md)コマンドを使用する必要があります。 これを制御するその他の方法については、「 [Symopt\_LOAD\_LINES](symbol-options.md#symopt-load-lines)」を参照してください。

<span id="_______-log_a_au_o_ou__LogFile"></span><span id="_______-log_a_au_o_ou__logfile"></span><span id="_______-LOG_A_AU_O_OU__LOGFILE"></span>**-ログ**{**a | au | o | ou**}*ログファイル*  
ログファイルへの情報のログ記録を開始します。 *LogFile*が既に存在する場合は、 **-logo**が使用されていると上書きされます。 **-loga**が使用されている場合は、出力がファイルに追加されます。 **-Logau**オプションと **-logau**オプションは、それぞれ、ログファイルが Unicode ファイルであることを除いて、 **-logau**および-- **logo**と同様に動作します。 詳細については、「 [KD でのログファイルの保持](keeping-a-log-file-in-kd.md)」を参照してください。

<span id="_______-m______"></span><span id="_______-M______"></span>**-m**   
シリアルポートがモデムに接続されていることを示します。 キャリア検出シグナルを監視するようにデバッガーに指示します。

<span id="_______-myob______"></span><span id="_______-MYOB______"></span>**-myob**   
Dbghelp .dll とのバージョンが一致しない場合、デバッガーは引き続き実行されます。 ( **-Myob**スイッチがないと、これは致命的なエラーと見なされます)。

このオプションの2つ目の効果は、対象のコンピューターに侵入したときに通常表示される警告が表示されないことです。

<span id="_______-n______"></span><span id="_______-N______"></span>**-n**   
*ノイズシンボルの読み込み*: シンボルハンドラーからの詳細出力を有効にします。 詳細およびその他の制御方法については、「 [Symopt\_デバッグ](symbol-options.md#symopt-debug)」を参照してください。

<span id="_______-noio______"></span><span id="_______-NOIO______"></span>**-noio**   
デバッグサーバーを入力または出力に使用しないようにします。 入力は、デバッグクライアント (および **-c**コマンドラインオプションで指定された最初のコマンドまたはコマンドスクリプト) からのみ受け入れられます。

すべての出力は、デバッグクライアントに送られます。 詳細については、「[**デバッグサーバーのアクティブ化**](activating-a-debugging-server.md)」を参照してください。

<span id="_______-noshell______"></span><span id="_______-NOSHELL______"></span>**-noshell**   
すべて**のシェル**コマンドを禁止します。 この禁止は、新しいデバッグセッションが開始された場合でも、デバッガーが実行されている限り最後に実行されます。 詳細と、シェルコマンドを無効にするその他の方法については、「[シェルコマンドの使用](using-shell-commands.md)」を参照してください。

<span id="_______-QR_______Server______"></span><span id="_______-qr_______server______"></span><span id="_______-QR_______SERVER______"></span>**-QR** *サーバー*   
指定したネットワークサーバー上で実行されているすべてのデバッグサーバーを一覧表示します。 *サーバー*の前にある2つの円記号 (**\\\\**) は省略可能です。 詳細については、「[**デバッグサーバーの検索**](searching-for-debugging-servers.md)」を参照してください。

**-QR**パラメーターを他のパラメーターと共に使用することはできません。 このコマンドは、実際には KD を開始しません。

<span id="_______-r______"></span><span id="_______-R______"></span>**-r**   
レジスタを表示します。

<span id="_______-s______"></span><span id="_______-S______"></span>**-s**   
遅延シンボルの読み込みを無効にします。 これにより、プロセスの起動が遅くなります。 詳細およびその他の制御方法については、「 [Symopt\_遅延\_読み込み](symbol-options.md#symopt-deferred-loads)」を参照してください。

<span id="_______-sdce______"></span><span id="_______-SDCE______"></span>**-sdce**   
シンボルの読み込み中に、デバッガーが**ファイルアクセスエラー**ダイアログボックスを表示します。 詳細およびその他の制御方法については、「 [Symopt\_FAIL\_重大\_エラー](symbol-options.md#symopt-fail-critical-errors)」を参照してください。

<span id="_______-secure______"></span><span id="_______-SECURE______"></span>**-セキュリティで保護された**   
[保護モード](secure-mode.md)をアクティブにします。

<span id="_______-ses______"></span><span id="_______-SES______"></span>**-ses**   
デバッガーがすべてのシンボルファイルの厳密な評価を実行し、疑わしいシンボルをすべて無視します。 詳細およびその他の制御方法については、「 [Symopt\_EXACT\_SYMBOLS](symbol-options.md#symopt-exact-symbols)」を参照してください。

<span id="_______-sflags_0xNumber"></span><span id="_______-sflags_0xnumber"></span><span id="_______-SFLAGS_0XNUMBER"></span> **-sflags 0x ** * * Number  
すべてのシンボルハンドラーオプションを一度に設定します。 *Number*は**0x**で始まる16進数の数字にする必要があります。 **0x**が指定されていない10進数を使用できますが、シンボルオプションはバイナリフラグであるため、16進数を使用することをお勧めします。 このオプションは、すべてのシンボルハンドラーの既定値をオーバーライドするため、注意して使用する必要があります。 詳細については、「[シンボルオプションの設定](symbol-options.md)」を参照してください。

<span id="_______-sicv______"></span><span id="_______-SICV______"></span>**-sicv**   
シンボルハンドラーが CV レコードを無視するようにします。 詳細およびこれを制御するその他の方法については、「 [Symopt\_IGNORE\_CVREC](symbol-options.md#symopt-ignore-cvrec)」を参照してください。

<span id="_______-sins______"></span><span id="_______-SINS______"></span>**-sins**   
デバッガーがシンボルパスと実行可能イメージパス環境変数を無視するようにします。 詳細については、「 [Symopt\_IGNORE\_NT\_SYMPATH](symbol-options.md#symopt-ignore-nt-sympath)」を参照してください。

<span id="_______-snc______"></span><span id="_______-SNC______"></span>**-snc**   
デバッガーが変換をオフC++にします。 詳細およびその他の制御方法については、「 [Symopt\_no\_CPP](symbol-options.md#symopt-no-cpp)」を参照してください。

<span id="_______-snul______"></span><span id="_______-SNUL______"></span>**-snul**   
非修飾名に対するシンボルの自動読み込みを無効にします。 詳細およびその他の制御方法については、「 [Symopt\_no\_非修飾\_読み込み](symbol-options.md#symopt-no-unqualified-loads)」を参照してください。

<span id="_______-srcpath_______SourcePath______"></span><span id="_______-srcpath_______sourcepath______"></span><span id="_______-SRCPATH_______SOURCEPATH______"></span>**-srcpath** *SourcePath*   
ソースファイルの検索パスを指定します。 複数のパスはセミコロン (**;**) で区切ります。 パスにスペースが含まれている場合は、引用符で囲む必要があります。 詳細について、およびこのパスを変更するその他の方法については、「[ソースパス](source-path.md)」を参照してください。

<span id="_______-sup______"></span><span id="_______-SUP______"></span>**-sup**   
シンボルを検索するたびに、シンボルハンドラーがパブリックシンボルテーブルを検索します。 詳細およびその他の制御方法については、「 [Symopt\_AUTO\_PUBLICS](symbol-options.md#symopt-auto-publics)」を参照してください。

<span id="_______-t________PrintErrorLevel______"></span><span id="_______-t________printerrorlevel______"></span><span id="_______-T________PRINTERRORLEVEL______"></span>**-t** *プリンター rorlevel*   
デバッガーにエラーメッセージを表示させるエラーレベルを指定します。 これは、0、1、2、または3に等しい10進数です。 値は次のように記述されます。

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
<td align="left"><p>エラーを表示しません。</p></td>
</tr>
<tr class="even">
<td align="left"><p>1</p></td>
<td align="left"><p>エラー</p></td>
<td align="left"><p>エラーレベルのデバッグイベントを表示します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>2</p></td>
<td align="left"><p>MINORERROR</p></td>
<td align="left"><p>MINORERROR およびエラーレベルのデバッグイベントを表示します。</p></td>
</tr>
<tr class="even">
<td align="left"><p>3</p></td>
<td align="left"><p>警告</p></td>
<td align="left"><p>警告、MINORERROR、およびエラーレベルのデバッグイベントを表示します。</p></td>
</tr>
</tbody>
</table>

 

このエラーレベルは、Microsoft Windows のチェックされたビルドでのみ意味があります。 既定値は 1 です。 チェックを行ったビルドは、Windows 10 バージョン1803より前の古いバージョンの Windows で使用できました。

<span id="_______-v______"></span><span id="_______-V______"></span>**-v**   
読み込み、遅延読み込み、およびアンロードの詳細メッセージを生成します。

<span id="_______-version______"></span><span id="_______-VERSION______"></span>**-バージョン**   
デバッガーのバージョン文字列を出力します。

<span id="_______-wake_______PID______"></span><span id="_______-wake_______pid______"></span><span id="_______-WAKE_______PID______"></span>**-wake** *PID*   
*PID*によってプロセス ID が指定されているユーザーモードデバッガーのスリープモードを終了します。 このコマンドは、スリープモード中にターゲットコンピューター上で発行する必要があります。 詳細については[、「カーネルデバッガーからのユーザーモードデバッガーの制御](controlling-the-user-mode-debugger-from-the-kernel-debugger.md)」を参照してください。

**-Wake**パラメーターを他のパラメーターと共に使用することはできません。 このコマンドは、実際には KD を開始しません。

<span id="_______-x______"></span><span id="_______-X______"></span>**-x**   
例外が発生した原因となったアプリケーションやモジュールではなく、例外が最初に発生したときにデバッガーを中断させます。 (最初の eb nt を除き、 **-b**と同じ**です。NtGlobalFlag 9; g**コマンド。)

<span id="_______-y_______SymbolPath______"></span><span id="_______-y_______symbolpath______"></span><span id="_______-Y_______SYMBOLPATH______"></span>**-y** *シンボルパス*   
シンボルの検索パスを指定します。 複数のパスはセミコロン (**;**) で区切ります。 パスにスペースが含まれている場合は、引用符で囲む必要があります。 詳細およびこのパスを変更するその他の方法については、「[シンボルパス](symbol-path.md)」を参照してください。

<span id="_______-z_______DumpFile______"></span><span id="_______-z_______dumpfile______"></span><span id="_______-Z_______DUMPFILE______"></span>**-z** *ダンプファイル*   
デバッグするクラッシュダンプファイルの名前を指定します。 パスとファイル名にスペースが含まれている場合、引用符で囲む必要があります。 複数**の**ダンプファイルを同時に開くことができます。その際、それぞれに異なる*ダンプファイル*値を指定します。 詳細については、「 [KD を使用したカーネルモードダンプファイルの分析](analyzing-a-kernel-mode-dump-file-with-kd.md)」を参照してください。

<span id="_______-zp_______PageFile______"></span><span id="_______-zp_______pagefile______"></span><span id="_______-ZP_______PAGEFILE______"></span>**-zp** *ページファイル*   
変更されたページファイルの名前を指定します。 これは、ダンプファイルをデバッグしていて、[**ページイン (Page In Memory)**](-pagein--page-in-memory-.md)コマンドを使用する場合に便利です。 標準の Windows ページファイルで **-zp**を使用することはできません。特別に変更されたページファイルのみ使用できます。

<span id="_______-_______"></span>**-?**   
コマンドラインのヘルプテキストを表示します。

KD は、ターゲットが実行されているプラットフォームを自動的に検出します。 KD コマンドラインでターゲットを指定する必要はありません。 古い構文 (名前*I386KD*または*IA64KD*を使用) は廃止されています。

 

 






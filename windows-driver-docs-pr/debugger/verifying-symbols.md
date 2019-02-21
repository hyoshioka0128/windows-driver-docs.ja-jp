---
title: シンボルを確認します。
description: シンボルを確認します。
ms.assetid: 61b4fcce-960b-4091-b575-4dd53c39cff2
keywords:
- シンボルを確認しています
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0ef6c6bcf0cb03a3924091da76a53914535320a8
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56528456"
---
# <a name="verifying-symbols"></a>シンボルを確認します。


## <span id="ddk_verifying_symbols_dbg"></span><span id="DDK_VERIFYING_SYMBOLS_DBG"></span>


シンボルに関する問題は、さまざまな方法で表示できます。 おそらくスタック トレースは、正しくない情報が表示され、スタック内の関数の名前を識別するために失敗します。 または、おそらくをモジュール、関数、変数、構造体、またはデータ型の名前を解釈できません。 デバッガー コマンド。

デバッガーがシンボルを正しく読み込んでしていないことが疑われる場合は、この問題を調査するために行えるいくつかの手順です。

まず、使用して、 [ **lm (読み込まれたモジュールの一覧)** ](lm--list-loaded-modules-.md)シンボル情報に読み込まれたモジュールの一覧を表示するコマンド。 このコマンドの最も便利な形式は次のです。

```dbgcmd
0:000> lml 
```

WinDbg を使用している場合、[デバッグ |モジュール](debug---modules.md)メニュー コマンドにもこの情報を確認することができます。

任意のメモまたはこれらの表示に表示される省略形に特に注意してください。 これらの解釈を参照してください。[シンボルの状態の省略形](symbol-status-abbreviations.md)します。

適切なシンボル ファイルが見つからない場合、まず最初にシンボル パスを確認することです。

```dbgcmd
0:000> .sympath
Current Symbol Path is: d:\MyInstallation\i386\symbols\retail
```

シンボル パスが間違っている場合、修正します。 カーネル デバッガー make を使用している場合ことを確認、ローカル %windir% では、シンボルのパスです。

使用してシンボルを再読み込みし、 [ **.reload (モジュールの再読み込み)** ](-reload--reload-module-.md)コマンド。

```dbgcmd
0:000> .reload ModuleName 
```

有効にする必要がある、シンボル パスが正しい場合は、*ノイズの多いモード*シンボル ファイルを表示できるように**dbghelp**を読み込んでいます。 次に、モジュールを再読み込みします。 参照してください[シンボル オプションを設定](symbol-options.md)ノイズの多いモードをアクティブ化する方法についてはします。

Microsoft Windows のシンボルの「ノイズ」再読み込みの例を次に示します。

```dbgcmd
kd> !sym noisy
kd> .reload nt
 1: Kernel Version 2081 MP Checked
 2: Kernel base = 0x80400000 PsLoadedModuleList = 0x80506fa0
 3: DBGHELP: FindExecutableImageEx-> Looking for D:\MyInstallation\i386\ntkrnlmp.exe...mismatched timestamp
 4: DBGHELP: No image file available for ntkrnlmp.exe
 5: DBGHELP: FindDebugInfoFileEx-> Looking for
 6: d:\MyInstallation\i386\symbols\retail\symbols\exe\ntkrnlmp.dbg... no file
 7: DBGHELP: FindDebugInfoFileEx-> Looking for
 8: d:\MyInstallation\i386\symbols\retail\symbols\exe\ntkrnlmp.pdb... no file
 9: DBGHELP: FindDebugInfoFileEx-> Looking for d:\MyInstallation\i386\symbols\retail\exe\ntkrnlmp.dbg... OK
10: DBGHELP: LocatePDB-> Looking for d:\MyInstallation\i386\symbols\retail\exe\ntkrnlmp.pdb... OK
11: *** WARNING: symbols checksum and timestamp is wrong 0x0036a4ea 0x00361a83 for ntkrnlmp.exe
```

シンボルのハンドラーは、まず、(行 3 および 4) をロードしようとしてがモジュールに一致するイメージを探します。 イメージ自体は常に、必要ありませんが、シンボル ハンドラーは多くの場合、失敗、正しくないものが存在する場合。 これらの行が、デバッガーにあるイメージを表示する**d:\\MyInstallation\\i386\\ntkrnlmp.exe**時刻、日付のタイムスタンプが一致しませんでしたが。 時刻と日付スタンプが一致していないため、検索が続行されます。 次に、デバッガーは、.dbg ファイルと読み込まれたイメージに一致する .pdb ファイルを検索します。 これらは、行 6 ~ 10 です。 11 行目は、シンボルが読み込まれた場合でも、イメージのタイムスタンプと一致しませんでしたを示します (これは、シンボルありました)。

シンボルの検索に致命的な障害が発生した場合は、フォームのメッセージを参照してくださいは。

```dbgcmd
ImgHlpFindDebugInfo(00000000, module.dll, c:\MyDir;c:\SomeDir, 0823345, 0) failed
```

これは、ファイル システムの障害、ネットワーク エラー、破損している .dbg ファイルなどの項目で発生する可能性があります。

### <a name="span-iddiagnosingsymbolloadingerrorsspanspan-iddiagnosingsymbolloadingerrorsspandiagnosing-symbol-loading-errors"></a><span id="diagnosing_symbol_loading_errors"></span><span id="DIAGNOSING_SYMBOL_LOADING_ERRORS"></span>シンボルの読み込みエラーを診断します。

ノイズの多いモードの場合、デバッガーはエラー コードを印刷ことがありますとシンボル ファイルを読み込むことができません。 .Dbg ファイルのエラー コードは、winerror.h で表示されます。 .Pdb のエラー コードが別のソースから取得され、最も一般的なエラーは、英語のプレーン テキストで印刷されます。

Winerror.h から .dbg ファイルのいくつかの一般的なエラー コードは次のとおりです。

<span id="0xB"></span><span id="0xb"></span><span id="0XB"></span>0 xb  
エラー\_不良\_形式

<span id="0x3"></span><span id="0X3"></span>0x3  
エラー\_パス\_いない\_が見つかりました

<span id="0x35"></span><span id="0X35"></span>0x35  
エラー\_不良\_NETPATH

ネットワーク エラーのため、シンボル ファイルを読み込むことができないことことができます。 エラーが発生した場合\_不良\_形式またはエラー\_不適切な\_NETPATH して、ネットワーク上の別のコンピューターからシンボルの読み込みは、ホスト コンピューターにシンボル ファイルをコピーしてください、およびシンボル パスのパスを配置します。 シンボルの再読み込みを再試行してください。

### <a name="span-idverifyingyoursearchpathandsymbolsspanspan-idverifyingyoursearchpathandsymbolsspanverifying-your-search-path-and-symbols"></a><span id="verifying_your_search_path_and_symbols"></span><span id="VERIFYING_YOUR_SEARCH_PATH_AND_SYMBOLS"></span>検索パスとシンボルを確認します。

"C:\\MyDir; c:\\SomeDir"シンボル パスを表します。 どこを探してくださいデバッグ情報ですか。

場合に、Windows のビルドなど、無料のデバッグ情報のバイナリが削除されて、まず、次の場所で .dbg ファイルを検索します。

```dbgcmd
c:\MyDir\symbols\exe\ntoskrnl.dbg
c:\SomeDir\symbols\exe\ntoskrnl.dbg
c:\MyDir\exe\ntoskrnl.dbg
c:\SomeDir\exe\ntoskrnl.dbg
c:\MyDir\ntoskrnl.dbg
c:\SomeDir\ntoskrnl.dbg
current-working-directory\ntoskrnl.dbg
```

次に、次の場所に .pdb ファイルを探します。

```dbgcmd
c:\MyDir\symbols\exe\ntoskrnl.pdb
c:\MyDir\exe\ntoskrnl.pdb
c:\MyDir\ntoskrnl.pdb
c:\SomeDir\symbols\exe\ntoskrnl.pdb
c:\SomeDir\exe\ntoskrnl.pdb
c:\SomeDir\ntoskrnl.pdb
current-working-directory\ntoskrnl.pdb
```

で .dbg ファイルの検索、.pdb 検索ではありませんが、MyDir と SomeDir ディレクトリから検索をインターリーブするので、デバッガーに注意してください。

Windows XP および Windows の以降のバージョンでは、すべての .dbg シンボル ファイルは使用しません。 参照してください[シンボルとシンボル ファイル](symbols-and-symbol-files.md)詳細についてはします。

### <a name="span-idmismatchedbuildsspanspan-idmismatchedbuildsspanmismatched-builds"></a><span id="mismatched_builds"></span><span id="MISMATCHED_BUILDS"></span>一致しないビルド

多くの場合、更新されるコンピューター上の障害のデバッグに最も一般的な問題の 1 つは、さまざまなビルドからシンボルが一致しません。 この問題の 3 つの一般的な原因は: 間違ったビルドのシンボルを指して、対応する文字を含めずに個別に構築されたバイナリを使用して、およびマルチプロセッサのコンピューターで、ユニプロセッサ ハードウェア アブストラクション レイヤー (HAL) とカーネル シンボルを使用します。 最初の 2 つは単に該当する、バイナリとシンボルの3 つ目は、hal の名前を変更して修正できます\*.dbg と hal.dbg を ntoskrnl.dbg ntkrnlmp.dbg します。

Windows のどのようなビルドがターゲット コンピューターにインストールされているを確認するを使用して、 [ **vertarget (ターゲット コンピューター バージョンの表示)** ](vertarget--show-target-computer-version-.md)コマンド。

```dbgcmd
kd> vertarget 
Windows XP Kernel Version 2505 UP Free x86 compatible
Built by: 2505.main.010626-1514
Kernel base = 0x804d0000 PsLoadedModuleList = 0x80548748
Debug session time: Mon Jul 02 14:41:11 2001
System Uptime: 0 days 0:04:53 
```

### <a name="span-idtestingthesymbolsspanspan-idtestingthesymbolsspantesting-the-symbols"></a><span id="testing_the_symbols"></span><span id="TESTING_THE_SYMBOLS"></span>シンボルのテスト

シンボルのテストは困難です。 デバッガーでのスタック トレースを確認してかどうか、デバッグ出力が正しく表示が含まれます。 1 つの例を次に示します。

```dbgcmd
kd> u videoprt!videoportfindadapter2
Loading symbols for 0xf2860000     videoprt.sys ->   videoprt.sys

VIDEOPRT!VideoPortFindAdapter2:
f2856f42 55               push    ebp
f2856f43 8bec             mov     ebp,esp
f2856f45 81ecb8010000     sub     esp,0x1b8
f2856f4b 8b4518           mov     eax,[ebp+0x18]
f2856f4e 53               push    ebx
f2856f4f 8365f400         and     dword ptr [ebp-0xc],0x
f2856f53 8065ff00         and     byte ptr [ebp-0x1],0x0
f2856f57 56               push    esi
```

**U**コマンド unassembles videoprt.sys で videoportfindadapter 文字列。 シンボルは、スタックの一般的なコマンドのようなために、デバッガーを正しく**プッシュ**と**mov**スタックに表示されます。 ほとんどの関数は、add、sub、またはプッシュ操作の基本ポインター (ebp) またはスタック ポインター (esp) を使用して、先頭します。

シンボルが正しく動作しない場合、通常は明らかです。 Glintmp.sys は、関数が横に表示されないために、この例でのシンボルがない**Glintmp**:

```dbgcmd
kd> kb
Loading symbols for 0xf28d0000     videoprt.sys ->   videoprt.sys
Loading symbols for 0xf9cdd000      glintmp.sys ->   glintmp.sys
*** ERROR: Symbols could not be loaded for glintmp.sys
ChildEBP RetAddr  Args to Child
f29bf1b0 8045b5fa 00000001 0000a100 00000030 ntoskrnl!RtlpBreakWithStatusInstruction
f29bf1b0 8044904e 00000001 0000a100 00000030 ntoskrnl!KeUpdateSystemTime+0x13e
f29bf234 f28d1955 f9b7d000 ffafb2dc f9b7d000 ntoskrnl!READ_REGISTER_ULONG+0x6
f29bf248 f9cde411 f9b7d000 f29bf2b0 f9ba0060 VIDEOPRT!VideoPortReadRegisterUlong+0x27
00000002 00000000 00000000 00000000 00000000 glintMP+0x1411 [No function listed.] 
```

このスタック トレースの正しくないビルドのシンボルを読み込みました。 方法はありません関数の一覧の最初の 2 つの呼び出しに注意してください。 このスタック トレースは、win32k.sys 描画の四角形の問題のようになります。

```dbgcmd
1: kd> 
1: kd> kb                      [Local        9:50 AM]
Loading symbols for 0xf22b0000       agpcpq.sys ->   agpcpq.sys
*** WARNING: symbols checksum is wrong 0x0000735a 0x00000000 for agpcpq.sys
*** ERROR: Symbols could not be loaded for agpcpq.sys
Loading symbols for 0xa0000000       win32k.sys ->   win32k.sys
*** WARNING: symbols checksum is wrong 0x00191a41 0x001995a9 for win32k.sys
ChildEBP RetAddr  Args to Child
be682b18 f22b372b 82707128 f21c1ffc 826a70f8 agpCPQ+0x125b [No function listed.]
be682b4c a0140dd4 826a72f0 e11410a8 a0139605 agpCPQ+0x372b [No function listed.]
be682b80 a00f5646 e1145100 e1cee560 e1cee560 win32k!vPatCpyRect1_6x6+0x20b
00000001 00000000 00000000 00000000 00000000 win32k!RemoteRedrawRectangle+0x32 
```

適切なスタック トレースを次に示します。 問題が AGP440.sys 本当にします。 スタック トレースに表示される最初の項目が問題なのでは、通常は。 Win32k.sys 四角形のエラーがなくなったことに注意してください。

```dbgcmd
1: kd> kb                      [Local        9:49 AM]
ChildEBP RetAddr  Args to Child
be682b18 f22b372b 82707128 f21c1ffc 826a70f8 agpCPQ!AgpReleaseMemory+0x88
be682b30 f20a385c 82703638 e183ec68 00000000 agpCPQ!AgpInterfaceReleaseMemory+0x8b
be682b4c a0140dd4 826a72f0 e11410a8 a0139605 VIDEOPRT!AgpReleasePhysical+0x44
be682b58 a0139605 e1cee560 e11410a8 a00e5f0a win32k!OsAGPFree+0x14
be682b64 a00e5f0a e1cee560 e11410a8 e1cee560 win32k!AGPFree+0xd
be682b80 a00f5646 e1145100 e1cee560 e1cee560 win32k!HeapVidMemFini+0x49
be682b9c a00f5c20 e1cee008 e1cee008 be682c0c win32k!vDdDisableDriver+0x3a
be682bac a00da510 e1cee008 00000000 be682c0c win32k!vDdDisableDirectDraw+0x2d
be682bc4 a00da787 00000000 e1843df8 e1843de8 win32k!PDEVOBJ__vDisableSurface+0x27
be682bec a00d59fb 00000000 e1843de8 00000000 win32k!PDEVOBJ__vUnreferencePdev+0x204
be682c04 a00d7421 e1cee008 82566a98 00000001 win32k!DrvDestroyMDEV+0x30
be682ce0 a00a9e7f e1843e10 e184a008 00000000 win32k!DrvChangeDisplaySettings+0x8b3
be682d20 a008b543 00000000 00000000 00000000 win32k!xxxUserChangeDisplaySettings+0x106
be682d48 8045d119 00000000 00000000 00000000 win32k!NtUserChangeDisplaySettings+0x48
be682d48 77e63660 00000000 00000000 00000000 ntkrnlmp!KiSystemService+0xc9 
```

### <a name="span-idusefulcommandsandextensionsspanspan-idusefulcommandsandextensionsspanuseful-commands-and-extensions"></a><span id="useful_commands_and_extensions"></span><span id="USEFUL_COMMANDS_AND_EXTENSIONS"></span>便利なコマンドと拡張機能

次のコマンドと拡張機能は、シンボルに関する問題を追跡に役立ちます。

<span id="lm__List_Loaded_Modules_"></span><span id="lm__list_loaded_modules_"></span><span id="LM__LIST_LOADED_MODULES_"></span>[**lm (読み込まれたモジュールを一覧表示)**](lm--list-loaded-modules-.md)  
すべてのモジュールの一覧を示し、これらのモジュールですべてのシンボルの読み込み中です。

<span id="_dh_image-header-base"></span><span id="_DH_IMAGE-HEADER-BASE"></span>[**!dh image-header-base**](-dh.md)  
開始位置として、読み込まれたイメージのヘッダー情報を表示します。*イメージ ベース ヘッダー*します。

<span id=".RELOAD__N"></span>[**.reload/n**](-reload--reload-module-.md)  
カーネルのすべてのシンボルを再読み込みします。

<span id=".reload__image-name_"></span><span id=".RELOAD__IMAGE-NAME_"></span>[**.reload \[image-name\]**](-reload--reload-module-.md)  
(CDB または WinDbg のみ)イメージのシンボルを再読み込み*イメージ名*します。 ない場合は*イメージ名*指定すると、すべてのイメージのシンボルを再読み込みします。 (これはシンボルをシンボル パスが変更された後に再読み込みするために必要)

<span id="_sym_noisy"></span><span id="_SYM_NOISY"></span>[**! ノイズの多い sym**](-sym.md)  
シンボルの読み込みの詳細モードをオンにします。 モジュールの読み込みに関する情報を取得するために使用できます。 参照してください[シンボル オプションを設定](symbol-options.md)詳細についてはします。

<span id=".sympath__new-symbol-path_"></span><span id=".SYMPATH__NEW-SYMBOL-PATH_"></span>[**.sympath \[new-symbol-path\]**](-sympath--set-symbol-path-.md)  
現在のシンボル パスを表示します。 または、新しいシンボルのパスを設定します。 参照してください[シンボル パス](symbol-path.md)詳細についてはします。

カーネルのシンボルが正しいこと、完全なスタックが届かない場合は、次のコマンドでも利用できます。

<span id="X___"></span><span id="x___"></span>[**X \*!**](x--examine-symbols-.md)  
これには、シンボルが読み込まれている現在のモジュールが一覧表示します。 これは、カーネルのシンボルが正しい場合に便利です。

<span id=".RELOAD__USER"></span>[**.reload/user**](-reload--reload-module-.md)  
これについては、すべてのユーザー モード シンボルを再読み込みを試みます。 これは、別のプロセスで発生した後で、1 つのプロセスの実行中にシンボルが読み込まれた場合、カーネル デバッグを実行して、中断中に必要です。 この場合、このコマンドを実行しない限り、新しいプロセスからユーザー モードのシンボルは読み込まれません。

<span id="X_wdmaud__start_"></span><span id="x_wdmaud__start_"></span><span id="X_WDMAUD__START_"></span>[**X wdmaud!\*開始\\***](x--examine-symbols-.md)  
これでシンボルのみが一覧表示、 **wdmaud**名前に"start"文字列を含むモジュール。 これは、すべてのシンボルの再読み込みを強制的利点**wdmaud**、のみ"start"を持つでそれらに表示されます。 (つまり、短い一覧についてがいくつかの確認、読み込みが行われることがありますがいくつかの記号には、"start"では常にであるため)。

シンボルを検証するための他の 1 つの便利な方法では、コードを unassembling です。 ほとんどの関数は、add、sub、またはプッシュ操作が、いずれかの基本ポインターを使用して、先頭 (**ebp**) またはスタック ポインター (**esp**または**sp**)。 Unassembling を再試行してください ([**U 関数**](u--unassemble-.md))、シンボルを確認する (オフセット 0) から、スタック上の関数の一部です。

### <a name="span-idnetworkandportproblemsspanspan-idnetworkandportproblemsspannetwork-and-port-problems"></a><span id="network_and_port_problems"></span><span id="NETWORK_AND_PORT_PROBLEMS"></span>ネットワークとポートの問題

シンボル ファイルとは、デバッガーに接続中に問題が発生します。 問題が発生した場合に留意する点を次に示します。

-   COM ポートをテスト システムでデバッグ ケーブルが接続を決定します。

-   テスト システムの boot.ini の設定を確認します。 探して、 **/debug**スイッチし、ボー レートおよび COM ポートの設定を確認します。

-   ネットワークの問題は、デバッグ シンボル ファイルに、ネットワークを介してアクセスする場合に干渉ことができます。

-   シンボルのツリーの適切なディレクトリに、区切られていない場合、.dll .sys ファイルと同じ名前 (たとえば − mga64.sys および mga64.dll) は、デバッガーを混乱します。

-   カーネル デバッガーは常になどのビルドのシンボル ファイルにプライベート シンボル ファイルを置き換えます。 倍精度浮動小数点シンボル パスを確認し、操作を行います、**.reload * * * FileName*記号を不適切に動作します。 [ **! Dll** ](-dlls.md)コマンドは、便利です。

### <a name="span-idquestionsandmisconceptionsspanspan-idquestionsandmisconceptionsspanquestions-and-misconceptions"></a><span id="questions_and_misconceptions"></span><span id="QUESTIONS_AND_MISCONCEPTIONS"></span>疑問と誤解

**Q:** シンボル、正常に読み込みましたが、スタックが間違っているようです。 別のデバッガーとは

**A:** 必須ではありません。 問題の最も可能性の高い原因は、正しくない記号が得られたらです。 か有効なシンボルが読み込まれているかどうかを判断するには、このセクションで説明する手順を実行します。 一部の機能は動作しているためには有効なシンボルがあることを前提としてはいません。 たとえば、非常にうまくことができますを実行する**dd nt! ntbuildnumber**または**u nt!KeInitializeProcess**と正しくない記号を使用します。 上記の手順を使用していることを確認します。

**Q:** デバッガーは正しくない記号ありますか。

**A:** さあ何とも言えません。 多くの場合、いいことと厳密に一致しない記号を使用します。 たとえば、以前の Windows ビルドからシンボルを通常は特定の場合、作業しますが、これは、機能と、されませんが、ルールはありません。

**Q:** カーネル デバッガーで停止したいるし、ユーザー モード プロセス用のシンボルを表示します。 実行できるでしょうか。

**A:** ほとんどの場合。 このシナリオのサポートは、カーネル デバッガーが、各プロセスのモジュールの読み込みを追跡するために十分な情報を維持しませんが、妥当な回避策があるため、最低レベルです。 ユーザー モードのモジュールのシンボルを読み込むには、実行、 **.reload-ユーザー**コマンド。 現在のコンテキストのユーザー モードのモジュールが読み込まれます。

**Q:** 次のメッセージは何を意味しますか。

`*** WARNING: symbols checksum and timestamp is wrong 0x0036d6bf 0x0036ab55 for ntkrnlmp.exe`

**A:** Ntkrnlmp.exe のシンボルが正しくないを意味します。

 

 






---
title: 事後デバッグを有効にする
description: このトピックでは、事後検証のデバッグを有効にする方法をについて説明します
ms.assetid: ae116b60-fed2-4e1d-98a8-9fe83f460c50
keywords: デバッグします。 デバッグ、Windbg、事後検証のデバッグ、ジャストイン タイムのデバッグ、JIT デバッグ、AeDebug レジストリ キー
ms.date: 09/17/2018
ms.localizationpriority: medium
ms.openlocfilehash: cb3b9dfa53ae3ef7a615f1586a1ed92ba0a585be
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67361386"
---
# <a name="enabling-postmortem-debugging"></a>事後デバッグを有効にする


## <a name="span-idddkenablingpostmortemdebuggingdbgspanspan-idddkenablingpostmortemdebuggingdbgspanuser-mode-exception-handling"></a><span id="ddk_enabling_postmortem_debugging_dbg"></span><span id="DDK_ENABLING_POSTMORTEM_DEBUGGING_DBG"></span>ユーザー モード例外処理


**例外とブレークポイント**

アプリケーションの最も一般的なエラーは、例外と呼ばれます。 アクセス違反、0 による除算のエラー、数値オーバーフロー、CLR の例外、およびその他のさまざまなエラーが含まれます。 アプリケーションでは、ブレークポイントの割り込みをこともあります。 これらは、Windows が (たとえば、必要なモジュールを読み込むことができません)、アプリケーションを実行できない場合、またはブレークポイントが発生した場合に発生します。 ブレークポイントをデバッガーでコードに挿入されるかなどの関数によって呼び出された[ **DebugBreak**](https://docs.microsoft.com/windows/desktop/api/debugapi/nf-debugapi-debugbreak)します。

**例外ハンドラーの優先順位**

構成値とデバッガーをアクティブに基づき、Windows は、さまざまな方法でユーザー モードのエラーを処理します。 次の順序は、ユーザー モードのエラー処理に使用される優先順位を示します。

1.  ユーザー モード デバッガーは現在、エラーが発生したプロセスにアタッチされて、すべてのエラーがこのデバッガーを中断するターゲットになります。

    ユーザー モード デバッガーがアタッチされている限り、その他のエラー処理メソッドは使用されません - 場合でも、 [ **gn (Go で処理されない例外)** ](gn--gn--go-with-exception-not-handled-.md)コマンドを使用します。

2.  ユーザー モード デバッガーがアタッチされていないと、実行中のコードは、独自の例外処理ルーチンが場合 (たとえば、 **- お試しくださいを除く**)、この例外処理ルーチンはエラーを処理しようとしています。

3.  ユーザー モードのデバッガーがアタッチされていない Windows が開いているカーネル デバッグ接続し、エラーは、ブレークポイントの割り込み、Windows は、カーネル デバッガーにお問い合わせくださいしようとします。

    Windows のブート プロセス中には、カーネル デバッグ接続を開く必要があります。 ユーザー モードの割り込みのカーネル デバッガーに侵入を防止する場合で KDbgCtrl ユーティリティを使用することができます、 **-du**パラメーター。 カーネル デバッグ接続を構成する方法と KDbgCtrl を使用する方法の詳細については、次を参照してください。[を取得する設定をデバッグ用](getting-set-up-for-debugging.md)します。

    カーネル デバッガーで使用することができます[ **(移動により例外を処理) gh** ](gh--go-with-exception-handled-.md)エラーを無視し、ターゲットの実行を継続します。 使用することができます[ **gn (Go で処理されない例外)** ](gn--gn--go-with-exception-not-handled-.md)をカーネル デバッガーをバイパスし、手順 4 に進みます。

4.  手順 1、2、および 3 の条件が該当しない場合、Windows は AeDebug レジストリ値で構成されているデバッグ ツール アクティブ化されます。 任意のプログラムを選択できます事前に、ツールとしてこのような状況で使用します。 選択したプログラムと呼ばれます、*事後デバッガー*します。

5.  手順 1、2、および 3 の条件は適用されない場合に、事後分析のデバッガーが登録されていない場合は、Windows エラー報告 (WER) は、メッセージが表示され、利用できる場合は、ソリューションを提供します。 WER には、適切な値は レジストリで設定されているかどうか、メモリ ダンプ ファイルも書き込みます。 詳細については、次を参照してください。[を使用して WER](https://go.microsoft.com/fwlink/p?LinkID=257799)と[ユーザー モード ダンプを収集](https://go.microsoft.com/fwlink/p?LinkID=257798)します。

**DebugBreak 関数**

事後分析のデバッガーがインストールされている場合することが意図的にデバッガーに割り込むユーザー モード アプリケーションから呼び出すことによって、 **DebugBreak**関数。

## <a name="span-idspecifyingapostmortemdebuggerspanspan-idspecifyingapostmortemdebuggerspanspan-idspecifyingapostmortemdebuggerspanspecifying-a-postmortem-debugger"></a><span id="Specifying_a_Postmortem_Debugger"></span><span id="specifying_a_postmortem_debugger"></span><span id="SPECIFYING_A_POSTMORTEM_DEBUGGER"></span>事後分析のデバッガーを指定します。


このセクションでは、事後デバッガーとして WinDbg などのツールを構成する方法について説明します。 構成されると、事後分析のデバッガーは自動的に開始たびに、アプリケーションがクラッシュします。

**事後のデバッガーのレジストリ キーを投稿します。**

Windows エラー報告 (WER) は、AeDebug レジストリ キーの設定値を使用して事後分析のデバッガー プロセスを作成します。

**HKLM**\\**ソフトウェア**\\**Microsoft**\\**Windows NT** \\ **CurrentVersion**\\**AeDebug**

関心のある 2 つのプライマリのレジストリ値がある*デバッガー*と*自動*します。*デバッガー*レジストリ値は、事後分析のデバッガーのコマンドラインを指定します。 *自動*事後分析のデバッガーは自動的に開始されている場合、または最初に確認のメッセージ ボックスが表示される場合、レジストリ値を指定します。

<span id="Debugger__REG_SZ_"></span><span id="debugger__reg_sz_"></span><span id="DEBUGGER__REG_SZ_"></span>**デバッガー (REG\_SZ)**  

この REG\_SZ 値は、事後検証のデバッグを処理するデバッガーを指定します。

デバッガーは、既定のパス内にあるディレクトリにある場合を除き、デバッガーへの完全パスを一覧表示する必要があります。

コマンドラインは、3 つのパラメーターを含む printf スタイルの呼び出しを使用して、デバッガーの文字列から生成されます。 順序が固定されていますが、使用可能なパラメーターの一部またはすべてを使用する必要はありません。

DWORD (% %ld) のターゲット プロセスのプロセス ID。

DWORD (% %ld) のイベント処理の事後分析のデバッガー プロセスに重複しています。 事後分析のデバッガーでは、イベントを通知、WER は事後にデバッガーを終了を待機することがなくターゲット プロセスが続行されます。 イベントは、問題が解決されているかどうかのみ通知する必要があります。 イベントを通知せずに、事後分析のデバッガーを終了、WER は、対象プロセスに関する情報のコレクションを続行します。

void\* (%p)、JIT のアドレス\_デバッグ\_ターゲット プロセスのアドレス空間に割り当てられている情報の構造体。 構造体には、追加の例外情報とコンテキストが含まれています。

<span id="Auto__REG_SZ_"></span><span id="auto__reg_sz_"></span><span id="AUTO__REG_SZ_"></span>**自動 (REG\_SZ)** この REG\_SZ 値は、いずれかでは常に**0**または**1**します。

場合**自動**に設定されている**0**、事後分析のデバッグ プロセスが開始される前に確認のメッセージ ボックスが表示されます。

場合**自動**に設定されている**1**、事後分析のデバッガーがすぐに作成します。

レジストリを手動で編集する場合は、レジストリの不適切な変更を起動する Windows 認めないため、慎重を実行します。

**コマンドラインの使用例**

多くの事後分析デバッガー-p を含むコマンドラインの使用し、-e スイッチをパラメーターを示すためには、PID とイベント (それぞれ)。 たとえば、WinDbg を使用してインストールする`windbg.exe -I`次の値を作成します。

```console
Debugger = "<Path>\WinDbg -p %ld -e %ld -g"
Auto = 1
```

WER %%ld% %ld %p パラメーターの使用方法に柔軟性があります。 次に例を示します。 WER パラメーター間の周り、またはスイッチを指定する必要はありません。 たとえば、インストール[Windows Sysinternals ProcDump](https://technet.microsoft.com/sysinternals/dd996900.aspx)を使用して`procdump.exe -i`%ld%%ld %p パラメーター WER % 間スイッチなしで、次の値を作成します。

```console
Debugger = "<Path>\procdump.exe" -accepteula -j "c:\Dumps" %ld %ld %p
Auto = 1
```

**32 ビットおよび 64 ビット デバッガー**

デバッガーで、64 ビット プラットフォーム上 (REG\_SZ) と 自動 (REG\_SZ) レジストリ値は 64 ビットおよび 32 ビット アプリケーション用に個別に定義します。 Windows (WOW) のキーに追加の Windows を使用して、32 ビット アプリケーションのデバッグ事後値を格納します。

**HKLM**\\**ソフトウェア**\\**Wow6432Node**\\**Microsoft** \\ **Windows NT**\\**CurrentVersion**\\**AeDebug**

64 ビット プラットフォームでは、32 ビット プロセスと 64 ビット プロセス用の 64 ビット デバッガーの 32 ビットの事後デバッガーを使用します。 これにより、64 ビット デバッガーが 32 ビット プロセスで、32 ビット スレッドではなく、WOW64 のスレッドに重点を置くことがなくなります。

インストールのコマンドを 2 回実行は、このツールを Windows のデバッグの事後分析デバッガーなど、多くの事後分析デバッガーにもう 1 回、x86 バージョン、もう 1 回、x64 バージョン。 たとえば、対話型の事後分析デバッガーとして WinDbg を使用する、`windbg.exe -I`コマンドが 2 回、1 回実行する各バージョン。

64 ビット インストール:

```console
C:\Program Files (x86)\Windows Kits\10\Debuggers\x64\windbg.exe –I
```

これは、これらの値で、レジストリ キーを更新します。

```reg
HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows NT\CurrentVersion\AeDebug
Debugger = "C:\Program Files (x86)\Windows Kits\10\Debuggers\x64\windbg.exe" -p %ld -e %ld –g
```

32 ビット インストール:

```console
C:\Program Files (x86)\Windows Kits\10\Debuggers\x86\windbg.exe –I
```

これは、これらの値で、レジストリ キーを更新します。

```reg
HKEY_LOCAL_MACHINE\SOFTWARE\WOW6432Node\Microsoft\Windows NT\CurrentVersion\AeDebug
Debugger = "C:\Program Files (x86)\Windows Kits\10\Debuggers\x86\windbg.exe" -p %ld -e %ld –g
```

## <a name="span-idconfiguringspanspan-idconfiguringspanspan-idconfiguringspanconfiguring-post-mortem-debuggers"></a><span id="Configuring"></span><span id="configuring"></span><span id="CONFIGURING"></span>投稿の事後デバッガーを構成します。


### <a name="span-iddebuggingtoolsforwindowsspanspan-iddebuggingtoolsforwindowsspanspan-iddebuggingtoolsforwindowsspandebugging-tools-for-windows"></a><span id="Debugging_Tools_for_Windows"></span><span id="debugging_tools_for_windows"></span><span id="DEBUGGING_TOOLS_FOR_WINDOWS"></span>Windows 用デバッグ ツール

デバッグ ツールの Windows のデバッガー、事後デバッガーとして設定されているすべてのサポート。 インストール コマンドでは、対話的にデバッグするプロセスの予定です。

**WinDbg**

WinDbg の事後分析のデバッガーを設定するには、実行`windbg -I`します。 (、`I`大文字で入力する必要があります)。このコマンドは、使用後に成功または失敗のメッセージが表示されます。 32 と 64 ビット アプリケーションの両方を使用するには、両方の 64 と 32 のデバッガーのコマンドを実行します。

```console
C:\Program Files (x86)\Windows Kits\10\Debuggers\x64\windbg.exe –I
C:\Program Files (x86)\Windows Kits\10\Debuggers\x86\windbg.exe –I
```

AeDebug レジストリ エントリがされる方法は、この構成された`windbg -I`を実行します。

```console
Debugger = "<Path>\WinDbg -p %ld -e %ld -g"
Auto = 1
```

例では、 *&lt;パス&gt;* デバッガーが配置されているディレクトリです。

-P と-e パラメーターは、プロセス ID とイベントを前に説明したように渡します。

**-G** WinDbg を g (移動) コマンドを渡し、現在の命令の実行を継続します。

**注**   g (移動) コマンドを渡すことの重要な問題があります。 この方法で問題があること例外常に、繰り返されない、通常、一時的な状態コードが再起動したときに存在しなくなったため。 この問題の詳細については、次を参照してください。 [ **.jdinfo (使用 JIT\_デバッグ\_情報)** ](-jdinfo--use-jit-debug-info-.md)します。

この問題を回避するには、.jdinfo または .dump/j を使用します。 このアプローチを使用すると、デバッガーは、関心のあるコードのエラーのコンテキスト内でいます。 詳細については、次を参照してください。[ジャスト イン タイム (JIT) デバッグ](#jit)このトピックで後述します。

 

**CDB**

事後分析のデバッガーを CDB に設定するには、実行**cdb iae** (をインストールする AeDebug) または**cdb iaec** *KeyString* (コマンドを使用してインストール AeDebug)。

```console
C:\Program Files (x86)\Windows Kits\10\Debuggers\x64\cdb.exe -iae
C:\Program Files (x86)\Windows Kits\10\Debuggers\x86\cdb.exe -iae
```

ときに、 **- iaec**パラメーターを使用すると、 *KeyString*事後分析のデバッガーを起動するために使用するコマンドラインの末尾に追加する文字列を指定します。 場合*KeyString*スペースが含まれることは、引用符で囲む必要があります。

```console
C:\Program Files (x86)\Windows Kits\10\Debuggers\x64\cdb.exe -iaec [KeyString]
C:\Program Files (x86)\Windows Kits\10\Debuggers\x86\cdb.exe -iaec [KeyString]
```

このコマンドでは、失敗した場合、成功した場合は nothing とエラー メッセージを表示します。

**NTSD**

NTSD の事後分析のデバッガーを設定するには、実行**ntsd iae** (をインストールする AeDebug) または**ntsd iaec** *KeyString* (コマンドを使用してインストール AeDebug)。

```console
C:\Program Files (x86)\Windows Kits\10\Debuggers\x64\ntsd.exe -iae
C:\Program Files (x86)\Windows Kits\10\Debuggers\x86\ntsd.exe -iae
```

ときに、 **- iaec**パラメーターを使用すると、 *KeyString*事後分析のデバッガーを起動するために使用するコマンドラインの末尾に追加する文字列を指定します。 場合*KeyString*スペースが含まれることは、引用符で囲む必要があります。

```console
C:\Program Files (x86)\Windows Kits\10\Debuggers\x64\ntsd.exe -iaec [KeyString]
C:\Program Files (x86)\Windows Kits\10\Debuggers\x86\ntsd.exe -iaec [KeyString]
```

このコマンドは、エラー発生時に新しいコンソール ウィンドウに成功した場合は nothing とエラーを表示します。

**注**  を指定する - iaec スイッチを使用しないでください-p % %ld-e % %ld-g パラメーターは、常に、事後分析のデバッガーのコマンドラインの先頭に表示される、ため server パラメーターで最初に表示しない限り、サーバーは動作しないため、-コマンドライン。 このパラメーターを含む事後デバッガーをインストールするには、レジストリを手動で編集する必要があります。

 

### <a name="span-idvisualstudiojitdebuggerspanspan-idvisualstudiojitdebuggerspanspan-idvisualstudiojitdebuggerspanvisual-studio-jit-debugger"></a><span id="Visual_Studio_JIT_Debugger"></span><span id="visual_studio_jit_debugger"></span><span id="VISUAL_STUDIO_JIT_DEBUGGER"></span>Visual Studio の JIT デバッガー

Visual Studio がインストールされている場合、vsjitdebugger.exe は post の事後デバッガーとして登録されます。 Visual Studio の JIT デバッガーは、対話的にデバッグするプロセスの予定です。

```console
Debugger = "C:\WINDOWS\system32\vsjitdebugger.exe" -p %ld -e %ld
```

Visual Studio が更新または再インストールされている、このエントリは再書き込み、任意の代替を上書きする値のセット。

### <a name="span-idwindowsysinternalsprocdumpspanspan-idwindowsysinternalsprocdumpspanspan-idwindowsysinternalsprocdumpspanwindow-sysinternals-procdump"></a><span id="Window_Sysinternals_ProcDump"></span><span id="window_sysinternals_procdump"></span><span id="WINDOW_SYSINTERNALS_PROCDUMP"></span>ウィンドウの Sysinternals ProcDump

Windows Sysinternals ProcDump ユーティリティは、事後分析のダンプをキャプチャにも使用できます。 使用して、ProcDump のダウンロードの詳細については、次を参照してください。 [ProcDump](https://technet.microsoft.com/sysinternals/dd996900.aspx) technet。

ように、 [ **.dump** ](-dump--create-dump-file-.md) WinDbg コマンド、ProcDump にクラッシュ ダンプをキャプチャすることは非対話的にします。 キャプチャは、Windows システムの任意のセッションで発生します。

ProcDump が終了するは、エラーが発生したプロセスが終了し、ダンプ ファイルのキャプチャが完了すると、WER し、障害が報告されます。

使用`procdump -i`procdump と事後のデバッグ、32 ビットおよび 64 ビット両方の ProcDump をアンインストールするをインストールします。

```console
<Path>\procdump.exe -i
```

インストールとアンインストール コマンドの出力に成功した場合、およびエラー発生時のエラーでレジストリの値を変更します。

レジストリで ProcDump コマンド ライン オプションに設定されます。

```console
Debugger = <Path>\ProcDump.exe -accepteula -j "<DumpFolder>" %ld %ld %p
```

ProcDump は 3 つすべてのパラメーター - PID、イベント、および JIT を使用して\_デバッグ\_情報。 詳細については、JIT\_デバッグ\_INFO パラメーターを参照してください[ジャスト イン タイム (JIT) デバッグ](#jit)以下。

ダンプのサイズ、サイズのオプション セット MiniPlus せずミニ (プロセス/スレッド/ハンドル/モジュール/アドレス空間) に既定値をキャプチャする (さらにメモリ最適化ミニ\_プライベート ページ) -mp セット、または完全な (すべてメモリ -".dump/mA"に相当) を使って ma 設定。

十分な空き容量、完全なシステムの場合 (-ma) キャプチャをお勧めします。

使用して-i ma は、すべてのメモリのキャプチャを指定するオプションします。 必要に応じて、ダンプ ファイルのパスを指定します。

```console
<Path>\procdump.exe -ma -i c:\Dumps
```

システムの制限付きのドライブ容量、MiniPlus、(-mp) キャプチャをお勧めします。

```console
<Path>\procdump.exe -mp -i c:\Dumps
```

ダンプ ファイルの保存先フォルダーは省略可能です。 既定では、現在のフォルダーです。 フォルダーと等しいまたはそれ以上の c: の用途は、ACL を使用してセキュリティで保護する必要があります\\Windows\\Temp します。フォルダーに関連するセキュリティを管理する方法の詳細については、次を参照してください。[セキュリティ事後デバッグ中に](security-during-postmortem-debugging.md)します。

事後分析のデバッガーと ProcDump をアンインストールして、以前の設定の復元、-u (アンインストール) オプションを使用します。

```console
<Path>\procdump.exe -u
```

インストールと 64 ビット プラットフォーム上で 64 ビットおよび 32 ビット値の両方のコマンド セットをアンインストールします。

ProcDump は、"パック"されるアプリケーションの - として 32 ビットおよび 64 ビット バージョンの両方を含む実行可能ファイル、32 ビットと 64 ビットの両方に同じ実行可能ファイルを使用します。 ProcDump を実行すると自動的に切り替わりますバージョン、ターゲット プロセスが実行されているバージョンに一致しない場合。

## <a name="span-idjitspanspan-idjitspan-just-in-time-jit-debugging"></a><span id="JIT"></span><span id="jit"></span> ジャスト イン タイム (JIT) デバッグ


**エラーが発生したアプリケーションにコンテキストの設定**

前述のようは、非常に JIT を使用して、クラッシュの原因となった例外にコンテキストを設定することが望ましい\_デバッグ\_INFO パラメーター。 詳細については、次を参照してください。 [ **.jdinfo (使用 JIT\_デバッグ\_情報)** ](-jdinfo--use-jit-debug-info-.md)します。

**Windows 用デバッグ ツール**

この例は、レジストリを編集して、最初のコマンドを実行する方法を示します (-c)、.jdinfo を使用する&lt;アドレス&gt;コマンドを追加の例外情報を表示して、コンテキスト (方法と似ています例外の場所を変更します。ecxr が使用されるコンテキスト例外レコードに設定)。

```console
Debugger = "<Path>\windbg.exe -p %ld -e %ld -c ".jdinfo 0x%p"
Auto = 1
```

%P パラメーターは、JIT のアドレス\_デバッグ\_ターゲット プロセスのアドレス空間内の情報の構造体。 %P パラメーターが 16 進数値として解釈されるように事前 0 x が付加されます。 詳細については、次を参照してください。 [ **.jdinfo (使用 JIT\_デバッグ\_情報)** ](-jdinfo--use-jit-debug-info-.md)します。

さまざまな 32 ビットおよび 64 ビットのアプリをデバッグするには、両方、32 ビットおよび 64 ビットのレジストリ キー (前述)、64 ビットおよび 32 ビット WinDbg.exe の場所に適切なパスの設定を構成します。

**.Dump を使用してダンプ ファイルを作成します。**

ファイル、障害が発生するたびににはダンプをキャプチャするには、JIT が含まれています\_デバッグ\_情報のデータを使用して、.dump/j&lt;アドレス&gt;します。

```console
<Path>\windbg.exe -p %ld -e %ld -c ".dump /j %p /u <DumpPath>\AeDebug.dmp; qd"
```

/U オプションを使用すると、複数のダンプ ファイルが自動的に作成を許可するのに一意のファイル名を生成します。 詳細については、オプションは、「 [ **.dump (ダンプ ファイルの作成)** ](-dump--create-dump-file-.md)します。

作成されたダンプの必要があります、JITDEBUG\_既定例外コンテキストとして格納される情報のデータ。 .Jdinfo を使用して、例外情報を表示し、コンテキストを設定するのにのではなく、例外レコードとコンテキストを設定するのに .ecxr を表示するのに .exr-1 を使用します。 詳細については、次を参照してください。 [ **.exr (例外レコードの表示)** ](-exr--display-exception-record-.md)と[ **.ecxr (例外コンテキスト レコードの表示)** ](-ecxr--display-exception-context-record-.md)します。

**Windows エラー報告 - q/qd**

方法は、Windows エラー報告、エラーが報告かどうか、デバッグ セッションが終了を決定します。

デバッガーの終了する前に qd を使用して、デバッグ セッションをデタッチすると、WER は、エラーを報告します。

Q (または接続を取り外さず、デバッガーが閉じているかどうか) を使用して、デバッグ セッションを終了すると、WER は、エラーを報告しません。

追加 *; q*または *; qd*目的の動作を呼び出すコマンド文字列の末尾にします。

たとえば、CDB がダンプをキャプチャした後に、エラーを報告して WER を許可するのには、このコマンド文字列を構成します。

```console
<Path>\cdb.exe -p %ld -e %ld -c ".dump /j 0x%p /u c:\Dumps\AeDebug.dmp; qd"
```

この例では、WinDbg はダンプをキャプチャした後に、エラーを報告して WER が可能です。

```console
<Path>\windbg.exe -p %ld -e %ld -c ".dump /j %p /u <DumpPath>\AeDebug.dmp; qd""
```

## <a name="span-idsecurityvulnerabilitiesspanspan-idsecurityvulnerabilitiesspansecurity-vulnerabilities"></a><span id="security_vulnerabilities"></span><span id="SECURITY_VULNERABILITIES"></span>セキュリティの脆弱性


他のユーザーと共有しているコンピューター上の事後分析デバッグの有効化を検討している場合は、次を参照してください。[セキュリティ事後デバッグ中に](security-during-postmortem-debugging.md)します。

 

 






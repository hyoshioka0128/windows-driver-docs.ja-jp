---
title: 事後デバッグを有効にする
description: このトピックでは、事後分析のデバッグを有効にする方法について説明します
ms.assetid: ae116b60-fed2-4e1d-98a8-9fe83f460c50
keywords: デバッギング. デバッグ、Windbg、事後分析、just-in-time デバッグ、JIT デバッグ、AeDebug レジストリキー
ms.date: 09/17/2018
ms.localizationpriority: medium
ms.openlocfilehash: 66978e922da8f8b0699038359d0b1bf3d80dd9b2
ms.sourcegitcommit: dadc9ced1670d667e31eb0cb58d6a622f0f09c46
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/09/2020
ms.locfileid: "84534371"
---
# <a name="enabling-postmortem-debugging"></a>事後デバッグを有効にする


## <a name="span-idddk_enabling_postmortem_debugging_dbgspanspan-idddk_enabling_postmortem_debugging_dbgspanuser-mode-exception-handling"></a><span id="ddk_enabling_postmortem_debugging_dbg"></span><span id="DDK_ENABLING_POSTMORTEM_DEBUGGING_DBG"></span>ユーザーモードの例外処理


**例外とブレークポイント**

最も一般的なアプリケーションエラーは、例外と呼ばれます。 これには、アクセス違反、0除算エラー、数値オーバーフロー、CLR 例外、およびその他多くの種類のエラーが含まれます。 アプリケーションでブレークポイントの割り込みが発生することもあります。 これらは、Windows がアプリケーションを実行できない場合 (たとえば、必要なモジュールを読み込むことができない場合や、ブレークポイントが検出された場合) に発生します。 ブレークポイントは、デバッガーによってコードに挿入することも、 [**DebugBreak**](https://docs.microsoft.com/windows/desktop/api/debugapi/nf-debugapi-debugbreak)などの関数を介して呼び出すこともできます。

**例外ハンドラーの優先順位**

構成値とアクティブなデバッガーに基づいて、Windows はさまざまな方法でユーザーモードエラーを処理します。 次のシーケンスは、ユーザーモードのエラー処理に使用される優先順位を示しています。

1.  現在エラーが発生しているプロセスにユーザーモードのデバッガーがアタッチされている場合は、すべてのエラーによってターゲットがこのデバッガーで中断されます。

    ユーザーモードのデバッガーがアタッチされている限り、他のエラー処理メソッドは使用されません。これは、 [**gn ([例外を処理しない])**](gn--gn--go-with-exception-not-handled-.md)コマンドを使用する場合でも同じです。

2.  ユーザーモードのデバッガーがアタッチされておらず、実行中のコードに独自の例外処理ルーチン (たとえば、 **try-except**) がある場合、この例外処理ルーチンはエラーを処理しようとします。

3.  ユーザーモードのデバッガーがアタッチされておらず、Windows に開いているカーネルデバッグ接続があり、エラーがブレークポイントの割り込みである場合、Windows はカーネルデバッガーにアクセスしようとします。

    カーネルデバッグ接続は、Windows のブートプロセス中に開く必要があります。 ユーザーモードの割り込みによってカーネルデバッガーが中断されないようにするには、 **-du**パラメーターを指定して KDbgCtrl ユーティリティを使用します。 カーネルデバッグ接続の構成方法と KDbgCtrl の使用方法の詳細については、「[デバッグのセットアップ](getting-set-up-for-debugging.md)」を参照してください。

    カーネルデバッガーでは、 [**gh (例外処理による移動)**](gh--go-with-exception-handled-.md)を使用してエラーを無視し、ターゲットの実行を続行できます。 カーネルデバッガーをバイパスして手順4に進むには、 [**gn (例外を処理しないで実行)**](gn--gn--go-with-exception-not-handled-.md)を使用できます。

4.  手順1、2、および3の条件が適用されない場合、Windows は AeDebug レジストリ値で構成されたデバッグツールをアクティブ化します。 この状況で使用するツールとして、任意のプログラムを事前に選択できます。 選択したプログラムは、*事後分析デバッガー*と呼ばれます。

5.  手順1、2、および3の条件が適用されず、事後分析デバッガーが登録されていない場合は、Windows エラー報告 (WER) によってメッセージが表示され、使用可能な場合は解決策が提供されます。 また、レジストリに適切な値が設定されている場合、WER はメモリダンプファイルも書き込みます。 詳細については、「 [WER の使用](https://docs.microsoft.com/windows/win32/wer/using-wer)」および「[ユーザーモードダンプの収集](https://docs.microsoft.com/windows/win32/wer/collecting-user-mode-dumps)」を参照してください。

**DebugBreak 関数**

事後分析デバッガーがインストールされている場合は、 **DebugBreak**関数を呼び出すことによって、ユーザーモードアプリケーションからデバッガーを意図的に中断できます。

## <a name="span-idspecifying_a_postmortem_debuggerspanspan-idspecifying_a_postmortem_debuggerspanspan-idspecifying_a_postmortem_debuggerspanspecifying-a-postmortem-debugger"></a><span id="Specifying_a_Postmortem_Debugger"></span><span id="specifying_a_postmortem_debugger"></span><span id="SPECIFYING_A_POSTMORTEM_DEBUGGER"></span>事後分析デバッガーの指定


このセクションでは、WinDbg などのツールを事後分析デバッガーとして構成する方法について説明します。 構成が完了すると、アプリケーションがクラッシュするたびに、事後分析デバッガーが自動的に開始されます。

**事後デバッガーのレジストリキー**

Windows エラー報告 (WER) は、AeDebug レジストリキーに設定された値を使用して、事後分析デバッガープロセスを作成します。

**HKLM** \\**ソフトウェア** \\**Microsoft** \\**WINDOWS NT** \\**CurrentVersion** \\**AeDebug**

[*デバッガー* ] と [*自動*] の2つの主要なレジストリ値があります。*デバッガー*のレジストリ値は、事後分析デバッガーのコマンドラインを指定します。 *自動*レジストリ値は、事後分析デバッガーが自動的に開始されるかどうか、または確認メッセージボックスが最初に表示されるかどうかを指定します。

<span id="Debugger__REG_SZ_"></span><span id="debugger__reg_sz_"></span><span id="DEBUGGER__REG_SZ_"></span>**デバッガー (REG \_ SZ)**  

この REG \_ SZ 値は、事後分析デバッグを処理するデバッガーを指定します。

デバッガーが既定のパスにあるディレクトリに配置されている場合を除き、デバッガーへの完全なパスを一覧表示する必要があります。

コマンドラインは、3つのパラメーターを含む printf スタイルの呼び出しを通じて、デバッガー文字列から生成されます。 順序は固定されていますが、使用可能なパラメーターのいずれかまたはすべてを使用する必要はありません。

DWORD (% ld)-ターゲットプロセスのプロセス ID。

DWORD (% ld)-イベントハンドルが事後分析デバッガープロセスに重複しています。 事後分析デバッガーによってイベントが通知される場合、WER は、事後分析デバッガーが終了するのを待たずにターゲットプロセスを継続します。 イベントは、問題が解決された場合にのみ通知する必要があります。 イベントを通知せずに事後分析デバッガーが終了した場合、WER はターゲットプロセスに関する情報の収集を続行します。

void \* (% p)- \_ \_ ターゲットプロセスのアドレス空間に割り当てられた JIT デバッグ情報の構造体のアドレス。 構造体には、追加の例外情報とコンテキストが含まれています。

<span id="Auto__REG_SZ_"></span><span id="auto__reg_sz_"></span><span id="AUTO__REG_SZ_"></span>**Auto (reg \_ SZ)** この REG \_SZ value は常に**0**または**1**です。

**Auto**が**0**に設定されている場合は、事後分析のデバッグプロセスが開始される前に、確認メッセージボックスが表示されます。

**Auto**が**1**に設定されている場合、事後分析デバッガーがすぐに作成されます。

レジストリを手動で編集する場合は、レジストリに対する不適切な変更によって Windows の起動が許可されていない可能性があるため、慎重に行う必要があります。

**コマンドラインの使用例**

多くの事後分析デバッガーでは、-p スイッチと-e スイッチを含むコマンドラインを使用して、パラメーターが PID とイベント (それぞれ) であることを示します。 たとえば、を使用して WinDbg をインストールすると、 `windbg.exe -I` 次の値が作成されます。

```console
Debugger = "<Path>\WinDbg -p %ld -e %ld -g"
Auto = 1
```

WER% ld% ld% p パラメーターを使用する方法には柔軟性があります。 次に例を示します。 WER パラメーターの前後のスイッチを指定する必要はありません。 たとえば、を使用して[Windows Sysinternals ProcDump](https://docs.microsoft.com/sysinternals/downloads/procdump)をインストールする `procdump.exe -i` と、次の値が作成され、WER% ld% ld% p パラメーターの間にスイッチがありません。

```console
Debugger = "<Path>\procdump.exe" -accepteula -j "c:\Dumps" %ld %ld %p
Auto = 1
```

**32および64ビットのデバッガー**

64ビットプラットフォームでは、デバッガー (REG \_ sz) と自動 (reg \_ sz) レジストリ値は、64ビットアプリケーションと32ビットアプリケーションに対して個別に定義されます。 追加の Windows on Windows (WOW) キーは、32ビットアプリケーションの事後分析値を格納するために使用されます。

**HKLM** \\**ソフトウェア** \\**Wow6432Node** \\**Microsoft** \\**WINDOWS NT** \\**CurrentVersion** \\**AeDebug**

64ビットプラットフォームでは、32ビットプロセスには32ビットの事後分析デバッガーを、64ビットプロセスには64ビットのデバッガーを使用します。 これにより、32ビットプロセスで、32ビットスレッドではなく、WOW64 スレッドに焦点を当てる64ビットデバッガーが回避されます。

Windows 事後分析用デバッグツールなど、多くの事後対応デバッガーでは、インストールコマンドを2回実行する必要があります。x86 バージョンで1回、x64 バージョンで1回。 たとえば、対話的な事後分析デバッガーとして WinDbg を使用する場合、 `windbg.exe -I` コマンドはバージョンごとに1回実行されます。

64ビットインストール:

```console
C:\Program Files (x86)\Windows Kits\10\Debuggers\x64\windbg.exe –I
```

これにより、レジストリキーが次の値で更新されます。

```reg
HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows NT\CurrentVersion\AeDebug
Debugger = "C:\Program Files (x86)\Windows Kits\10\Debuggers\x64\windbg.exe" -p %ld -e %ld –g
```

32ビットインストール:

```console
C:\Program Files (x86)\Windows Kits\10\Debuggers\x86\windbg.exe –I
```

これにより、レジストリキーが次の値で更新されます。

```reg
HKEY_LOCAL_MACHINE\SOFTWARE\WOW6432Node\Microsoft\Windows NT\CurrentVersion\AeDebug
Debugger = "C:\Program Files (x86)\Windows Kits\10\Debuggers\x86\windbg.exe" -p %ld -e %ld –g
```

## <a name="span-idconfiguringspanspan-idconfiguringspanspan-idconfiguringspanconfiguring-post-mortem-debuggers"></a><span id="Configuring"></span><span id="configuring"></span><span id="CONFIGURING"></span>事後分析デバッガーの構成


### <a name="span-iddebugging_tools_for_windowsspanspan-iddebugging_tools_for_windowsspanspan-iddebugging_tools_for_windowsspandebugging-tools-for-windows"></a><span id="Debugging_Tools_for_Windows"></span><span id="debugging_tools_for_windows"></span><span id="DEBUGGING_TOOLS_FOR_WINDOWS"></span>Windows 用デバッグツール

Windows デバッガー用のデバッグツールはすべて、事後分析デバッガーとしての設定をサポートしています。 インストールコマンドを実行すると、プロセスが対話形式でデバッグされます。

**WinDbg**

事後分析デバッガーを WinDbg に設定するには、を実行 `windbg -I` します。 (は `I` 大文字にする必要があります)。このコマンドを使用すると、成功または失敗のメッセージが表示されます。 32と64の両方のビットアプリケーションを操作するには、64デバッガーと32デバッガーの両方に対してコマンドを実行します。

```console
C:\Program Files (x86)\Windows Kits\10\Debuggers\x64\windbg.exe –I
C:\Program Files (x86)\Windows Kits\10\Debuggers\x86\windbg.exe –I
```

この方法では、の実行時に AeDebug レジストリエントリが構成され `windbg -I` ます。

```console
Debugger = "<Path>\WinDbg -p %ld -e %ld -g"
Auto = 1
```

例では、 * &lt; Path &gt; *はデバッガーが配置されているディレクトリです。

前に説明したように、-p パラメーターと-e パラメーターには、プロセス ID とイベントが渡されます。

**-G**は、g (ゴー) コマンドを WinDbg に渡し、現在の命令から実行を継続します。

**メモ**   G (ゴー) コマンドを渡すことに大きな問題があります。 この方法の問題は、例外が常に繰り返されるわけではありません。通常は、コードの再起動時に存在しなくなった一時的な状態が原因です。 この問題の詳細については、「 [**. jdinfo (JIT \_ デバッグ \_ 情報の使用)**](-jdinfo--use-jit-debug-info-.md)」を参照してください。

この問題を回避するには、. jdinfo または. dump/j. を使用します。 この方法により、デバッガーは目的のコードエラーのコンテキストになることができます。 詳細については、このトピックで後述する「just-in-time [(JIT) デバッグ](#jit)」を参照してください。

 

**CDB**

事後分析デバッガーを CDB に設定するには、 **cdb-iae** (install AeDebug) または**cdb-iae** *keystring* (install AeDebug with Command) を実行します。

```console
C:\Program Files (x86)\Windows Kits\10\Debuggers\x64\cdb.exe -iae
C:\Program Files (x86)\Windows Kits\10\Debuggers\x86\cdb.exe -iae
```

**-Iaec**パラメーターを使用する場合、 *keystring*は、事後分析デバッガーを起動するために使用されるコマンドラインの末尾に追加される文字列を指定します。 *Keystring*にスペースが含まれている場合は、引用符で囲む必要があります。

```console
C:\Program Files (x86)\Windows Kits\10\Debuggers\x64\cdb.exe -iaec [KeyString]
C:\Program Files (x86)\Windows Kits\10\Debuggers\x86\cdb.exe -iaec [KeyString]
```

このコマンドは、成功した場合は何も表示せず、失敗した場合はエラーメッセージを表示します。

**NTSD**

事後分析デバッガーを NTSD に設定するには、 **ntsd-iae** (install AeDebug) または**ntsd-iae** *keystring* (install AeDebug with Command) を実行します。

```console
C:\Program Files (x86)\Windows Kits\10\Debuggers\x64\ntsd.exe -iae
C:\Program Files (x86)\Windows Kits\10\Debuggers\x86\ntsd.exe -iae
```

**-Iaec**パラメーターを使用する場合、 *keystring*は、事後分析デバッガーを起動するために使用されるコマンドラインの末尾に追加される文字列を指定します。 *Keystring*にスペースが含まれている場合は、引用符で囲む必要があります。

```console
C:\Program Files (x86)\Windows Kits\10\Debuggers\x64\ntsd.exe -iaec [KeyString]
C:\Program Files (x86)\Windows Kits\10\Debuggers\x86\ntsd.exe -iaec [KeyString]
```

このコマンドを実行すると、成功した場合は何も表示されず、エラーが発生した場合は新しいコンソールウィンドウにエラーが表示されます。

**メモ**   -P% ld-e% ld-g パラメーターは常に事後分析デバッガーのコマンドラインで表示されるため、-iaec スイッチを使用して-server パラメーターを指定することはできません。-server は、コマンドラインで最初に表示されない限り機能しません。 このパラメーターを含む事後分析デバッガーをインストールするには、レジストリを手動で編集する必要があります。

 

### <a name="span-idvisual_studio_jit_debuggerspanspan-idvisual_studio_jit_debuggerspanspan-idvisual_studio_jit_debuggerspanvisual-studio-jit-debugger"></a><span id="Visual_Studio_JIT_Debugger"></span><span id="visual_studio_jit_debugger"></span><span id="VISUAL_STUDIO_JIT_DEBUGGER"></span>Visual Studio JIT デバッガー

Visual Studio がインストールされている場合、vsjitdebugger.exe は事後分析デバッガーとして登録されます。 Visual Studio JIT デバッガーは、プロセスを対話的にデバッグすることを意図しています。

```console
Debugger = "C:\WINDOWS\system32\vsjitdebugger.exe" -p %ld -e %ld
```

Visual Studio が更新または再インストールされると、このエントリは再作成され、別の値セットが上書きされます。

### <a name="span-idwindow_sysinternals_procdumpspanspan-idwindow_sysinternals_procdumpspanspan-idwindow_sysinternals_procdumpspanwindow-sysinternals-procdump"></a><span id="Window_Sysinternals_ProcDump"></span><span id="window_sysinternals_procdump"></span><span id="WINDOW_SYSINTERNALS_PROCDUMP"></span>Window Sysinternals ProcDump

Windows Sysinternals ProcDump ユーティリティは、事後分析のダンプキャプチャにも使用できます。 ProcDump の使用とダウンロードの詳細については、 [ProcDump](https://docs.microsoft.com/sysinternals/downloads/procdump)を参照してください。

[**. Dump**](-dump--create-dump-file-.md) WinDbg コマンドと同様に、ProcDump は、クラッシュのダンプを非対話形式でキャプチャできます。 キャプチャは、任意の Windows システムセッションで発生する可能性があります。

ProcDump は、ダンプファイルのキャプチャが完了すると終了します。 WER はエラーを報告し、エラーが発生したプロセスは終了します。

`procdump -i`Procdump をインストールするにはを使用し、32と64ビットの両方のデバッグデバッグ用に procdump をアンインストールするには、を使用します。

```console
<Path>\procdump.exe -i
```

Install コマンドと uninstall コマンドを指定すると、成功時に変更されたレジストリ値と、失敗した場合のエラーが出力されます。

レジストリの ProcDump コマンドラインオプションは次のように設定されています。

```console
Debugger = <Path>\ProcDump.exe -accepteula -j "<DumpFolder>" %ld %ld %p
```

ProcDump は、PID、Event、および JIT デバッグ情報の3つのパラメーターをすべて使用 \_ \_ します。 JIT デバッグ情報パラメーターの詳細につい \_ \_ ては、次の「 [just-in-time (jit) デバッグ](#jit)」を参照してください。

既定では、キャプチャされるダンプのサイズは、サイズオプションが設定されていない場合はミニ (プロセス/スレッド/ハンドル/モジュール/アドレス空間) に設定され、-mp セットの場合は MiniPlus ( \_ すべてのメモリは ". dump/mA" に相当) に設定されます。

ドライブの空き領域が十分にあるシステムの場合は、フル (-ma) キャプチャを使用することをお勧めします。

-Ma を-i オプションと共に使用して、すべてのメモリキャプチャを指定します。 必要に応じて、ダンプファイルのパスを指定します。

```console
<Path>\procdump.exe -ma -i c:\Dumps
```

ドライブ領域が制限されているシステムの場合は、MiniPlus (-mp) キャプチャを使用することをお勧めします。

```console
<Path>\procdump.exe -mp -i c:\Dumps
```

ダンプファイルを保存するフォルダーは省略可能です。 既定値は現在のフォルダーです。 フォルダーは、C: Windows Temp で使用されるものと同等またはそれ以上の ACL で保護されている必要があり \\ \\ ます。フォルダーに関連するセキュリティの管理の詳細については、「[事後分析のデバッグ中のセキュリティ](security-during-postmortem-debugging.md)」を参照してください。

ProcDump を事後分析デバッガーとしてアンインストールし、以前の設定を復元するには、-u (Uninstall) オプションを使用します。

```console
<Path>\procdump.exe -u
```

インストールとアンインストールのコマンドでは、64ビットプラットフォームで64ビットと32ビットの両方の値が設定されます。

ProcDump は、32ビット版と64ビット版の両方のアプリケーションを含む "パックされた" 実行可能ファイルです。そのため、32ビットと64ビットの両方で同じ実行可能ファイルが使用されます。 ProcDump を実行すると、実行されているバージョンがターゲットプロセスと一致しない場合、バージョンが自動的に切り替えられます。

## <a name="span-idjitspanspan-idjitspan-just-in-time-jit-debugging"></a><span id="JIT"></span><span id="jit"></span>ジャストインタイム (JIT) デバッグ


**エラーが発生したアプリケーションへのコンテキストの設定**

前に説明したように、JIT デバッグ情報パラメーターを使用したクラッシュの原因となった例外にコンテキストを設定することをお勧めし \_ \_ ます。 詳細については、「 [**. jdinfo (JIT \_ デバッグ \_ 情報の使用)**](-jdinfo--use-jit-debug-info-.md)」を参照してください。

**Windows 用デバッグ ツール**

この例では、レジストリを編集して、jdinfo address コマンドを使用して追加の例外情報を表示する最初のコマンド (-c) を実行 &lt; &gt; し、コンテキストを例外の場所に変更する方法を示します (例: ecxr を使用してコンテキストを例外レコードに設定します)。

```console
Debugger = "<Path>\windbg.exe -p %ld -e %ld -c ".jdinfo 0x%p"
Auto = 1
```

% P パラメーターは、 \_ \_ ターゲットプロセスのアドレス空間にある JIT デバッグ情報の構造体のアドレスです。 % P パラメーターは、16進値として解釈されるように0x で事前に付加されています。 詳細については、「 [**. jdinfo (JIT \_ デバッグ \_ 情報の使用)**](-jdinfo--use-jit-debug-info-.md)」を参照してください。

32と64ビットのアプリの組み合わせをデバッグするには、32と64の両方のビットレジストリキー (上記を参照) の両方を構成し、適切なパスを64ビットと32ビットの WinDbg の場所に設定します。

**ダンプを使用したダンプファイルの作成**

JIT デバッグ情報データを含むエラーが発生した場合にダンプファイルをキャプチャするには \_ \_ 、. dump/j アドレスを使用し &lt; &gt; ます。

```console
<Path>\windbg.exe -p %ld -e %ld -c ".dump /j %p /u <DumpPath>\AeDebug.dmp; qd"
```

/U オプションを使用して一意のファイル名を生成し、複数のダンプファイルを自動的に作成できるようにします。 オプションの詳細については、「 [**. dump (ダンプファイルを作成する)**](-dump--create-dump-file-.md)」を参照してください。

作成されたダンプには、JITDEBUG \_ INFO データが既定の例外コンテキストとして格納されます。 Jdinfo を使用して例外情報を表示し、コンテキストを設定する代わりに、. exr-1 を使用して例外レコードを表示し、. ecxr を使用してコンテキストを設定します。 詳細については、「 [**(例外レコードの表示)**](-exr--display-exception-record-.md) 」および「 [**Ecxr (例外コンテキストレコードの表示)**](-ecxr--display-exception-context-record-.md)」を参照してください。

**Windows エラー報告-q/qd**

デバッグセッションの終了方法によって、Windows エラー報告がエラーを報告するかどうかが決まります。

デバッガーが終了する前に qd を使用してデバッグセッションをデタッチすると、WER はエラーを報告します。

Q を使用してデバッグセッションを終了した場合 (またはデバッガーがデタッチせずに閉じた場合)、WER はエラーを報告しません。

目的の動作を呼び出すために、コマンド文字列の末尾に*q*または *; qd*を追加します。

たとえば、CDB がダンプをキャプチャした後に WER がエラーを報告できるようにするには、このコマンド文字列を構成します。

```console
<Path>\cdb.exe -p %ld -e %ld -c ".dump /j 0x%p /u c:\Dumps\AeDebug.dmp; qd"
```

この例では、WinDbg がダンプをキャプチャした後に、WER がエラーを報告できるようにします。

```console
<Path>\windbg.exe -p %ld -e %ld -c ".dump /j %p /u <DumpPath>\AeDebug.dmp; qd""
```

## <a name="span-idsecurity_vulnerabilitiesspanspan-idsecurity_vulnerabilitiesspansecurity-vulnerabilities"></a><span id="security_vulnerabilities"></span><span id="SECURITY_VULNERABILITIES"></span>セキュリティの脆弱性


他のユーザーと共有するコンピューターで事後分析のデバッグを有効にすることを検討している場合は、「[事後分析のデバッグ中のセキュリティ](security-during-postmortem-debugging.md)」を参照してください。

 

 






---
title: 複数のターゲットのデバッグ
description: 複数のターゲットのデバッグ
ms.assetid: 93eb6b49-e7a0-4f30-ade8-94019a1adf43
keywords:
- 複数のターゲット
- システム
- システム, 概要
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 323836a8d1f357108793f224bc68473ef5eb1d14
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56548906"
---
# <a name="debugging-multiple-targets"></a>複数のターゲットのデバッグ


## <span id="ddk_debugging_multiple_targets_dbg"></span><span id="DDK_DEBUGGING_MULTIPLE_TARGETS_DBG"></span>


複数のダンプ ファイルをデバッグまたはユーザー モード アプリケーションを同時にライブできます。 各ターゲットには、1 つまたは複数のプロセスが含まれているし、プロセスごとに 1 つまたは複数のスレッドが含まれています。

これらのターゲットにまとめられます*システム*します。 システムは、簡単に識別および操作でグループ化されたターゲットのセットです。 システムの定義は次のとおりです。

-   各カーネル モードまたはユーザー モード ダンプ ファイルは、別のシステムです。

-   別のコンピューター上のライブ ユーザー モード アプリケーションをデバッグする際に (を使用して、[プロセス サーバー](process-servers--user-mode-.md)、Dbgsrv など)、各アプリケーションは別のシステムです。

-   ローカル コンピューターのライブ ユーザー モード アプリケーションをデバッグする場合は、アプリケーションが 1 つのシステムに結合されます。

*現在*または*active*システムは、現在デバッグしているシステム。

### <a name="span-idacquiringmultipletargetsspanspan-idacquiringmultipletargetsspanacquiring-multiple-targets"></a><span id="acquiring_multiple_targets"></span><span id="ACQUIRING_MULTIPLE_TARGETS"></span>複数のターゲットを取得します。

最初のターゲットは、通常の方法で取得されます。

使用して追加のライブ ユーザー モード アプリケーションをデバッグすることができます、 [ **.attach (プロセスにアタッチ)** ](-attach--attach-to-process-.md)または[ **(プロセスの作成) に関する**](-create--create-process-.md)コマンドの後に、 **g (移動)** コマンド。

使用して追加のダンプ ファイルをデバッグすることができます、 [ **.opendump (ダンプ ファイルを開く)** ](-opendump--open-dump-file-.md)コマンドの後に、 **g (移動)** コマンド。 デバッガーが開始されるとは、複数のダンプ ファイルを開くこともできます。 複数のダンプ ファイルを開くには、複数 **-z**コマンドで、その後は、別のファイル名でそれぞれのスイッチ。

さまざまなシステム上のプロセスがある場合でも、上記のコマンドを使用できます。 各システムにプロセス サーバーを起動し、使用する必要があります-premote パラメーター **.attach**または**に関する**適切なプロセス サーバーを識別するためにします。 使用する場合、 **.attach**または**に関する**を指定せずにもう一度コマンドは、premote パラメーターでは、デバッガーにアタッチするか、現在のシステム上のプロセスを作成します。

### <a name="span-idmanipulatingsystemsandtargetsspanspan-idmanipulatingsystemsandtargetsspanmanipulating-systems-and-targets"></a><span id="manipulating_systems_and_targets"></span><span id="MANIPULATING_SYSTEMS_AND_TARGETS"></span>システムとターゲットを操作します。

デバッグの開始時に、現在のシステムは、デバッガーが最後に接続されている 1 つにします。 例外が発生する場合、現在のシステムにこの例外が発生したシステムに切り替わります。

1 つのターゲットを閉じ、その他のターゲットのデバッグを続行を使用して、 [ **.kill (プロセスの強制終了)** ](-kill--kill-process-.md)コマンド。 使用することができます、 [ **.detach (プロセスからデタッチ)** ](-detach--detach-from-process-.md)コマンドまたは WinDbg の[デバッグ |デバッグ対象をデタッチ](debug---detach-debuggee.md)メニュー コマンドを代わりにします。 これらのコマンドでは、ターゲットからデバッガーをデタッチする、ターゲットの動作のままです。

複数のシステムのデバッグを制御するには、次のメソッドを使用できます。

-   [ **| |(システム状態)** ](----system-status-.md)コマンドでは、1 つまたは複数のシステムに関する情報を表示します。

-   [ **| |s (現在のシステムの設定)** ](--s--set-current-system-.md)コマンドでは、現在のシステムを選択できます。

-   (WinDbg のみ)[プロセスとスレッド ウィンドウ](processes-and-threads-window.md)により、表示や、システム、プロセス、およびスレッドを選択します。

これらのコマンドを使用して、現在のシステムを選択して、標準のコマンドを使用して[、現在のプロセスとスレッドを選択します。](controlling-processes-and-threads.md)、メモリとレジスタを表示するコマンドのコンテキストを決定することができます。

ただし、これらのプロセスの実行を分離することはできません。 [ **G (移動)** ](g--go-.md)コマンドが常に一緒に実行するすべてのターゲットを実行します。

**注**コマンドのデバッグの種類ごとに異なる方法で動作しているために、ライブのターゲットと、ダンプ ターゲットをデバッグするときに、問題があります。 たとえば、使用する場合、 **g (移動)** コマンドの場合は、現在のシステムは、ダンプ ファイル、デバッガーが実行を開始がすることはできません戻るデバッガーに割り込む、break コマンドが認識されないため、ダンプ ファイルのデバッグの有効とします。


<a name="example"></a>例
-------

同時に 3 つのダンプ ファイルを使用するのにには、WinDbg の開始時に読み込むに ~ z のオプションを使用することができます。 

```console
windbg -z c:\notepad.dmp -z c:\paint.dmp -z c:\calc.dmp
```

詳細については、次を参照してください。 [WinDbg コマンド ライン オプション](windbg-command-line-options.md)します。 使用することもできます、 [.opendump](-opendump--open-dump-file-.md)と[ **g (移動)** ](g--go-.md)コマンドを追加で読み込むが、デバッガー内のファイルをダンプします。 

使用して、 [| |(システム状態)](----system-status-.md)コマンドを 3 つすべてのシステムが存在することを確認します。

```dbgcmd
||0:0:007> ||
.  0 User mini dump: c:\notepad.dmp
   1 User mini dump: C:\paint.dmp
   2 User mini dump: c:\calc.dmp
```

使用して、 [ **g (移動)** ](g--go-.md)コマンドのダンプ ファイルの読み込みを完了します。 
```dbgcmd
||0:0:007> g

************* Path validation summary **************
Response                         Time (ms)     Location
Deferred                                       srv*
Symbol search path is: srv*
Executable search path is: 
Windows 10 Version 15063 MP (4 procs) Free x64
Product: WinNt, suite: SingleUserTS
15063.0.amd64fre.rs2_release.170317-1834
Machine Name:
Debug session time: Fri Jun  9 15:52:04.000 2017 (UTC - 7:00)
System Uptime: not available
Process Uptime: 0 days 0:03:44.000
...............................................................
This dump file has a breakpoint exception stored in it.
The stored exception information can be accessed via .ecxr.
ntdll!DbgBreakPoint:
00007ff8`aada8d70 cc              int     3
```

使用して、 [| |s (現在のシステムの設定)](--s--set-current-system-.md)コマンドを現在のシステムの 1 に設定し、現在のシステムを表示します。

```dbgcmd
||1:1:017> ||1s
||1:1:017> ||
   0 User mini dump: c:\notepad.dmp
.  1 User mini dump: c:\paint.dmp
   2 User mini dump: c:\calc.dmp
```

使用することができます、 [.detach](-detach--detach-from-process-.md)コマンドを完了したら、現在のダンプ ファイルを見るします。

```dbgcmd
||1:1:017> .detach
ntdll!DbgBreakPoint:
00007ff8`aada8d70 cc              int     3
Detached
||0:0:007> ||
.  0 User mini dump: c:\notepad.dmp
   2 User mini dump: c:\calc.dmp
```

<a name="resources"></a>参考資料
---------

デバッグの詳細については、次のリソースを参照してください。

**ブックの「**

- Mario Hewardt と Daniel Pravat によって高度な Windows のデバッグ

- 内部の Windows デバッグ:A Practical Guide to デバッグ出力およびトレース戦略 Tarik Soulami によって Windows の

- Pavel Yosifovich、Alex Ionescu、E. のある Mark Russinovich と David A. Solomon によって Windows の内部構造 

**ビデオ**

デフラグ ツール WinDbg エピソード 13 ~ 29 の表示します。 [https://channel9.msdn.com/Shows/Defrag-Tools](https://channel9.msdn.com/Shows/Defrag-Tools) 











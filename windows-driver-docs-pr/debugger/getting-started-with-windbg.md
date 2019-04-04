---
title: WinDbg ドライバーの概要 (ユーザー モード)
description: WinDbg では、Windows のツールのデバッグに含まれるカーネル モードとユーザー モード デバッガーです。 ここでユーザー モード デバッガーとして WinDbg を使用するのに役立つ実践的な演習を開始する提供されています。
ms.assetid: 8C2D2D0C-7E54-4711-A6FD-970E040F1C50
ms.date: 10/09/2017
ms.localizationpriority: medium
ms.openlocfilehash: d11e51525659a53c16a4356b013dc782e4f97019
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56578928"
---
# <a name="getting-started-with-windbg-user-mode"></a>WinDbg ドライバーの概要 (ユーザー モード)

WinDbg では、Windows のツールのデバッグに含まれるカーネル モードとユーザー モード デバッガーです。 ここでユーザー モード デバッガーとして WinDbg を使用するのに役立つ実践的な演習を開始する提供されています。

Windows のツールのデバッグを取得する方法については、[デバッグ ツールの Windows (WinDbg、KD、CDB、NTSD)](https://go.microsoft.com/fwlink/p?linkid=223405)を参照してください。 

デバッグ ツールをインストールした後は、64 ビット (x64) と、ツールの 32 ビット (x86) バージョンのインストール ディレクトリを見つけます。 以下に例を示します。

-   C:\\プログラム ファイル (x86)\\Windows キット\\8.1\\デバッガー\\x64
-   C:\\プログラム ファイル (x86)\\Windows キット\\8.1\\デバッガー\\x86

## <a name="span-idlaunchnotepadandattachwindbgspanspan-idlaunchnotepadandattachwindbgspanspan-idlaunchnotepadandattachwindbgspanlaunch-notepad-and-attach-windbg"></a><span id="Launch_Notepad_and_attach_WinDbg"></span><span id="launch_notepad_and_attach_windbg"></span><span id="LAUNCH_NOTEPAD_AND_ATTACH_WINDBG"></span>メモ帳を起動し、WinDbg をアタッチします。

1.  インストール ディレクトリに移動し、WinDbg.exe を開きます。

2.  デバッガーのドキュメントは回線で利用できるも[ここ](https://go.microsoft.com/fwlink/p?linkid=223405)します。

3.  **ファイル**] メニューの [選択**実行可能ファイルのオープン**します。 開いている実行可能ファイル ダイアログ ボックスで、notepad.exe を含むフォルダーに移動します (たとえば、c:\\Windows\\System32)。 **ファイル名**notepad.exe を入力します。 **[開く]** をクリックします。

    ![windbg をメモ帳を起動した後のスクリーン ショット](images/windbggetstart01.png)

4.  コマンドラインで、WinDbg ウィンドウの下部の近くには、このコマンドを入力します。

    [.sympath srv\*](https://go.microsoft.com/fwlink/p?linkid=399238)

    出力は次のようにします。

    ```dbgcmd
    Symbol search path is: srv*
    Expanded Symbol search path is: cache*;SRV
    ```

    シンボルの検索パスは、シンボル (PDB) ファイルを検索する場所を WinDbg に指示します。 デバッガーでは、シンボル ファイルのコード モジュール (関数名、変数名、およびなど) に関する情報を取得する必要があります。

    このコマンドは、最初に行う WinDbg に指示を入力します。 検索とシンボル ファイルの読み込み。

    [.reload](https://go.microsoft.com/fwlink/p?linkid=399239)

5.  Notepad.exe モジュールのシンボルを表示するには、このコマンドを入力します。

    [メモ帳 x! *](https://go.microsoft.com/fwlink/p?linkid=399240)

    **注**  出力が表示されない場合は、入力[ **.reload** ](https://go.microsoft.com/fwlink/p?linkid=399239)もう一度です。

    メインが含まれている Notepad.exe モジュールのシンボルを表示するには、このコマンドを入力します。

    [メモ帳 x!\*メイン\*](https://go.microsoft.com/fwlink/p?linkid=399240)
 
    出力は次のようにします。

    ```dbgcmd
    000000d0`428ff7e8 00007ff6`3282122f notepad!WinMain
    ...
    ```

6.  メモ帳でブレークポイントを設定します。WinMain、このコマンドを入力します。

    [bu メモ帳!WinMain](https://go.microsoft.com/fwlink/p?linkid=399390)

    ブレークポイントが設定されたことを確認するには、このコマンドを入力します。

    [bl](https://go.microsoft.com/fwlink/p?linkid=399391)

    出力は次のようにします。

    ```dbgcmd
    0 e 00007ff6`32825f64     0001 (0001)  0:**** notepad!WinMain
    ```

7.  実行しているメモ帳を起動するには、このコマンドを入力します。

    [g](https://go.microsoft.com/fwlink/p?linkid=399388)

    メモ帳を実行するまで、 **WinMain**関数、およびデバッガーでし中断します。

    メモ帳プロセスに読み込まれるコード モジュールの一覧を表示するには、このコマンドを入力します。

    [lm](https://go.microsoft.com/fwlink/p?linkid=399237)

    出力は次のようにします。

    ```dbgcmd
    0:000> lm
    start             end                 module name
    00007ff6`32820000 00007ff6`3285a000   notepad    (pdb symbols)          C:\...\notepad.pdb
    00007ffc`ab7e0000 00007ffc`ab85b000   WINSPOOL   (deferred)             
    00007ffc`aba10000 00007ffc`abc6a000   COMCTL32   (deferred)             
    00007ffc`adea0000 00007ffc`adf3f000   SHCORE     (deferred)             
    00007ffc`af490000 00007ffc`af59f000   KERNELBASE   (deferred)             
    00007ffc`af7d0000 00007ffc`af877000   msvcrt     (deferred)             
    00007ffc`af880000 00007ffc`b0c96000   SHELL32    (deferred)             
    00007ffc`b0e40000 00007ffc`b0ef7000   OLEAUT32   (deferred)             
    00007ffc`b0f00000 00007ffc`b0f57000   sechost    (deferred)             
    00007ffc`b0f60000 00007ffc`b1005000   ADVAPI32   (deferred)             
    00007ffc`b1010000 00007ffc`b1155000   GDI32      (deferred)             
    00007ffc`b1160000 00007ffc`b1296000   RPCRT4     (deferred)             
    00007ffc`b12a0000 00007ffc`b1411000   USER32     (deferred)             
    00007ffc`b1420000 00007ffc`b15f6000   combase    (deferred)             
    00007ffc`b16c0000 00007ffc`b17f9000   MSCTF      (deferred)             
    00007ffc`b1800000 00007ffc`b189a000   COMDLG32   (deferred)             
    00007ffc`b18a0000 00007ffc`b18f1000   SHLWAPI    (deferred)             
    00007ffc`b1b60000 00007ffc`b1cd8000   ole32      (deferred)             
    00007ffc`b1cf0000 00007ffc`b1e2a000   KERNEL32   (pdb symbols)          C:\...\kernel32.pdb
    00007ffc`b1eb0000 00007ffc`b1ee4000   IMM32      (deferred)             
    00007ffc`b1f50000 00007ffc`b20fa000   ntdll      (private pdb symbols)  C:\...\ntdll.pdb
    ```

    スタック トレースを表示するには、このコマンドを入力します。

    [K](https://go.microsoft.com/fwlink/p?linkid=399389)

    出力は次のようにします。

    ```dbgcmd
    Breakpoint 0 hit
    notepad!WinMain:
    00007ff6`32825f64 488bc4          mov     rax,rsp
    0:000> k
    Child-SP          RetAddr           Call Site
    00000048`4e0cf6a8 00007ff6`3282122f notepad!WinMain
    00000048`4e0cf6b0 00007ffc`b1cf16ad notepad!WinMainCRTStartup+0x1a7
    00000048`4e0cf770 00007ffc`b1fc4629 KERNEL32!BaseThreadInitThunk+0xd
    00000048`4e0cf7a0 00000000`00000000 ntdll!RtlUserThreadStart+0x1d ...
    ```

8.  もう一度実行しているメモ帳を起動するには、このコマンドを入力します。

    [g](https://go.microsoft.com/fwlink/p?linkid=399388)

9.  メモ帳に侵入する**Break**から、**デバッグ**メニュー。

10. 設定し、ブレークポイントを確認します。 **ZwWriteFile**、これらのコマンドを入力します。

    [bu ntdll!ZwWriteFile](https://go.microsoft.com/fwlink/p?linkid=399390)

    [bl](https://go.microsoft.com/fwlink/p?linkid=399391)

11. 入力[g](https://go.microsoft.com/fwlink/p?linkid=399388)をもう一度実行しているメモ帳を起動します。 メモ帳 ウィンドウで、いくつかのテキストを入力し、選択**保存**から、**ファイル**メニュー。 に関してはで、実行中のコード区切り**ZwCreateFile**します。 入力[k](https://go.microsoft.com/fwlink/p?linkid=399389)スタック トレースを表示します。

    ![windbg でスタック トレースのスクリーン ショット](images/windbggetstart02.png)

    WinDbg ウィンドウで、コマンドの行の左側には、プロセッサ、およびスレッドの番号に注意してください。 この例では、現在のプロセッサ数が 0 の場合と、現在のスレッド数は 11 です。 それでは見ている (これが実行されているプロセッサ 0 に当たります)、11 のスレッドのスタック トレース。

12. メモ帳プロセスのすべてのスレッドの一覧を表示するには、このコマンドの (ティルダ) を入力します。

    [~](https://go.microsoft.com/fwlink/p?linkid=399392)

    出力は次のようにします。

    ```dbgcmd
    0:011> ~
       0  Id: 10c8.128c Suspend: 1 Teb: 00007ff6`31cdd000 Unfrozen
       1  Id: 10c8.1a10 Suspend: 1 Teb: 00007ff6`31cdb000 Unfrozen
       2  Id: 10c8.1850 Suspend: 1 Teb: 00007ff6`31cd9000 Unfrozen
       3  Id: 10c8.1774 Suspend: 1 Teb: 00007ff6`31cd7000 Unfrozen
       4  Id: 10c8.1e80 Suspend: 1 Teb: 00007ff6`31cd5000 Unfrozen
       5  Id: 10c8.10ac Suspend: 1 Teb: 00007ff6`31cd3000 Unfrozen
       6  Id: 10c8.13a4 Suspend: 1 Teb: 00007ff6`31bae000 Unfrozen
       7  Id: 10c8.2b4 Suspend: 1 Teb: 00007ff6`31bac000 Unfrozen
       8  Id: 10c8.1df0 Suspend: 1 Teb: 00007ff6`31baa000 Unfrozen
       9  Id: 10c8.1664 Suspend: 1 Teb: 00007ff6`31ba8000 Unfrozen
      10  Id: 10c8.15e4 Suspend: 1 Teb: 00007ff6`31ba6000 Unfrozen
    . 11  Id: 10c8.8bc Suspend: 1 Teb: 00007ff6`31ba4000 Unfrozen
    ```

    この例では、インデックス 0 から 11 までに 12 個のスレッドがあります。

13. 0 のスレッドのスタック トレースを確認するには、これらのコマンドを入力します。

    [~ 0](https://go.microsoft.com/fwlink/p?linkid=399393)

    [K](https://go.microsoft.com/fwlink/p?linkid=399389)

    出力は次のようにします。

    ```dbgcmd
    0:011> ~0s
    USER32!SystemParametersInfoW:
    00007ffc`b12a4d20 48895c2408      mov     qword ptr [rsp+8], ...
    0:000> k
    Child-SP          RetAddr           Call Site
    00000033`d1e9da48 00007ffc`adfb227d USER32!SystemParametersInfoW
    (Inline Function) --------`-------- uxtheme!IsHighContrastMode+0x1d
    00000033`d1e9da50 00007ffc`adfb2f12 uxtheme!IsThemeActive+0x4d
    ...
    00000033`d1e9f810 00007ffc`b1cf16ad notepad!WinMainCRTStartup+0x1a7
    00000033`d1e9f8d0 00007ffc`b1fc4629 KERNEL32!BaseThreadInitThunk+0xd
    00000033`d1e9f900 00000000`00000000 ntdll!RtlUserThreadStart+0x1d
    ```

14. デバッグを終了し、メモ帳プロセスからデタッチするには、このコマンドを入力します。

    [qd](https://go.microsoft.com/fwlink/p?linkid=399394)

## <a name="span-idlaunchyourownapplicationandattachwindbgspanspan-idlaunchyourownapplicationandattachwindbgspanspan-idlaunchyourownapplicationandattachwindbgspanlaunch-your-own-application-and-attach-windbg"></a><span id="Launch_your_own_application_and_attach_WinDbg"></span><span id="launch_your_own_application_and_attach_windbg"></span><span id="LAUNCH_YOUR_OWN_APPLICATION_AND_ATTACH_WINDBG"></span>独自のアプリケーションを起動し、WinDbg をアタッチします。


書き込み、この小さなコンソール アプリケーションを構築したとします。

```dbgcmd
...
void MyFunction(long p1, long p2, long p3)
{
    long x = p1 + p2 + p3;
    long y = 0;
    y = x / p2;
}

void main ()
{
    long a = 2;
    long b = 0;
    MyFunction(a, b, 5);
}
```

この演習では前提としています、ビルド済みアプリケーション (MyApp.exe) とシンボル ファイル (MyApp.pdb) の c: は\\MyApp\\x64\\をデバッグします。 アプリケーションのソース コードが c: であると仮定されますも\\MyApp\\MyApp します。

1.  WinDbg を開きます。

2.  **ファイル**] メニューの [選択**実行可能ファイルのオープン**します。 開いている実行可能ファイル ダイアログ ボックスで、c: に移動します。\\MyApp\\x64\\をデバッグします。 **ファイル名**MyApp.exe を入力します。 **[開く]** をクリックします。
3.  これらのコマンドを入力します。

    [.sympath srv\*](https://go.microsoft.com/fwlink/p?linkid=399238)

    .sympath + c:\\MyApp\\x64\\デバッグ

    [c: .srcpath\\MyApp\\MyApp](https://go.microsoft.com/fwlink/p?linkid=399395)

    今すぐ WinDbg は、アプリケーション用のシンボルとソース コードの検索場所を認識します。

4.  これらのコマンドを入力します。

    [.reload](https://go.microsoft.com/fwlink/p?linkid=399239)

    [bu MyApp! メイン](https://go.microsoft.com/fwlink/p?linkid=399390)

    [g](https://go.microsoft.com/fwlink/p?linkid=399388)

    際、アプリケーションがデバッガーにブレークその**メイン**関数。

    WinDbg では、ソース コードと、コマンド ウィンドウを表示します。

    ![windbg でソース コードのスクリーン ショット](images/windbggetstart03.png)

5.  **デバッグ**] メニューの [選択**ステップ イン**(またはキーを押します**F11**)。 ステップ インにステップ インを続けて**MyFunction**します。 行にステップ インしたら`y = x / p2`アプリケーションがクラッシュして、デバッガーを中断します。 出力は次のようにします。

    ```dbgcmd
    (1450.1424): Integer divide-by-zero - code c0000094 (first chance)
    First chance exceptions are reported before any exception handling.
    This exception may be expected and handled.
    MyApp!MyFunction+0x44:
    00007ff6`3be11064 f77c2428    idiv  eax,dword ptr [rsp+28h] ss:00000063`2036f808=00000000
    ```

6.  次のコマンドを入力します。

    [! - v の分析](https://go.microsoft.com/fwlink/p?linkid=399396)

    WinDbg では、(この場合は 0 による除算)、問題の分析が表示されます。

    ```dbgcmd
    FAULTING_IP: 
    MyApp!MyFunction+44 [c:\myapp\myapp\myapp.cpp @ 7]
    00007ff6`3be11064 f77c2428        idiv    eax,dword ptr [rsp+28h]

    EXCEPTION_RECORD:  ffffffffffffffff -- (.exr 0xffffffffffffffff)
    ExceptionAddress: 00007ff63be11064 (MyApp!MyFunction+0x0000000000000044)
       ExceptionCode: c0000094 (Integer divide-by-zero)
      ExceptionFlags: 00000000
    NumberParameters: 0
    ...
    STACK_TEXT:  
    00000063`2036f7e0 00007ff6`3be110b8 : ... : MyApp!MyFunction+0x44
    00000063`2036f800 00007ff6`3be1141d : ... : MyApp!main+0x38
    00000063`2036f840 00007ff6`3be1154e : ... : MyApp!__tmainCRTStartup+0x19d
    00000063`2036f8b0 00007ffc`b1cf16ad : ... : MyApp!mainCRTStartup+0xe
    00000063`2036f8e0 00007ffc`b1fc4629 : ... : KERNEL32!BaseThreadInitThunk+0xd
    00000063`2036f910 00000000`00000000 : ... : ntdll!RtlUserThreadStart+0x1d

    STACK_COMMAND: dt ntdll!LdrpLastDllInitializer BaseDllName ;dt ntdll!LdrpFailureData ;.cxr 0x0 ;kb

    FOLLOWUP_IP: 
    MyApp!MyFunction+44 [c:\myapp\myapp\myapp.cpp @ 7]
    00007ff6`3be11064 f77c2428        idiv    eax,dword ptr [rsp+28h]

    FAULTING_SOURCE_LINE:  c:\myapp\myapp\myapp.cpp

    FAULTING_SOURCE_FILE:  c:\myapp\myapp\myapp.cpp

    FAULTING_SOURCE_LINE_NUMBER:  7

    FAULTING_SOURCE_CODE:  
         3: void MyFunction(long p1, long p2, long p3)
         4: {
         5:     long x = p1 + p2 + p3;
         6:     long y = 0;
    >    7:  y = x / p2;
         8: }
         9: 
        10: void main ()
        11: {
        12:     long a = 2;
    ...
    ```

## <a name="span-idsummaryofcommandsspanspan-idsummaryofcommandsspanspan-idsummaryofcommandsspansummary-of-commands"></a><span id="Summary_of_commands"></span><span id="summary_of_commands"></span><span id="SUMMARY_OF_COMMANDS"></span>コマンドの概要


-   **内容**コマンドを**ヘルプ**メニュー
-   [.sympath (シンボル パスの設定)](https://go.microsoft.com/fwlink/p?linkid=399238)
-   [.reload (モジュールの再読み込み)](https://go.microsoft.com/fwlink/p?linkid=399239)
-   [x (シンボルの検証)](https://go.microsoft.com/fwlink/p?linkid=399240)
-   [g (移動)](https://go.microsoft.com/fwlink/p?linkid=399388)
-   **中断**コマンドを**デバッグ**メニュー
-   [lm (読み込まれたモジュールを一覧表示)](https://go.microsoft.com/fwlink/p?linkid=399237)
-   [k (Display Stack Backtrace)](https://go.microsoft.com/fwlink/p?linkid=399389)
-   [bu (ブレークポイントの設定)](https://go.microsoft.com/fwlink/p?linkid=399390)
-   [bl (ブレークポイントの一覧)](https://go.microsoft.com/fwlink/p?linkid=399390)
-   [~ (スレッドの状態)](https://go.microsoft.com/fwlink/p?linkid=399392)
-   [~ s (現在のスレッドのセット)](https://go.microsoft.com/fwlink/p?linkid=399393)
-   [.sympath + (シンボル パスの設定) を既存のシンボル パスに追加します。](https://go.microsoft.com/fwlink/p?linkid=399238)
-   [.srcpath (ソース パスの設定)](https://go.microsoft.com/fwlink/p?linkid=399395)
-   **ステップ イン**コマンドを**デバッグ**メニュー (**F11**)
-   [! - v の分析](https://go.microsoft.com/fwlink/p?linkid=399396)
-   [qd (Quit およびデタッチ)](https://go.microsoft.com/fwlink/p?linkid=399394)

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>関連トピック


[WinDbg ドライバーの概要 (カーネル モード)](getting-started-with-windbg--kernel-mode-.md)

[デバッガーの操作](https://go.microsoft.com/fwlink/p?linkid=399247)

[デバッグの手法](https://go.microsoft.com/fwlink/p?linkid=399248)

[(WinDbg、KD、CDB、NTSD)、Windows 用デバッグ ツール](https://go.microsoft.com/fwlink/p?linkid=223405)

 

 







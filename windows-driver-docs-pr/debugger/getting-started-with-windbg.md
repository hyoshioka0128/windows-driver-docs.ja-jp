---
title: WinDbg ドライバーの概要 (ユーザー モード)
description: WinDbg は、Debugging Tools for Windows に含まれているカーネルモードおよびユーザーモードのデバッガーです。 ここでは、ユーザーモードのデバッガーとして WinDbg の使用を開始する際に役立つ実践的な演習を提供します。
ms.assetid: 8C2D2D0C-7E54-4711-A6FD-970E040F1C50
ms.date: 06/05/2020
ms.localizationpriority: high
ms.openlocfilehash: 4e45ddb13f02a0a2d7f8e76f70aeb818e6c39e4d
ms.sourcegitcommit: 1d531bf9d02653fdf9ad728126d68b8acb86182e
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/29/2020
ms.locfileid: "87402311"
---
# <a name="getting-started-with-windbg-user-mode"></a>WinDbg ドライバーの概要 (ユーザー モード)

WinDbg は、Debugging Tools for Windows に含まれているカーネルモードおよびユーザーモードのデバッガーです。 ここでは、ユーザーモードのデバッガーとして WinDbg の使用を開始する際に役立つ実践的な演習を提供します。

Debugging Tools for Windows を取得する方法については、「[Debugging Tools for Windows (WinDbg、KD、CDB、NTSD)](https://docs.microsoft.com//windows-hardware/drivers/debugger/)」を参照してください。

デバッグ ツールをインストールしたら、64 ビット (x64) および 32 ビット (x86) バージョンのツールのインストール ディレクトリを検索します。 次に、例を示します。

- C:\\Program Files (x86)\\Windows Kits\\10\\Debuggers\\x64
- C:\\Program Files (x86)\\Windows Kits\\10\\Debuggers\\x86

## <a name="launch-notepad-and-attach-windbg"></a>メモ帳を起動して WinDbg をアタッチする

1. インストール ディレクトリに移動し、WinDbg.exe を開きます。

2. デバッガーのドキュメントは、[docs.microsoft.com](https://docs.microsoft.com/windows-hardware/drivers/debugger/) からオンラインで入手することもできます。

3. **[ファイル]** メニューで **[実行可能ファイルを開く]** を選択します。 [実行可能ファイルを開く] ダイアログ ボックスで、notepad.exe が格納されているフォルダー (たとえば、C:\\Windows\\System32) に移動します。 **[ファイル名]** に「notepad.exe」と入力します。 **[開く]** をクリックします。

    ![メモ帳を起動した後の WinDbg のスクリーンショット](images/windbggetstart01.png)

4. WinDbg ウィンドウの下の方にあるコマンド ラインに、次のコマンドを入力します。

    [.sympath srv\*](-sympath--set-symbol-path-.md)

    出力は次のようになります。

    ```dbgcmd
    Symbol search path is: srv*
    Expanded Symbol search path is: cache*;SRV
    ```

    シンボルの検索パスにより、シンボル (PDB) ファイルを検索する場所が WinDbg に指示されます。 デバッガーには、コード モジュール (関数名、変数名など) に関する情報を取得するために、シンボル ファイルが必要です。

    次のコマンドを入力します。これは、シンボル ファイルの最初の検索と読み込みを実行するように WinDbg に指示します。

    [.reload](-reload--reload-module-.md)

5. Notepad.exe モジュールのシンボルを表示するには、次のコマンドを入力します。

    [x notepad!*](x--examine-symbols-.md)

    **注**  出力が表示されない場合は、もう一度「[ **.reload**](-reload--reload-module-.md)」と入力します。

    main を含む Notepad.exe モジュール内のシンボルを表示するには、次のコマンドを入力します。

    [x notepad!\*main\*](x--examine-symbols-.md)

    出力は次のようになります。

    ```dbgcmd
    000000d0`428ff7e8 00007ff6`3282122f notepad!WinMain
    ...
    ```

6. notepad!WinMain にブレークポイントを配置するには、次のコマンドを入力します。

    [bu notepad!WinMain](bp--bu--bm--set-breakpoint-.md)

    ブレークポイントが設定されたことを確認するには、次のコマンドを入力します。

    [bl](bl--breakpoint-list-.md)

    出力は次のようになります。

    ```dbgcmd
    0 e 00007ff6`32825f64     0001 (0001)  0:**** notepad!WinMain
    ```

7. メモ帳の実行を開始するには、次のコマンドを入力します。

    [g](g--go-.md)

    メモ帳は、**WinMain** 関数に至るまで実行された後、デバッガーが中断されます。

    ```dbgcmd
    Breakpoint 0 hit
    notepad!WinMain:
    00007ff6`32825f64 488bc4          mov     rax,rsp
    ```

    メモ帳プロセスに読み込まれているコード モジュールの一覧を表示するには、次のコマンドを入力します。

    [lm](lm--list-loaded-modules-.md)

    出力は次のようになります。

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

    スタック トレースを表示するには、次のコマンドを入力します。

    [k](k--kb--kc--kd--kp--kp--kv--display-stack-backtrace-.md)

    出力は次のようになります。

    ```dbgcmd
    0:000> k
    Child-SP          RetAddr           Call Site
    00000048`4e0cf6a8 00007ff6`3282122f notepad!WinMain
    00000048`4e0cf6b0 00007ffc`b1cf16ad notepad!WinMainCRTStartup+0x1a7
    00000048`4e0cf770 00007ffc`b1fc4629 KERNEL32!BaseThreadInitThunk+0xd
    00000048`4e0cf7a0 00000000`00000000 ntdll!RtlUserThreadStart+0x1d ...
    ```

8. メモ帳の実行を再度開始するには、次のコマンドを入力します。

    [g](g--go-.md)

9. メモ帳を中断するには、 **[デバッグ]** メニューから **[中断]** を選択します。

10. **ZwWriteFile** でブレークポイントを設定して確認するには、次のコマンドを入力します。

    [bu ntdll!ZwWriteFile](bp--bu--bm--set-breakpoint-.md)

    [bl](bl--breakpoint-list-.md)

11. 「[g](g--go-.md)」を入力して、メモ帳の実行を再度開始します。 メモ帳ウィンドウで、何らかのテキストを入力し、 **[ファイル]** メニューから **[保存]** を選択します。 実行中のコードは、**ZwCreateFile** まで来ると、中断されます。 スタック トレースを表示するには、「[k](k--kb--kc--kd--kp--kp--kv--display-stack-backtrace-.md)」を入力します。

    ![WinDbg のスタック トレースのスクリーンショット](images/windbggetstart02.png)

    コマンド ラインの左側にある [WinDbg] ウィンドウで、プロセッサ番号とスレッド番号に注目してください。 この例では、現在のプロセッサ番号は 0、現在のスレッド番号は 11 になっています。 したがって、スレッド 11 のスタック トレース (プロセッサ 0 で実行されている) を見ていることになります。

12. メモ帳プロセス内のすべてのスレッドの一覧を表示するには、次のコマンド (チルダ) を入力します。

    [~](---thread-status-.md)

    出力は次のようになります。

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

    この例では、インデックス 0 - 11 の 12 個のスレッドがあります。

13. スレッド 0 のスタック トレースを確認するには、次のコマンドを入力します。

    [~0s](-s--set-current-thread-.md)

    [k](k--kb--kc--kd--kp--kp--kv--display-stack-backtrace-.md)

    出力は次のようになります。

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

14. デバッグを終了し、メモ帳プロセスからデタッチするには、次のコマンドを入力します。

    [qd](qd--quit-and-detach-.md)

## <a name="launch-your-own-application-and-attach-windbg"></a>独自のアプリケーションを起動し、WinDbg をアタッチする

この小さなコンソール アプリケーションを作成してビルドしたとします。

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

この演習では、ビルドされたアプリケーション (MyApp.exe) とシンボル ファイル (MyApp) が C:\\MyApp\\x64\\Debug にあると想定します。 また、アプリケーションのソース コードが C:\\MyApp\\MyApp にあり、ターゲット マシンが MyApp.exe をコンパイルしたと想定します。

1. WinDbg を開きます。

2. **[ファイル]** メニューで **[実行可能ファイルを開く]** を選択します。 [実行可能ファイルを開く] ダイアログ ボックスで、C:\\MyApp\\x64\\Debug に移動します。 **[ファイル名]** に「MyApp.exe」と入力します。 **[開く]** をクリックします。
3. 次のコマンドを入力します。

    [.symfix](-symfix--set-symbol-store-path-.md)

    [.sympath](-sympath--set-symbol-path-.md)+ C:\\MyApp\\x64\\Debug

    これで、アプリケーションのシンボルとソース コードの検索場所が WinDbg で認識されるようになりました。 この場合、シンボルにはソース ファイルへの完全修飾パスがあるため、[.srcpath](-srcpath---lsrcpath--set-source-path-.md) でソース コードの場所を設定する必要はありません。

4. 次のコマンドを入力します。

    [.reload](-reload--reload-module-.md)

    [bu MyApp!main](bp--bu--bm--set-breakpoint-.md)

    [g](g--go-.md)

    アプリケーションが、その **main** 関数まで来ると、デバッガーが中断されます。

    WinDbg により、ソース コードとコマンド ウィンドウが表示されます。

    ![WinDbg のソース コードのスクリーンショット](images/windbggetstart03.png)

5. **[デバッグ]** メニューで、 **[ステップ イン]** を選択します (または **F11** キーを押します)。 **MyFunction** にステップ インするまで、ステップ実行を続行します。 行 `y = x / p2` にステップ インすると、アプリケーションがクラッシュし、デバッガーが中断されます。 出力は次のようになります。

    ```dbgcmd
    (1450.1424): Integer divide-by-zero - code c0000094 (first chance)
    First chance exceptions are reported before any exception handling.
    This exception may be expected and handled.
    MyApp!MyFunction+0x44:
    00007ff6`3be11064 f77c2428    idiv  eax,dword ptr [rsp+28h] ss:00000063`2036f808=00000000
    ```

6. 次のコマンドを入力します。

    [!analyze -v](-analyze.md)

    WinDbg により、問題の分析が表示されます (この場合は 0 による除算)。

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

## <a name="summary-of-commands"></a>コマンドのまとめ

- **[ヘルプ]** メニューの **[コンテンツ]** コマンド
- [.sympath (シンボル パスの設定)](-sympath--set-symbol-path-.md)
- [.reload (モジュールの再読み込み)](-reload--reload-module-.md)
- [x (シンボルの検証)](x--examine-symbols-.md)
- [g (実行)](g--go-.md)
- **[デバッグ]** メニューの **[中断]** コマンド
- [lm (読み込まれたモジュールの一覧表示)](lm--list-loaded-modules-.md)
- [k (スタック バックトレースの表示)](k--kb--kc--kd--kp--kp--kv--display-stack-backtrace-.md)
- [bu (ブレークポイントの設定)](bp--bu--bm--set-breakpoint-.md)
- [bl (ブレークポイントの一覧)](bl--breakpoint-list-.md)
- [~ (スレッドの状態)](---thread-status-.md)
- [~s (現在のスレッドの設定)](-s--set-current-thread-.md)
- [.sympath+ (シンボル パスの設定) を既存のシンボル パスに追加する](-sympath--set-symbol-path-.md)
- [.srcpath (ソース パスの設定)](-srcpath---lsrcpath--set-source-path-.md)
- **[デバッグ]** メニューの **[ステップ イン]** コマンド (**F11**)
- [!analyze -v](-analyze.md)
- [qd (終了してデタッチ)](qd--quit-and-detach-.md)

## <a name="related-topics"></a>関連トピック

[WinDbg ドライバーの概要 (カーネル モード)](getting-started-with-windbg--kernel-mode-.md)

[デバッガーの操作](debugger-operation-win8.md)

[デバッグの手法](debugging-techniques.md)

[Debugging Tools for Windows (WinDbg、KD、CDB、NTSD)](https://docs.microsoft.com/windows-hardware/drivers/debugger/)

[WinDbg プレビューを使用したデバッグ](debugging-using-windbg-preview.md)

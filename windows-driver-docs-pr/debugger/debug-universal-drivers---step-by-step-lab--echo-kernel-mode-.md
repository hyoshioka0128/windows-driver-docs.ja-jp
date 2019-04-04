---
title: ユニバーサル ドライバー - ステップ バイ ステップのラボ (エコー カーネル モード) のデバッグします。
description: このラボでは、WinDbg カーネル デバッガーについて説明します。 WinDbg は、カーネル モードのサンプルをエコー ドライバー コードのデバッグに使用されます。
ms.assetid: 3FBC3693-4288-42BA-B1E8-84DC2A9AFFD9
keywords:
- ラボをデバッグします。
- ステップ バイ ステップ
- エコー
ms.date: 03/28/2019
ms.localizationpriority: medium
ms.openlocfilehash: 8900b9f6098ccf2c560d21b4cf941c484ff089c3
ms.sourcegitcommit: 1a5d7884cec9dd8d2b85242bee78b56a1cf8e4c9
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/01/2019
ms.locfileid: "58761859"
---
# <a name="span-iddebuggerdebuguniversaldrivers-stepbysteplabechokernel-modespandebug-universal-drivers---step-by-step-lab-echo-kernel-mode"></a><span id="debugger.debug_universal_drivers_-_step_by_step_lab__echo_kernel-mode_"></span>ユニバーサル ドライバー - ステップ バイ ステップのラボ (エコー カーネル モード) のデバッグします。


このラボでは、WinDbg カーネル デバッガーについて説明します。 WinDbg は、カーネル モードのサンプルをエコー ドライバー コードのデバッグに使用されます。

## <a name="span-idlabobjectivesspanspan-idlabobjectivesspanspan-idlabobjectivesspanlab-objectives"></a><span id="Lab_objectives"></span><span id="lab_objectives"></span><span id="LAB_OBJECTIVES"></span>ラボの目的


このラボには、デバッグ ツールを紹介し、一般的なデバッグ コマンドを教える、許可された改行ポイントの使用方法を示しますデバッグ拡張機能の使用方法を示して演習が含まれています。

この演習では、ライブのカーネル デバッグ接続を使用して、次の探索にします。

-   Windows のデバッガー コマンドを使用します。
-   (呼び出し履歴、変数、スレッド、IRQL) 標準のコマンドを使用します。
-   ドライバーのコマンドのデバッグを高度な使用 (! コマンド)
-   シンボルを使用します。
-   ライブ デバッグのブレークポイントを設定します。
-   呼び出し履歴の表示
-   プラグ アンド プレイ デバイスのツリーを表示します
-   スレッドとプロセスのコンテキストを使用します。

**注**Windows デバッガーを使用する場合は 2 つの種類のデバッグ、実行できるユーザーまたはカーネル モードのデバッグします。

*ユーザー モード*-ユーザー モードでコンピューターでアプリケーションやサブシステムを実行します。 ユーザー モードで実行されるプロセスは、独自の仮想アドレス空間内で行います。 システム ハードウェア、使用、およびシステムの整合性を損なう可能性があるシステムの他の部分が割り当てられていないメモリを含む、システムの多くの部分に直接アクセスが禁止されます。 ユーザー モードで実行されているプロセスが、システムおよびその他のユーザー モード プロセスから効果的に分離されたため、これらのリソース使用でき、干渉ことはできません。

*カーネル モード*-カーネル モードは、オペレーティング システムおよび特権のあるプログラムが実行されるプロセッサへのアクセス モード。 カーネル モード コードは、システムの任意の部分にアクセスする権限を持つ、ユーザー モード コードのように制限されません。 ユーザー モードまたはカーネル モードのいずれかで実行されている他のプロセスのあらゆる部分にアクセスできます。 コア OS 機能の多くと多くのハードウェア デバイス ドライバーは、カーネル モードで実行します。

多くのデバイス ドライバーをデバッグするために使用するメソッドであるために、このラボはカーネル モードのデバッグに焦点します。


この演習では、ユーザー モードおよびカーネル モードのデバッグ中に頻繁に使用するデバッグ コマンドについて説明します。 この演習では、デバッグ拡張機能についても説明 (とも呼ばれる"! コマンド") のカーネル モードのデバッグに使用します。

## <a name="span-idlabsetupspanspan-idlabsetupspanspan-idlabsetupspanlab-setup"></a><span id="Lab_setup"></span><span id="lab_setup"></span><span id="LAB_SETUP"></span>ラボのセットアップ


次のハードウェア ラボを完成させることができる必要があります。

-   ラップトップまたはデスクトップ コンピューター (ホスト) Windows 10 を実行しています。
-   ラップトップまたはデスクトップ コンピューター (ターゲット) Windows 10 を実行しています。
-   ネットワーク ハブまたはルーターと 2 台の Pc に接続するネットワーク ケーブル
-   シンボル ファイルをダウンロードにインターネットへのアクセス

次のソフトウェアのラボを完成させることができる必要があります。

-   Visual Studio 2017
-   Windows 10 用 Windows ソフトウェア開発キット (SDK)
-   Windows 10 用 Windows Driver Kit (WDK)
-   Windows 10 用のサンプルの echo ドライバー

ラボは、次のセクションでは、11 個にします。

-   [セクション 1:カーネル モードの WinDbg セッションに接続します。](#connectto)
-   [セクション 2:カーネル モードのデバッグ コマンドや技法](#kernelmodedebuggingcommandsandtechniques)
-   [セクション 3:ダウンロードして、KMDF ユニバーサル エコー ドライバーのビルド](#download)
-   [セクション 4:ターゲット システムにエコーの KMDF ドライバーのサンプルをインストールします。](#install)
-   [セクション 5:WinDbg を使用して、ドライバーに関する情報を表示するには](#usewindbgtodisplayinformation)
-   [セクション 6:プラグ アンド プレイ デバイス ツリーの情報を表示します。](#displayingtheplugandplaydevicetree)
-   [セクション 7:ブレークポイントとソース コードを使用します。](#workingwithbreakpoints)
-   [セクション 8:変数を表示し、呼び出し履歴](#viewingvariables)
-   [セクション 9:表示のプロセスとスレッド](#displayingprocessesandthreads)
-   [セクションの 10:IRQL、レジスタと WinDbg のセッションを終了します。](#irqlregistersmemory)
-   [第 11 条:Windows デバッグ用のリソース](#windowsdebuggingresources)

## <a name="span-idconnecttospanspan-idconnecttospansection-1-connect-to-a-kernel-mode-windbg-session"></a><span id="connectto"></span><span id="CONNECTTO"></span>セクション 1:カーネル モードの WinDbg セッションに接続します。


*セクション 1 では、ネットワークのホストとターゲット システム上でデバッグを構成します。*

このラボでの Pc は、カーネル デバッグをイーサネット ネットワーク接続を使用するように構成する必要があります。

この演習では、2 台の Pc を使用します。 Windows デバッガーを実行する、*ホスト*システムおよび KMDF エコー ドライバー上で実行、*ターゲット*システム。

 ネットワーク ハブまたはルーターとのネットワーク ケーブルを使用して、2 台の Pc を接続します。

![二重矢印で接続されている 2 台の pc](images/debuglab-image-targethostdrawing1.png)

カーネル モードのアプリケーションを使用し、WinDbg を使用して、イーサネット転送を KDNET を使用することをお勧めします。 イーサネット トランスポート プロトコルを使用する方法については、[WinDbg (カーネル モード) の概要](getting-started-with-windbg--kernel-mode-.md)を参照してください。 ターゲット コンピューターの設定に関する詳細については、[手動ドライバーの展開のコンピューターを準備する](https://msdn.microsoft.com/windows-drivers/develop/preparing_a_computer_for_manual_driver_deployment)と[設定を KDNET ネットワーク カーネル デバッグを自動的に](setting-up-a-network-debugging-connection-automatically.md)を参照してください。

### <a name="span-idconfigurekernelmodedebuggingusingethernetspanspan-idconfigurekernelmodedebuggingusingethernetspanspan-idconfigurekernelmodedebuggingusingethernetspanconfigure-kernelmode-debugging-using-ethernet"></a><span id="Configure__kernel_mode_debugging_using_ethernet"></span><span id="configure__kernel_mode_debugging_using_ethernet"></span><span id="CONFIGURE__KERNEL_MODE_DEBUGGING_USING_ETHERNET"></span>イーサネットを使用してカーネル – モードのデバッグを構成します。

カーネル モードが、ターゲット システムでのデバッグを有効にするには、次の手順を実行します。

**&lt;ホスト システムで**

1. ホスト システムと種類でコマンド プロンプトを開き**ipconfig**その IP アドレスを確認します。

```console
C:\>ipconfig
Windows IP Configuration
Ethernet adapter Ethernet:
   Connection-specific DNS Suffix  . :
   Link-local IPv6 Address . . . . . : fe80::c8b6:db13:d1e8:b13b%3
   Autoconfiguration IPv4 Address. . : 169.182.1.1
   Subnet Mask . . . . . . . . . . . : 255.255.0.0
   Default Gateway . . . . . . . . . :
```

2. ホスト システムの IP アドレスを記録します。 \_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_

**-&gt; ターゲット システム**

3. ターゲット システムでコマンド プロンプトを開きを使用して、 **ping**コマンドを 2 つのシステム間のネットワーク接続を確認します。 169.182.1.1 サンプル出力に表示されるのではなく、記録したホスト システムの実際の IP アドレスを使用します。

```console
C:\> ping 169.182.1.1

Pinging 169.182.1.1 with 32 bytes of data:
Reply from 169.182.1.1: bytes=32 time=1ms TTL=255
Reply from 169.182.1.1: bytes=32 time<1ms TTL=255
Reply from 169.182.1.1: bytes=32 time<1ms TTL=255
Reply from 169.182.1.1: bytes=32 time<1ms TTL=255

Ping statistics for 169.182.1.1:
    Packets: Sent = 4, Received = 4, Lost = 0 (0% loss),
Approximate round trip times in milli-seconds:
    Minimum = 0ms, Maximum = 1ms, Average = 0ms
```

カーネル モードの次の手順を実行して、ターゲット システムでのデバッグを有効にします。

> [!IMPORTANT]
> BCDEdit を使用してブート情報を変更する前に、テスト用のコンピューターの BitLocker とセキュア ブートなどの Windows セキュリティ機能を一時的に中断する必要があります。
> テストが完了すると、これらのセキュリティ機能を再度有効にし、適切なセキュリティ機能を無効にするテスト PC を管理します。

1. ターゲット コンピューターで、管理者としてコマンド プロンプト ウィンドウを開きます。 デバッグを有効にするには、このコマンドを入力します。

    ```console
    C:\> bcdedit /set {default} DEBUG YES
    ```

2. テスト署名を有効にするには、このコマンドを入力します。

    ```console
    C:\> bcdedit /set TESTSIGNING ON 
    ```


3. ホスト システムの IP アドレスを設定するには、このコマンドを入力します。 前のないように記録したホスト システムの IP アドレスを使用します。

    ```console
    C:\> bcdedit /dbgsettings net hostip:192.168.1.1 port:50000 key:1.2.3.4
    ```

**警告**接続のセキュリティを向上させ、ランダムなクライアントのデバッガーの接続要求のリスクを減らす、生成されたランダムなキーを自動の使用を検討してください。 詳細については、[設定を KDNET ネットワーク カーネル デバッグを自動的に](setting-up-a-network-debugging-connection-automatically.md)を参照してください。

4. Dbgsettings が正しく設定されていることを確認するには、このコマンドを入力します。

    ```console
    C:\> bcdedit /dbgsettings
    key                     1.2.3.4
    debugtype               NET
    hostip                  169.168.1.1
    port                    50000
    dhcp                    Yes
    The operation completed successfully.
    ```

**注:**  
**ファイアウォールとデバッガー**

確認の場合は、ファイアウォールからポップアップ メッセージを受信して、デバッガーを使用する、 **3 つすべて**ボックス。

![windows セキュリティの警告 - windows ファイアウォールがこのアプリの一部の機能をブロックします。 ](images/debuglab-image-firewall-dialog-box.png)



**&lt;ホスト システムで**

1. ホスト コンピューターで、管理者としてコマンド プロンプト ウィンドウを開きます。 X64 を使用して、WinDbg.exe Windows キットのインストールの一部としてインストールされた Windows Driver Kit (WDK) からのバージョン。 既定ではこちらです。

    ```console
    C:\> Cd C:\Program Files(x86)\Windows Kits\10\Debuggers\x64 
    ```

> [!NOTE]
> このラボでは、両方の Pc に、ターゲットとホストの両方で Windows の 64 ビット バージョンが実行されていることを前提としています。 場合はそうでない、最適な方法では、ターゲットを実行しているホストでツールの同じ「ビット数」を実行します。 たとえば、ターゲットが実行されている 32 ビット Windows では、ホスト上で 32 のバージョンのデバッガーを実行している場合です。 詳細については、[32 ビットまたは 64 ビット デバッグ ツールを選択する](choosing-a-32-bit-or-64-bit-debugger-package.md)を参照してください。
> 

2. 次のコマンドを使用してデバッグするリモート ユーザーに、WinDbg を起動します。 キーとポートの値は、先ほど設定と一致でターゲット BCDEdit を使用します。

    ```console
    WinDbg –k net:port=50000,key=1.2.3.4
    ```

**-&gt;ターゲット システム**

ターゲット システムを再起動します。

**&lt;ホスト システムで**

1 分または 2 では、ホスト システムで、デバッグ出力が表示されます。

```dbgcmd
Microsoft (R) Windows Debugger Version 10.0.17074.1002 AMD64
Copyright (c) Microsoft Corporation. All rights reserved.

Using NET for debugging
Opened WinSock 2.0
Waiting to reconnect...
Connected to target 169.182.1.1 on port 50005 on local IP 169.182.1.2
You can get the target MAC address by running .kdtargetmac command.
Connected to Windows 10 16299 x64 target at (Wed Feb 28 17:16:23.051 2018 (UTC - 8:00)), ptr64 TRUE
Kernel Debugger connection established.  (Initial Breakpoint requested)
Symbol search path is: srv*
Executable search path is: 
Windows 10 Kernel Version 16299 MP (4 procs) Free x64
Product: WinNt, suite: TerminalServer SingleUserTS
Built by: 16299.15.amd64fre.rs3_release.170928-1534
Machine Name:
Kernel base = 0xfffff800`9540d000 PsLoadedModuleList = 0xfffff800`95774110
Debug session time: Wed Feb 28 17:16:23.816 2018 (UTC - 8:00)
System Uptime: 0 days 0:00:20.534
```

デバッガー コマンド ウィンドウは、WinDbg で主にデバッグ情報ウィンドウです。 デバッガー コマンドを入力し、このウィンドウで、コマンドの出力を表示できます。

デバッガー コマンド ウィンドウは、2 つのペインに分割されます。 ウィンドウの下部にある小さいウィンドウ (コマンドのエントリのウィンドウ) でのコマンドを入力し、ウィンドウの上部にある大きいウィンドウで、コマンドの出力を表示します。

コマンドのエントリ ウィンドウで上向きの矢印と下向きコマンド履歴をスクロールする方向キー。 コマンドが表示されたら、それを編集またはキーを押して**ENTER**コマンドを実行します。

## <a name="span-idkernelmodedebuggingcommandsandtechniquesspanspan-idkernelmodedebuggingcommandsandtechniquesspanspan-idkernelmodedebuggingcommandsandtechniquesspansection-2-kernel-mode-debugging-commands-and-techniques"></a><span id="KernelModeDebuggingCommandsAndTechniques"></span><span id="kernelmodedebuggingcommandsandtechniques"></span><span id="KERNELMODEDEBUGGINGCOMMANDSANDTECHNIQUES"></span>セクション 2:カーネル モードのデバッグ コマンドや技法


*セクション 2 では、ターゲット システムに関する情報を表示するのにデバッグ コマンドを使用します。*

**&lt;ホスト システムで**

**.Prefer とデバッガーのマークアップ言語 (DML) を有効にする\_dml**

いくつかは、すばやく情報を収集するでクリックできるデバッガー マークアップ言語を使用してコマンドの表示テキストをデバッグします。

1. WinDBg で Ctrl + Break (Scroll Lock) を使用して、ターゲット システムで実行されているコードを中断します。 少しのターゲット システムが応答する時間がかかる場合があります。

![windows は、カーネルのライブ接続からのコマンド ウィンドウ出力の表示のデバッガーします。](images/debuglab-image-winddbg-hh.png)


2. デバッガー コマンド ウィンドウで DML を有効にするのには、次のコマンドを入力します。

```dbgcmd
0: kd> .prefer_dml 1
DML versions of commands on by default
```

***.Hh* を使用してヘルプを取得するには**

使用してコマンド ヘルプを参照にアクセスすることができます、 ***.hh*** コマンド。

3. コマンド リファレンスのヘルプを表示するには、次のコマンドを入力 **.prefer\_dml**します。

```dbgcmd
0: kd> .hh .prefer_dml
```

デバッガーのヘルプ ファイルのヘルプが表示されます、 **.prefer\_dml**コマンド。

![デバッガーのアプリケーションが表示されたヘルプの .prefer\-dml コマンド](images/debuglab-image-prefer-dml-help.png)

**ターゲット システム上の Windows のバージョンの表示**

5. 」と入力して、ターゲット システムでバージョン情報の詳細を表示、 [ **vertarget (ターゲット コンピューター バージョンの表示)** ](vertarget--show-target-computer-version-.md) WinDbg ウィンドウでコマンド。

```dbgcmd
0: kd> vertarget
Windows 10 Kernel Version 9926 MP (4 procs) Free x64
Product: WinNt, suite: TerminalServer SingleUserTS
Built by: 9926.0.amd64fre.fbl_awesome1501.150119-1648
Machine Name: ""
Kernel base = 0xfffff801`8d283000 PsLoadedModuleList = 0xfffff801`8d58aef0
Debug session time: Fri Feb 20 10:15:17.807 2015 (UTC - 8:00)
System Uptime: 0 days 01:31:58.931
```

**読み込まれたモジュールを一覧表示します。**

6. 」と入力して、読み込まれたモジュールを表示することで、適切なカーネル モード プロセスを使用していることを確認することができます、 [ **lm (読み込まれたモジュールの一覧)** ](lm--list-loaded-modules-.md) WinDbg ウィンドウでコマンド。

```dbgcmd
0: Kd> lm
start             end                 module name
fffff801`09200000 fffff801`0925f000   volmgrx    (no symbols)           
fffff801`09261000 fffff801`092de000   mcupdate_GenuineIntel   (no symbols)           
fffff801`092de000 fffff801`092ec000   werkernel   (export symbols)       werkernel.sys
fffff801`092ec000 fffff801`0934d000   CLFS       (export symbols)       CLFS.SYS
fffff801`0934d000 fffff801`0936f000   tm         (export symbols)       tm.sys
fffff801`0936f000 fffff801`09384000   PSHED      (export symbols)       PSHED.dll
fffff801`09384000 fffff801`0938e000   BOOTVID    (export symbols)       BOOTVID.dll
fffff801`0938e000 fffff801`093f7000   spaceport   (no symbols)           
fffff801`09400000 fffff801`094cf000   Wdf01000   (no symbols)           
fffff801`094d9000 fffff801`09561000   CI         (export symbols)       CI.dll
...
```

**注**が省略されている出力は、"... で示されます。 "このラボで。



7. 特定のモジュールに関する詳細情報を要求するには、v (詳細) オプションに示すようを使用します。

```dbgcmd
0: Kd> lm v m tcpip
Browse full module list
start             end                 module name
fffff801`09eeb000 fffff801`0a157000   tcpip      (no symbols)           
    Loaded symbol image file: tcpip.sys
    Image path: \SystemRoot\System32\drivers\tcpip.sys
    Image name: tcpip.sys
    Browse all global symbols  functions  data
    Timestamp:        Sun Nov 09 18:59:03 2014 (546029F7)
    CheckSum:         00263DB1
    ImageSize:        0026C000
    Translations:     0000.04b0 0000.04e4 0409.04b0 0409.04e4

Unable to enumerate user-mode unloaded modules, Win32 error 0n30
```

8. まだ読み込まれているシンボルとシンボルのパスを設定するがある、あるので限定された情報は、デバッガーで使用できます。

## <a name="span-iddownloadspanspan-iddownloadspanspan-iddownloadspansection-3-download-and-build-the-kmdf-universal-echo-driver"></a><span id="Download"></span><span id="download"></span><span id="DOWNLOAD"></span>セクション 3:ダウンロードして、KMDF ユニバーサル エコー ドライバーのビルド

*セクション 3 では、ダウンロードし、KMDF ユニバーサル エコーのドライバーをビルドします。*

通常は操作することで独自のドライバー コード WinDbg を使用する場合。 WinDbg の操作に慣れる、KMDF テンプレート Echo サンプル ドライバーを使用します。 使用可能なソース コードにも可能になります WinDbg で表示される情報を理解しやすくします。 さらに、このサンプルを使用して、シングル ステップ ネイティブのカーネル モード コードを示しています。 この手法を非常に複雑なカーネル モード コードの問題のデバッグで役に立つことができます。

をダウンロードして、Echo サンプル オーディオ ドライバーをビルドするには、次の手順を実行します。

1.  **ダウンロードして、GitHub から KMDF Echo サンプルを抽出**

    ここで、GitHub でエコー サンプルを表示するのにブラウザーを使用できます。

    [https://github.com/Microsoft/Windows-driver-samples/tree/97cf5197cf5b882b2c689d8dc2b555f2edf8f418/general/echo/kmdf](https://github.com/Microsoft/Windows-driver-samples/blob/97cf5197cf5b882b2c689d8dc2b555f2edf8f418/general/echo/kmdf/ReadMe.md)

    このサンプルでは参照できます。

    <https://github.com/Microsoft/Windows-driver-samples/blob/97cf5197cf5b882b2c689d8dc2b555f2edf8f418/general/echo/kmdf/ReadMe.md>

    すべてのユニバーサル ドライバーのサンプルは、ここを参照できます。

    <https://github.com/Microsoft/Windows-driver-samples>

    KMDF Echo サンプルについては、[全般] フォルダーにあります。

    ![windows ドライバーのサンプル 全般 フォルダーおよび zip のダウンロード ボタンを強調表示](images/debuglab-image-github.png)

    a.  このラボでは、ユニバーサル ドライバー サンプルは、1 つの zip ファイルをダウンロードする方法を示します。

    <https://github.com/Microsoft/Windows-driver-samples/archive/master.zip>

    b.  Master.zip ファイルをローカル ハード ドライブにダウンロードします。

    c. 右クリックして*Windows ドライバーのサンプル-master.zip*、選択**すべて展開**します。 新しいフォルダーを指定するか、抽出したファイルを保存する既存のサブスクリプションへの参照します。 たとえば、指定する*c:\\DriverSamples\\* として新しいファイルが抽出先フォルダーです。

    d. ファイルが抽出されると、次のサブフォルダーに移動します。

    *C:\\DriverSamples\\全般\\エコー\\kmdf*

2.  **Visual Studio でのドライバー ソリューションを開く**

    Microsoft Visual studio で次のようにクリックします**ファイル** &gt; **オープン** &gt; **プロジェクト/ソリューション.。** を抽出したファイルを含むフォルダーに移動します (たとえば、 *c:\\DriverSamples\\全般\\エコー\\kmdf*)。 ダブルクリックして、 *kmdfecho*ソリューション ファイルを開きます。

    Visual Studio で、ソリューション エクスプ ローラーを見つけます。 (これがまだ開いていない場合は、選択**ソリューション エクスプ ローラー**から、**ビュー**メニュー)。ソリューション エクスプ ローラーでは、3 つのプロジェクトを含む 1 つのソリューションを確認できます。

    ![visual studio と kmdfecho プロジェクトから読み込まれた device.c ファイル](images/debuglab-image-echo-visual-studio.png)

3.  **サンプルの構成とプラットフォームを設定します。**

    ソリューション エクスプ ローラーで右クリックして**ソリューション 'kmdfecho' (3 プロジェクト)**、選択**Configuration Manager**します。 構成とプラットフォームの設定は、3 つのプロジェクトの同じことを確認します。 既定では、構成が"Win10 Debug"に設定し、プラットフォームのすべてのプロジェクトの"Win64"に設定されています。 任意の構成または 1 つのプロジェクトのプラットフォームの変更を加えた場合は、残りの 3 つのプロジェクトに対しても同じ変更を行う必要があります。

4.  **ランタイム ライブラリを設定します。**

    ランタイム ライブラリの設定 - エコー ドライバーのプロパティ ページを開き、検索**C/C++** &gt; **コード生成**します。  ランタイム ライブラリを DLL のバージョンから以外の DLL バージョンに変更します。 この設定がないとは別に、対象のコンピュータに MSVC ランタイムをインストールする必要です。

    ![ランタイム ライブラリの設定を強調表示エコー プロパティ ページ](images/debuglab-image-echoapp-properties.png)

5.  **ドライバーの署名を確認します。**

    また、ドライバーのプロパティで確認**ドライバーの署名** &gt; **記号モード**「テスト サインオン」に設定されています。 Windows では、ドライバーが署名されている必要があるために必要です。

    ![エコー プロパティ ページ、サインイン モード設定を強調表示](images/debuglab-image-echoapp-driver-signing.png)

6.  **Visual Studio を使用してサンプルをビルドします。**

    Visual Studio で、次のようにクリックします。**ビルド** &gt; **ソリューションのビルド**します。

    すべてうまくいけば、windows のビルドは 3 つすべてのプロジェクトのビルドが成功したことを示すメッセージを表示する必要があります。

7.  **組み込みのドライバー ファイルを見つけます**

    ファイル エクスプ ローラーでは、サンプルの抽出されたファイルを含むフォルダーに移動します。 移動するなど、 *c:\\DriverSamples\\全般\\エコー\\kmdf*前に指定したフォルダーがある場合、します。 コンパイル済みのドライバー ファイルの場所がで選択した構成とプラットフォームの設定によって異なります、そのフォルダー内、 **Configuration Manager**します。 など、既定の設定のままの場合、コンパイル済みのドライバー ファイルに保存という名前のフォルダー  *\\x64\\デバッグ*64 ビットの場合は、ビルドをデバッグします。

    Autosync ドライバーのビルド済みのファイルを含むフォルダーに移動します。

    *C:\\DriverSamples\\全般\\エコー\\kmdf\\ドライバー\\AutoSync\\x64\\デバッグ*します。 

    フォルダーには、これらのファイルを含める必要があります。

    | ファイル     | 説明                                                                       |
    |----------|-----------------------------------------------------------------------------------|
    | Echo.sys | ドライバー ファイルです。                                                                  |
    | Echo.inf | ドライバーをインストールするために必要な情報が含まれる情報 (INF) ファイル。 |

    さらに、echoapp.exe ファイルが作成されており、その必要がありますにあります。*C:\\DriverSamples\\全般\\エコー\\kmdf\\exe\\x64\\デバッグ*

    | ファイル        | 説明                                                                       |
    |-------------|-----------------------------------------------------------------------------------|
    | EchoApp.exe | Echo.sys ドライバーと通信するコマンド プロンプト テストの実行可能ファイルです。 |     

8.  USB ドライブを検索またはホストから、ターゲット システムに組み込みのドライバー ファイル、およびテスト EchoApp をコピーするネットワーク共有を設定します。

次のセクションはターゲット システムにコードをコピーおよびしインストール ドライバーをテストします。

## <a name="span-idinstallspanspan-idinstallspanspan-idinstallspansection-4-install-the-kmdf-echo-driver-sample-on-the-target-system"></a><span id="Install"></span><span id="install"></span><span id="INSTALL"></span>セクション 4:ターゲット システムに KMDF エコー ドライバーのサンプルをインストールします。

*セクション 4 では、devcon を使用して、echo サンプル ドライバーをインストールします。*

**-&gt; ターゲット システム**

ドライバーをインストールするコンピューターと呼ばれる、*ターゲット コンピューター*または*テスト コンピューター*します。 通常、これを開発およびドライバー パッケージをビルド コンピューターから別のコンピューターです。 開発およびドライバーをビルドする場所のコンピューターと呼ばれる、*ホスト コンピューター*します。

ターゲット コンピューターに移行してドライバー パッケージ、ドライバーをインストールするプロセスと呼ばれます*展開*ドライバー。 エコー ドライバーのサンプルは、自動または手動で展開できます。

ドライバーを手動で展開する前に、テスト署名を有効にして、ターゲット コンピューターを準備する必要があります。 また、DevCon ツールを WDK のインストールで検索する必要があります。 その後、組み込みのドライバーのサンプルを実行する準備ができました。

ターゲット システム上のドライバーをインストールするには、次の手順を実行します。

**テストを有効にする署名されたドライバー**

テストを実行する機能を有効にするには、ドライバーが署名。

a.  Windows の設定を開きます。

b.  更新プログラムおよびセキュリティ、 **Recovery**します。

c. 高度な起動 で、次のようにクリックします。**今すぐ再起動**します。

d. PC が再起動すると、選択**のスタートアップ オプション**します。 Windows 10 では、次のように選択します。**トラブルシューティング** > **詳細オプション** > **スタートアップ設定**、[再起動] ボタンをクリックします。 

e. キーを押してドライバー署名の強制を無効にするを選択して、 **F7**キー。

f. ターゲット コンピューターを再起動します。


**&lt;ホスト システムで**

WDK のインストールの Tools フォルダーに移動し、DevCon ツールを見つけます。 たとえば、次のフォルダーを探します。

*C:\\Program Files (x86)\\Windows キット\\10.0\\ツール\\x64\\devcon.exe*に構築されたドライバー パッケージのターゲット フォルダーを作成 (たとえば、 *C:\\EchoDriver*)。 ホスト コンピューターで既に説明した組み込みのドライバーからのすべてのファイルをコピーし、ターゲット コンピューター上に作成したフォルダーに保存します。

ホスト システムに .cer 証明書を探し、組み込みのドライバー ファイルを含むフォルダー内のホスト コンピューター上の同じフォルダー内にあります。 対象のコンピューターに証明書ファイルを右クリックし、をクリックして**インストール**、テスト証明書をインストールする指示に従います。

ターゲット コンピューターの設定の詳細な手順について必要がある場合は、[手動ドライバーの展開のコンピューターを準備する](../develop/preparing-a-computer-for-manual-driver-deployment.md)を参照してください。

**-&gt; ターゲット システム**

**ドライバーをインストールします。**

次の手順では、インストールして、ドライバーのサンプルをテストする方法を示します。 ここで示しているのは、ドライバーのインストールに使う devcon ツールの一般的な構文です。

*devcon install &lt;INF ファイル&gt; &lt;ハードウェア ID&gt;*

このドライバーのインストールに必要な INF ファイル*echo.inf*します。 Inf ファイルにはインストールするためのハードウェア ID が含まれています、 *echo.sys*します。 ハードウェア ID は、echo サンプル**ルート\\エコー**します。

ターゲット コンピューターで、管理者としてコマンド プロンプト ウィンドウを開きます。 ドライバー パッケージ フォルダーに移動し、次のコマンドを入力します。

**devcon インストール echo.inf ルート\\エコー**エラー メッセージが表示された場合*devcon*へのパスを追加して認識されていない、 *devcon*ツール。 たとえば、という名前のフォルダーにコピーした*c:\\ツール*から次のコマンドを使用して再試行してください。

**c:\\ツール\\devcon インストール echo.inf ルート\\エコー**テスト ドライバーが署名されていない、ドライバーであることを示すダイアログ ボックスが表示されます。 **[かまわず続行]** をクリックして続行します。

![windows セキュリティの警告 - windows は、このドライバー ソフトウェアの発行元を確認できません](images/debuglab-image-install-security-warning.png)

詳細な手順についてを参照してください。[ドライバーの展開、テスト、およびデバッグ用コンピューターの構成](https://docs.microsoft.com/windows-hardware/drivers/gettingstarted/provision-a-target-computer-wdk-8-1)します。

ドライバーのサンプルを正常にインストールした後で、テストする準備ができましたがようになりました。

**デバイス マネージャーでのドライバーを確認します。**

コマンド プロンプト ウィンドウで、対象のコンピューターに次のように入力します。 **devmgmt**デバイス マネージャーを開きます。 デバイス マネージャーで、[表示] メニューには、種類別のデバイスを選択します。 デバイス ツリーで探します*サンプル WDF エコー ドライバー*サンプル [デバイス] ノードでします。

![強調表示されているサンプルの wdf エコー ドライバーを使用したデバイス マネージャーのツリー](images/debuglab-image-device-manager-echo.png)

**ドライバーをテストします。**

型**echoapp**ドライバーが機能していることを確認するテスト echo アプリを起動します。

```dbgcmd
C:\Samples\KMDF_Echo_Sample> echoapp
DevicePath: \\?\root#sample#0005#{cdc35b6e-0be4-4936-bf5f-5537380a7c1a}
Opened device successfully
512 Pattern Bytes Written successfully
512 Pattern Bytes Read successfully
Pattern Verified successfully
30720 Pattern Bytes Written successfully
30720 Pattern Bytes Read successfully
Pattern Verified successfully
```

## <a name="span-idusewindbgtodisplayinformationspanspan-idusewindbgtodisplayinformationspanspan-idusewindbgtodisplayinformationspansection-5-use-windbg-to-display-information-about-the-driver"></a><span id="UseWinDbgToDisplayInformation"></span><span id="usewindbgtodisplayinformation"></span><span id="USEWINDBGTODISPLAYINFORMATION"></span>セクション 5:WinDbg を使用して、ドライバーに関する情報を表示するには

*セクション 5 では、シンボル パスを設定し、カーネル デバッガー コマンドを使用して、KMDF echo サンプル ドライバーに関する情報を表示します。*

次の手順を実行することによって、ドライバーに関する情報を表示します。

**&lt;ホスト システムで**

1.  デバッガーが閉じている場合は、もう一度、管理者コマンド プロンプト ウィンドウで、次のコマンドを使用してを開きます。

    ```dbgcmd
    WinDbg -k net:port=50000,key=1.2.3.4
    ```

2.  Ctrl + Break (Scroll Lock) を使用して、ターゲット システムで実行されているコードを中断します。

**シンボル パスを設定します。**

1.  WinDbg の環境で Microsoft シンボル サーバーにシンボル パスを設定するには、使用、 **.symfix**コマンド。

    ```dbgcmd
    0: kd> .symfix
    ```

2.  ローカル シンボルを使用する、ローカル シンボルの場所を追加する追加のパスを使用して、 **.sympath +** し **.reload/f**します。

    ```dbgcmd
    0: kd> .sympath+ C:\DriverSamples\general\echo\kmdf
    0: kd> .reload /f
    ```

    **注**、 **.reload**コマンドと、 **/f** force オプションが指定したモジュールのすべてのシンボル情報を削除し、シンボルを再読み込みします。 場合によっては、このコマンドも再読み込みまたはモジュール自体がアンロードされます。



**注**WinDbg を提供する高度な機能を使用する適切なシンボルを読み込む必要があります。 シンボルが正しく構成されていない場合、シンボルに依存する機能を使用しようとしたときに、シンボルが使用できないことを示すメッセージが届きます。

```dbgcmd
0:000> dv
Unable to enumerate locals, HRESULT 0x80004005
Private symbols (symbols.pri) are required for locals.
Type “.hh dbgerr005” for details.
```



**注:**  
**シンボル サーバー**

シンボルを使用するために使用する方法を数多くあります。 多くの状況では、必要なときに、Microsoft が提供するシンボル サーバーからアクセス シンボルに PC を構成できます。 このチュートリアルでは、このアプローチを使用することを前提としています。 環境内でシンボルが別の場所にいる場合は、その場所を使用する手順を変更します。 詳細については、[シンボル ストアとシンボル サーバー](symbol-stores-and-symbol-servers.md)を参照してください。



**注:**  
**ソース コードのシンボルの要件を理解します。**

ソースのデバッグを実行するには、バイナリのチェック (デバッグ) バージョンをビルドする必要があります。 コンパイラでは、シンボル ファイル (.pdb ファイル) を作成します。 これらのシンボル ファイルは、バイナリの命令がソース行に対応させる方法をデバッガーに表示されます。 実際のソース ファイル自体も、デバッガーにアクセスできる必要があります。

シンボル ファイルでは、ソース コードのテキストは含まれません。 デバッグをお勧め、リンカーは、コードを最適化していない場合。 ソースのデバッグとローカル変数へのアクセスより難しくなると、コードが最適化されている場合もほぼ不可能です。 でローカル変数またはソース行の表示に関する問題が発生する場合は、次のビルド オプションを設定します。

```console
set COMPILE_DEBUG=1
set ENABLE_OPTIMIZER=0
```



1. エコー ドライバーに関する情報を表示するデバッガーの [コマンド] 領域で、次を入力します。

   ```dbgcmd
   0: kd> lm m echo* v
   Browse full module list
   start             end                 module name
   fffff801`4ae80000 fffff801`4ae89000   ECHO       (private pdb symbols)  C:\Samples\KMDF_ECHO_SAMPLE\echo.pdb
       Loaded symbol image file: ECHO.sys
       Image path: \SystemRoot\system32\DRIVERS\ECHO.sys
       Image name: ECHO.sys
   ...  
   ```

   詳しくは、[ **lm**](lm--list-loaded-modules-.md)を参照してください。

2. 設定するために必要に応じて\_dml = 1 前の出力の一部の要素は、ホット リンクをクリックすることができます。 をクリックして、*リンクのシンボル参照のすべてのグローバル*デバッグ、文字で始まる項目シンボルに関する情報を表示する出力の"a"です。

   ```dbgcmd
   0: kd> x /D Echo!a*
   ```

3. Echo サンプルが文字で始まるすべてのシンボルが含まれていない結局のところ、"a", ので、エコーありで開始エコー ドライバーに関連付けられているシンボルのすべてに関する情報を表示する入力 * * エコー x!エコー\\* * *。

   ```dbgcmd
   0: kd> x ECHO!Echo*
   fffff801`0bf95690 ECHO!EchoEvtIoQueueContextDestroy (void *)
   fffff801`0bf95000 ECHO!EchoEvtDeviceSelfManagedIoStart (struct WDFDEVICE__ *)
   fffff801`0bf95ac0 ECHO!EchoEvtTimerFunc (struct WDFTIMER__ *)
   fffff801`0bf9b120 ECHO!EchoEvtDeviceSelfManagedIoSuspend (struct WDFDEVICE__ *)
   ...
   ```

   詳しくは、[ **(シンボルを調べる) x**](x--examine-symbols-.md)を参照してください。

4. **! Lmi**拡張機能には、モジュールに関する情報が表示されます。 型 **! lmi エコー**します。 出力は、下に表示されるテキストのようになります。

   ```dbgcmd
   0: kd> !lmi echo
   Loaded Module Info: [echo] 
            Module: ECHO
      Base Address: fffff8010bf94000
        Image Name: ECHO.sys
   … 
   ```

5. 使用して、 **! dh**拡張機能を次に示すようにヘッダー情報を表示します。

   ```dbgcmd
   0: kd> !dh echo

   File Type: EXECUTABLE IMAGE
   FILE HEADER VALUES
        14C machine (i386)
          6 number of sections
   54AD8A42 time date stamp Wed Jan 07 11:34:26 2015
   ...
   ```

6. **デバッグのマスクを設定**

   すべてのデバッグ対象システムからメッセージを既定のデバッグのビット マスクを変更するには、次に表示される、デバッガーの種類。

   ```dbgcmd
   0: kd> ed nt!Kd_DEFAULT_MASK  0xFFFFFFFF
   ```

   0 xffffffff のマスクを使用すると、一部のドライバーは追加情報を表示します。 表示される情報量を削減したい場合は、0x00000000 にマスクを設定します。

   ```dbgcmd
   0: kd> ed nt!Kd_DEFAULT_MASK  0x00000000
   ```

   表示する dd コマンドを使用してでは、マスクがすべてのデバッガーのメッセージを表示する設定を確認します。 

   ```dbgcmd
   0: kd> dd nt!kd_DEFAULT_MASK 
   fffff802`bb4057c0  ffffffff 00000000 00000000 00000000
   fffff802`bb4057d0  00000000 00000000 00000000 00000000
   fffff802`bb4057e0  00000001 00000000 00000000 00000000
   fffff802`bb4057f0  00000000 00000000 00000000 00000000
   fffff802`bb405800  00000000 00000000 00000000 00000000
   fffff802`bb405810  00000000 00000000 00000000 00000000
   fffff802`bb405820  00000000 00000000 00000000 00000000
   fffff802`bb405830  00000000 00000000 00000000 00000000
   ```


## <a name="span-iddisplayingtheplugandplaydevicetreespanspan-iddisplayingtheplugandplaydevicetreespanspan-iddisplayingtheplugandplaydevicetreespansection-6-displaying-plug-and-play-device-tree-information"></a><span id="DisplayingThePlugAndPlayDeviceTree"></span><span id="displayingtheplugandplaydevicetree"></span><span id="DISPLAYINGTHEPLUGANDPLAYDEVICETREE"></span>セクション 6:プラグ アンド プレイ デバイス ツリーの情報を表示します。

*セクション 6 では、echo サンプルのデバイス ドライバーに関する情報とプラグ アンド プレイ デバイス ツリーに存在する場所が表示されます。*

プラグ アンド プレイ デバイス ツリーで、デバイス ドライバーに関する情報は、トラブルシューティングに役立ちます。 たとえば、デバイス ドライバーが、デバイス ツリーに常駐していない場合はデバイス ドライバーのインストールの問題。

デバイス ノードのデバッグ拡張機能の詳細については、[ **! devnode**](-devnode.md)を参照してください。

**&lt;ホスト システムで**

1. プラグ アンド プレイ デバイス ツリー内のすべてのデバイス ノードを表示するには、入力、 **! devnode 0 1**コマンド。

   ```dbgcmd
   0: kd> !devnode 0 1
   Dumping IopRootDeviceNode (= 0xffffe0005a3a8d30)
   DevNode 0xffffe0005a3a8d30 for PDO 0xffffe0005a3a9e50
     InstancePath is "HTREE\ROOT\0"
     State = DeviceNodeStarted (0x308)
     Previous State = DeviceNodeEnumerateCompletion (0x30d)
     DevNode 0xffffe0005a3a3d30 for PDO 0xffffe0005a3a4e50
       InstancePath is "ROOT\volmgr\0000"
       ServiceName is "volmgr"
       State = DeviceNodeStarted (0x308)
       Previous State = DeviceNodeEnumerateCompletion (0x30d)
       DevNode 0xffffe0005a324560 for PDO 0xffffe0005bd95ca0…
   …
   ```

2. Ctrl キーを押しながら F キーを使用して、デバイス ドライバーの名前を探すように生成される出力で検索する*エコー*します。

   ![検索対象の用語のエコーを表示するダイアログ ボックスを検索します。](images/debuglab-image-find-dialog.png)

3. エコーのデバイス ドライバーを読み込む必要があります。 使用して、 **! devnode 0 1 エコー**コマンドを次に示すように、エコー デバイス ドライバに関連付けられたプラグ アンド プレイ情報を表示します。

   ```dbgcmd
   0: Kd> !devnode 0 1 echo
   Dumping IopRootDeviceNode (= 0xffffe0007b725d30)
   DevNode 0xffffe0007b71a630 for PDO 0xffffe0007b71a960
     InstancePath is "ROOT\SAMPLE\0000"
     ServiceName is "ECHO"
     State = DeviceNodeStarted (0x308)
     Previous State = DeviceNodeEnumerateCompletion (0x30d)
   …
   ```

4. PDO ドライバーの実行中のインスタンスに関連付けられているが、前のコマンドに表示される出力に含まれています、この例では*0xffffe0007b71a960*します。 入力、 **! devobj**<em>&lt;PDO アドレス&gt;</em>エコーのデバイス ドライバに関連付けられているプラグ アンド プレイの情報を表示するコマンド。 されるアドレスを使用して、PDO **! devnode** PC では、ここで示すように 1 つない上を表示します。

   ```dbgcmd
   0: kd> !devobj 0xffffe0007b71a960
   Device object (ffffe0007b71a960) is for:
    0000000e \Driver\PnpManager DriverObject ffffe0007b727e60
   Current Irp 00000000 RefCount 0 Type 00000004 Flags 00001040
   Dacl ffffc102c9b36031 DevExt 00000000 DevObjExt ffffe0007b71aab0 DevNode ffffe0007b71a630 
   ExtensionFlags (0x00000800)  DOE_DEFAULT_SD_PRESENT
   Characteristics (0x00000180)  FILE_AUTOGENERATED_DEVICE_NAME, FILE_DEVICE_SECURE_OPEN
   AttachedDevice (Upper) ffffe000801fee20 \Driver\ECHO
   Device queue is not busy.
   ```

5. 出力が表示される、 **! devnode 0 1**コマンドには、ドライバーの実行中のインスタンスに関連付けられている PDO アドレスが含まれています、この例では*0xffffe0007b71a960*します。 入力、 **! devstack**<em>&lt;PDO アドレス&gt;</em>デバイス ドライバに関連付けられているプラグ アンド プレイの情報を表示するコマンド。 されるアドレスを使用して、PDO **! devnode** PC のない、次のように表示されます。

   ```dbgcmd
   0: kd> !devstack 0xffffe0007b71a960
     !DevObj           !DrvObj            !DevExt           ObjectName
     ffffe000801fee20  \Driver\ECHO       ffffe0007f72eff0  
   > ffffe0007b71a960  \Driver\PnpManager 00000000  0000000e
   !DevNode ffffe0007b71a630 :
     DeviceInst is "ROOT\SAMPLE\0000"
     ServiceName is "ECHO"
   ```

出力は、非常に単純なデバイス ドライバー スタックがあることを示しています。 エコー ドライバーでは、PnPManager ノードの子です。 PnPManager は、ルート ノードです。

\Driver\ECHO      

\Driver\PnpManager

この図より複雑なデバイス ノード ツリーを示しています。

![約 20 のノードを持つデバイス ノード ツリー](images/debuglab-image-device-node-tree.png)

**注**より複雑なドライバー スタックの詳細については、[ドライバー スタック](https://msdn.microsoft.com/library/windows/hardware/hh439632)と[デバイス ノードとデバイス スタック](https://msdn.microsoft.com/library/windows/hardware/ff554721)を参照してください。



## <a name="span-idworkingwithbreakpointsspanspan-idworkingwithbreakpointsspanspan-idworkingwithbreakpointsspansection-7-working-with-breakpoints-and-source-code"></a><span id="WorkingWithBreakpoints"></span><span id="workingwithbreakpoints"></span><span id="WORKINGWITHBREAKPOINTS"></span>セクション 7:ブレークポイントとソース コードを使用します。

*セクション 7 では、ブレークポイントとカーネル モードのソース コードを 1 つの手順を設定します。*

**注:**  
**コマンドを使用してブレークポイントの設定**

コードをステップ実行し、リアルタイムでの変数の値を確認するには、ブレークポイントを有効にして、ソース コードへのパスを設定する必要があります。

ブレークポイントを使用して、特定のコード行でコードの実行を停止します。 ことができますし、ステップ前進コードでその特定のセクションのコードをデバッグする、その時点から。

デバッグ コマンドを使用してブレークポイントを設定する、次のいずれかの操作を使用して**b**コマンド。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>bp</p></td>
<td align="left"><p>内にあるモジュールがアンロードされるまでアクティブになるブレークポイントを設定します。</p></td>
</tr>
<tr class="even">
<td align="left"><p>bu</p></td>
<td align="left"><p>未解決のモジュールが読み込まれていないと、モジュールを再読み込み時に再度有効にするブレークポイントを設定します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>bm</p></td>
<td align="left"><p>シンボルのブレークポイントを設定します。 このコマンドが bu または、bp を適切に使用でき、ワイルドカード * (など、クラスのすべてのメソッド) と一致するすべてのシンボルにブレークポイントを設定するためです。</p></td>
</tr>
</tbody>
</table>





詳細については、次を参照してください。 [WinDbg でソース コードをデバッグ](source-window.md)デバッグ リファレンス ドキュメント。

**&lt;ホスト システムで**

1.  WinDbg UI を使用していることを確認**デバッグ** &gt; **ソース モード**WinDbg の現在のセッションで有効にします。

2.  ソース パスをローカルのコードの場所を追加するには、次のコマンドを入力します。

    ```dbgcmd
    .srcpath+ C:\DriverSamples\KMDF_Echo_Sample\driver\AutoSync
    ```

3.  シンボル パスに、ローカル シンボルの場所を追加するには、次のコマンドを入力します。

    ```dbgcmd
    .sympath+ C:\DriverSamples\KMDF_Echo_Sample\driver\AutoSync
    ```

4.  使用して、 **x**コマンドのブレークポイントを使用する関数の名前を決定するエコー ドライバーに関連付けられているシンボルの検証をします。 ワイルド カードまたは Ctrl キーを押しながら F キーを使用して検索することができます、 **DeviceAdd**関数名。

    ```dbgcmd
    0: kd> x ECHO!EchoEvt*
    8b4c7490          ECHO!EchoEvtIoQueueContextDestroy (void *)
    8b4c7000          ECHO!EchoEvtDeviceSelfManagedIoStart (struct WDFDEVICE__ *)
    8b4c7820          ECHO!EchoEvtTimerFunc (struct WDFTIMER__ *)
    8b4cb0e0          ECHO!EchoEvtDeviceSelfManagedIoSuspend (struct WDFDEVICE__ *)
    8b4c75d0          ECHO!EchoEvtIoWrite (struct WDFQUEUE__ *, struct WDFREQUEST__ *, unsigned int)
    8b4cb170          ECHO!EchoEvtDeviceAdd (struct WDFDRIVER__ *, struct 
    …
    ```

    上記の出力に示す**DeviceAdd** 、エコー ドライバーのメソッドは*エコー!EchoEvtDeviceAdd*します。

    または、ブレークポイントの必要な関数名を検索するソース コードを確認しました。

5.  ブレークポイントを設定、 **bm**コマンドに続けて関数名、ドライバーの名前を使用して (たとえば**AddDevice**)、ブレークポイントを設定する場合は、感嘆符で区切られました。 使用します**AddDevice**読み込まれているドライバーを監視します。

    ```dbgcmd
    0: kd> bm ECHO!EchoEvtDeviceAdd
      1: fffff801`0bf9b1c0 @!"ECHO!EchoEvtDeviceAdd"
    ```

    **注:**  
    別の構文を使用するにはのような変数の設定と組み合わせて&lt;モジュール&gt;!&lt;シンボル&gt;、&lt;クラス&gt;::&lt;メソッド&gt;、'&lt;file.cpp&gt;:&lt;行番号&gt;'、または時間数をスキップ&lt;条件&gt; &lt; \#&gt;します。 詳細については、[WinDbg およびその他の Windows デバッガーでの条件付きブレークポイント](setting-a-conditional-breakpoint.md)を参照してください。



6.  」と入力して、ブレークポイントが設定されたことを確認する現在のブレークポイントを一覧表示、 **bl**コマンド。

    ```dbgcmd
    0: kd> bl
    1 e fffff801`0bf9b1c0     0001 (0001) ECHO!EchoEvtDeviceAdd
    ```

    上記の出力に"e"では、ブレークポイント番号 1 が起動を有効になっていることを示します。

7.  」と入力して、ターゲット システムでコードが実行を再開、**移動**コマンド**g**します。

8.  **-&gt; ターゲット システム**

    Windows、開き**デバイス マネージャー**アイコンを使用するか入力することで**mmc devmgmt.msc**します。 デバイス マネージャーで、展開、**サンプル**ノード。

9.  KMDF エコーのドライバー エントリを右クリックして**を無効にする** メニューから。

10. KMDF エコーのドライバー エントリをもう一度右クリックして**を有効にする** メニューから。

11. **&lt;ホスト システムで**

    ドライバーが有効にすると、 [ *AddDevice* ](https://msdn.microsoft.com/library/windows/hardware/ff540521)デバッグ ブレークポイントが起動して、ターゲット システムでドライバー コードの実行を停止する必要があります。 先頭に、実行を停止するか、ブレークポイントにヒットしたときに、 *AddDevice*ルーチン。 「1 のブレークポイントにヒット」デバッグ コマンドの出力が表示されます。

    ![サンプル コードのローカル変数とコマンド ウィンドウを表示する windbg](images/debuglab-image-breakpoint-echo-deviceadd.png)

12. 」と入力して、コードで行をステップ、 **p**コマンドまたは次の末尾に到達するまで、f10 キーを押して、 [ *AddDevice* ](https://msdn.microsoft.com/library/windows/hardware/ff540521)ルーチン。 中かっこ文字"}"のように強調表示されます。

    ![adddevice ルーチンの開始で強調表示されているかっこ文字を示すコード ウィンドウ](images/debuglab-image-breakpoint-end-deviceadd.png)

13. DeviceAdd コードが実行された後、次のセクションで、変数の状態は説明します。

**注:**  
**ブレークポイントの状態を変更します。**

既存のブレークポイントは、次のコマンドを使用して変更できます。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>bl</p></td>
<td align="left"><p>ブレークポイントが表示されます。</p></td>
</tr>
<tr class="even">
<td align="left"><p>ビジネス継続性</p></td>
<td align="left"><p>一覧からブレークポイントをクリアします。 ビジネス継続性を使用して、* すべてのブレークポイントをクリアします。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>bd</p></td>
<td align="left"><p>ブレークポイントを無効にします。 Bd を使用して、* すべてのブレークポイントを無効にします。</p></td>
</tr>
<tr class="even">
<td align="left"><p>する</p></td>
<td align="left"><p>ブレークポイントを有効にします。 使用する * すべてのブレークポイントを有効にします。</p></td>
</tr>
</tbody>
</table>



クリックしてブレークポイントも変更する代わりに、**編集** &gt; **ブレークポイント**WinDbg でします。 ブレークポイントの ダイアログ ボックスが既存のブレークポイントでのみ動作することに注意してください。 コマンドラインからは、新しいブレークポイントを設定する必要があります。



**注:**  
**メモリのアクセスのブレークポイントの設定**

メモリの場所にアクセスするときに発生するブレークポイントを設定することもできます。 使用して、 **ba** (アクセスの切断) コマンドを次の構文を使用します。

```dbgcmd
ba <access> <size> <address> {options}
```

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">オプション</th>
<th align="left">説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>E</p></td>
<td align="left"><p>(CPU では、アドレスから命令をフェッチ) したときに実行します。</p></td>
</tr>
<tr class="even">
<td align="left"><p>r</p></td>
<td align="left"><p>(CPU の読み取りまたは書き込みをアドレスに) 場合、読み取り/書き込み</p></td>
</tr>
<tr class="odd">
<td align="left"><p>W</p></td>
<td align="left"><p>書き込み (する場合、CPU は、アドレスに書き込む)</p></td>
</tr>
</tbody>
</table>



特定の時点、4 つのデータ ブレークポイントを設定することができますのみで、データを正しく配置すること、または、ブレークポイントをトリガーしないかどうかを確認するかどうかは (単語が 2 で割り切れるアドレスで終了する必要があります、dword が 4 で割り切れる必要があります、および (クワドワード)。 0 または 8 で)。

など、特定のメモリ アドレスで読み取り/書き込みのブレークポイントを設定するには、このようなコマンドを使用する可能性があります。

```dbgcmd
ba r 4 0x0003f7bf0
```



**注:**  
**デバッガー コマンド ウィンドウからコードをステップ実行**

次に使用できるコマンドを (かっこ内に表示する関連付けられたキーボード短いカット) 使用してコードをステップ実行します。

-   (Ctrl + Break) で中断 - このコマンドは、システムが実行されていて、WinDbg (カーネル デバッガーで、シーケンスは Ctrl + C) との通信に限り、システムが中断します。

-   (F7 キーまたは Ctrl + F10)、カーソル位置まで実行 – を解除し、; f7 キーを押して実行する変換元または [逆アセンブル] ウィンドウにカーソルを置きますコードの実行は、そのポイントまで実行されます。 コードの実行には、指定されたポイントが届かなかった場合は、コード実行のフロー (IF ステートメントが実行されない場合は) カーソルで示されるポイントに到達しません、WinDbg が壊れないことに注意してください。

-   ブレークポイントが発生したか、バグ チェックのようなイベントが発生するまで実行 (F5) – を実行します。

-   ステップ オーバー (F10): このコマンドは 1 つのステートメントや、一度に 1 つの命令を進めるコードが実行を実行します。 呼び出しが発生した場合はコードが実行は呼び出し経由で呼び出されたルーチンを入力しなくても渡します。 (場合、プログラミング言語は C または C++ と、WinDbg は元のモードでは、ソース モード有効にできますオンまたはオフを使用して**デバッグ**&gt;**ソース モード**)。

-   ステップ イン (F11) – する点を除いて、呼び出しの実行が呼び出されたルーチンに移動し、ステップ オーバーのようにこのコマンドは、します。

-   ステップ アウト (shift + f11): このコマンドの実行を実行して、現在の終了を実行するルーチン (呼び出し履歴内の現在の場所)。 これは、十分なルーチンを見た場合に便利です。



詳細については、次を参照してください。 [WinDbg でソース コードをデバッグ](source-window.md)デバッグ リファレンス ドキュメント。

## <a name="span-idviewingvariablesspanspan-idviewingvariablesspanspan-idviewingvariablesspansection-8-viewing-variables-and-call-stacks"></a><span id="ViewingVariables"></span><span id="viewingvariables"></span><span id="VIEWINGVARIABLES"></span>セクション 8:変数と呼び出し履歴を表示します。

*セクション 8 では、変数に関する情報を表示し、呼び出し履歴。*

このラボは、停止したことを想定しています、 [ *AddDevice* ](https://msdn.microsoft.com/library/windows/hardware/ff540521)ルーチンの前に説明したプロセスを使用します。 ここで表示する出力を表示するには、必要に応じて、前に説明した手順を繰り返します。

**&lt;ホスト システムで**

**変数を表示します。**

使用して、**ビュー** &gt; **ローカル**ローカル変数を表示するメニュー項目。

![windbg local variables window](images/debuglab-image-display-variables.png)

**グローバル変数**

グローバル変数のアドレスの場所を入力して検索できます*でしょうか。&lt;変数名&gt;* します。

**ローカル変数**

名前と特定のフレームのすべてのローカル変数の値を表示するには」と入力して、 **dv**コマンド。

```dbgcmd
0: kd> dv
         Driver = 0x00001fff`7ff9c838
     DeviceInit = 0xffffd001`51978190
         status = 0n0
```

**呼び出し履歴**

**注:**  
呼び出し履歴は、プログラム カウンターの現在の場所が原因となった関数呼び出しのチェーンです。 呼び出し履歴の最上位の関数は、現在の関数と、次の関数は、現在の関数を呼び出した関数、という具合です。

呼び出し履歴を表示するには、使用、k\*コマンド。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>サポート技術情報</p></td>
<td align="left"><p>スタックと最初の 3 つのパラメーターが表示されます。</p></td>
</tr>
<tr class="even">
<td align="left"><p>kp</p></td>
<td align="left"><p>スタックとパラメーターの完全な一覧が表示されます。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>kn</p></td>
<td align="left"><p>その横にあるフレーム情報を使用して履歴を表示することができます。</p></td>
</tr>
</tbody>
</table>





**&lt;ホスト システムで**

1. 使用可能な呼び出し履歴を保持する場合は、クリックして**ビュー** &gt; **コール スタック**を表示します。 追加情報の表示を切り替える、ウィンドウの上部にある列をクリックします。

![windbg 表示コール スタック ウィンドウ](images/debuglab-image-display-callstacks.png)

2. 使用して、 **kn**ブレーク状態にサンプルのアダプター コードのデバッグ中に呼び出し履歴を表示するコマンド。

```dbgcmd
3: kd> kn
# Child-SP          RetAddr           Call Site
00 ffffd001`51978110 fffff801`0942f55b ECHO!EchoEvtDeviceAdd+0x66 [c:\Samples\kmdf echo sample\c++\driver\autosync\driver.c @ 138]
01 (Inline Function) --------`-------- Wdf01000!FxDriverDeviceAdd::Invoke+0x30 [d:\wbrtm\minkernel\wdf\framework\shared\inc\private\common\fxdrivercallbacks.hpp @ 61]
02 ffffd001`51978150 fffff801`eed8097d Wdf01000!FxDriver::AddDevice+0xab [d:\wbrtm\minkernel\wdf\framework\shared\core\km\fxdriverkm.cpp @ 72]
03 ffffd001`51978570 fffff801`ef129423 nt!PpvUtilCallAddDevice+0x35 [d:\9142\minkernel\ntos\io\pnpmgr\verifier.c @ 104]
04 ffffd001`519785b0 fffff801`ef0c4112 nt!PnpCallAddDevice+0x63 [d:\9142\minkernel\ntos\io\pnpmgr\enum.c @ 7397]
05 ffffd001`51978630 fffff801`ef0c344f nt!PipCallDriverAddDevice+0x6e2 [d:\9142\minkernel\ntos\io\pnpmgr\enum.c @ 3390]
...
```

呼び出し履歴は、カーネル (nt) (PnP)、プラグ アンド プレイのコードを呼び出すコードを呼び出した driver framework (WDF) をその後にエコー ドライバーと呼ばれることを示しています。 **DeviceAdd**関数。

## <a name="span-iddisplayingprocessesandthreadsspanspan-iddisplayingprocessesandthreadsspanspan-iddisplayingprocessesandthreadsspansection-9-displaying-processes-and-threads"></a><span id="DisplayingProcessesAndThreads"></span><span id="displayingprocessesandthreads"></span><span id="DISPLAYINGPROCESSESANDTHREADS"></span>セクション 9:プロセスとスレッドを表示します。

### <a name="span-idprocessesspanspan-idprocessesspanspan-idprocessesspanprocesses"></a><span id="Processes"></span><span id="processes"></span><span id="PROCESSES"></span>プロセス

*セクション 9、カーネル モードで実行中のスレッドとプロセスに関する情報が表示されます。*

**注:**  
表示またはを使用して、プロセス情報を設定することができます、 [ **! プロセス**](-process.md)デバッガー拡張機能。 サウンドの再生時に使用されるプロセスを確認するブレークポイントを設定します。



1. **&lt;ホスト システムで**

   型、 **dv**コマンドに関連付けられているロケールの変数の確認を**EchoEvtIo**ルーチンが示すようにします。

   ```dbgcmd
   0: kd> dv ECHO!EchoEvtIo*
   ECHO!EchoEvtIoQueueContextDestroy
   ECHO!EchoEvtIoWrite
   ECHO!EchoEvtIoRead         
   ```

2. 使用して前のブレークポイントをクリアする * * bc \\* * *。

   ```dbgcmd
   0: kd> bc *  
   ```

3. 3. シンボルのブレークポイントを設定、 **EchoEvtIo**ルーチンは次のコマンドを使用します。

   ```dbgcmd
   0: kd> bm ECHO!EchoEvtIo*
     2: aade5490          @!”ECHO!EchoEvtIoQueueContextDestroy”
     3: aade55d0          @!”ECHO!EchoEvtIoWrite”
     4: aade54c0          @!”ECHO!EchoEvtIoRead”
   ```

4. ブレークポイントが正しく設定されていることを確認するブレークポイントの一覧を表示します。

   ```dbgcmd
   0: kd> bl
   1 e aabf0490 [c:\Samples\kmdf echo sample\c++\driver\autosync\queue.c @ 197]    0001 (0001) ECHO!EchoEvtIoQueueContextDestroy
   ...
   ```

5. 型**g**でコードが実行を再起動します。

   ```dbgcmd
   0: kd> g
   ```

6. **-&gt; ターゲット システム**

   ターゲット システムに EchoApp.exe ドライバーのテスト プログラムを実行します。

7. **&lt;ホスト システムで**

   アプリのテストを実行すると、ドライバーでの I/O ルーチンが呼び出されます。 これにより、発生するブレークポイントとターゲット システム上のドライバー コードの実行を停止します。

   ```dbgcmd
   Breakpoint 2 hit
   ECHO!EchoEvtIoWrite:
   fffff801`0bf95810 4c89442418      mov     qword ptr [rsp+18h],r8
   ```

8. 使用して、 **! プロセス**echoapp.exe の実行に関連する現在のプロセスを表示するコマンド。

   ```dbgcmd
   0: kd> !process
   PROCESS ffffe0007e6a7780
       SessionId: 1  Cid: 03c4    Peb: 7ff7cfec4000  ParentCid: 0f34
       DirBase: 1efd1b000  ObjectTable: ffffc001d77978c0  HandleCount:  34.
       Image: echoapp.exe
       VadRoot ffffe000802c79f0 Vads 30 Clone 0 Private 135. Modified 5. Locked 0.
       DeviceMap ffffc001d83c6e80
       Token                             ffffc001cf270050
       ElapsedTime                       00:00:00.052
       UserTime                          00:00:00.000
       KernelTime                        00:00:00.000
       QuotaPoolUsage[PagedPool]         33824
       QuotaPoolUsage[NonPagedPool]      4464
       Working Set Sizes (now,min,max)  (682, 50, 345) (2728KB, 200KB, 1380KB)
       PeakWorkingSetSize                652
       VirtualSize                       16 Mb
       PeakVirtualSize                   16 Mb
       PageFaultCount                    688
       MemoryPriority                    BACKGROUND
       BasePriority                      8
       CommitCharge                      138

           THREAD ffffe00080e32080  Cid 03c4.0ec0  Teb: 00007ff7cfece000 Win32Thread: 0000000000000000 RUNNING on processor 1
   ```

   プロセスがドライバーのイベントの書き込みで、ブレークポイントにヒットしたときに実行中だった echoapp.exe に関連付けられている出力を示しています。 詳細については、[ **! プロセス**](-process.md)を参照してください。

9. 使用して、 **! process 0 0**すべてのプロセスの概要情報を表示します。 出力には、CTRL キーを押しながら F キーを使用して、echoapp.exe 画像に関連付けられたプロセスの同じプロセスのアドレスを探します。 次に示す例では、プロセスのアドレスは、ffffe0007e6a7780 が。

   ```dbgcmd
   ...

   PROCESS ffffe0007e6a7780
       SessionId: 1  Cid: 0f68    Peb: 7ff7cfe7a000  ParentCid: 0f34
       DirBase: 1f7fb9000  ObjectTable: ffffc001cec82780  HandleCount:  34.
       Image: echoapp.exe

   ...
   ```

10. プロセス ID のレコードは、このラボに後で使用する echoapp.exe に関連付けられています。 後で使用するため、コピー バッファーのアドレスをコピーするのに CTRL + C を使用することもできます。

    \_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_(echoapp.exe プロセスのアドレス)

11. 入力**g** echoapp.exe の実行が完了するまで転送は、コードを実行するデバッガーを必要とします。 読み取りでブレークポイントにヒットし、何度もイベントを記述します。 Echoapp.exe が完了したらにデバッガーにブレーク、キーを押して CTRL + ScrLk (Ctrl + Break)。

12. 使用して、 **! プロセス**コマンドを別のプロセスが現在実行されていることを確認します。 プロセスのイメージの値を以下に示す出力*システム*とは異なる、*エコー*イメージの値。

    ```dbgcmd
    1: kd> !process
    PROCESS ffffe0007b65d900
        SessionId: none  Cid: 0004    Peb: 00000000  ParentCid: 0000
        DirBase: 001ab000  ObjectTable: ffffc001c9a03000  HandleCount: 786.
        Image: System
        VadRoot ffffe0007ce45930 Vads 14 Clone 0 Private 22. Modified 131605. Locked 64.
        DeviceMap ffffc001c9a0c220
        Token                             ffffc001c9a05530
        ElapsedTime                       21:31:02.516
    ...
    ```

    システム プロセスの ffffe0007b65d900 が実行中であること、OS が停止したときに上記の出力を示しています。

13. これで、使用、 **! プロセス**コマンドを実行して、先ほど記録した echoapp.exe に関連付けられていたプロセス ID を確認します。 次に示す例のプロセスのアドレスの代わりに、前に記録した echoapp.exe プロセス アドレスを指定します。

    ```dbgcmd
    0: kd> !process ffffe0007e6a7780
    TYPE mismatch for process object at 82a9acc0
    ```

    プロセス オブジェクトが不要になった echoapp.exe プロセスとして、使用可能なが現在実行されていません。

### <a name="span-idthreadsspanspan-idthreadsspanspan-idthreadsspanthreads"></a><span id="Threads"></span><span id="threads"></span><span id="THREADS"></span>スレッド

**注:**  
表示し、スレッドを設定するコマンドは、プロセスの非常に似ています。 使用して、 [ **! スレッド**](-thread.md)スレッドを表示するコマンド。 使用[ **.thread** ](-thread--set-register-context-.md)を現在のスレッドを設定します。



1.  **&lt;ホスト システムで**

    入力**g**コードが実行される、ターゲット システムを再起動するデバッガーを起動します。

2.  **-&gt; ターゲット システム**

    ターゲット システムに EchoApp.exe ドライバーのテスト プログラムを実行します。

3.  **&lt;ホスト システムで**

    ブレークポイントにヒットして、コードの実行を停止します。

    ```dbgcmd
    Breakpoint 4 hit
    ECHO!EchoEvtIoRead:
    aade54c0 55              push    ebp
    ```

4.  実行しているスレッドを表示するには、次のように入力します。 [ **! スレッド**](-thread.md)します。 次のような情報が表示されます。

    ```dbgcmd
    0: kd>  !thread
    THREAD ffffe000809a0880  Cid 0b28.1158  Teb: 00007ff7d00dd000 Win32Thread: 0000000000000000 RUNNING on processor 0
    IRP List:
        ffffe0007bc5be10: (0006,01f0) Flags: 00060a30  Mdl: 00000000
    Not impersonating
    DeviceMap                 ffffc001d83c6e80
    Owning Process            ffffe0008096c900       Image:         echoapp.exe
    ...
    ```

    イメージの名前をメモ*echoapp.exe*、テスト アプリに関連付けられているスレッドで対象にしていることを示します。

5.  4. 使用して、 **! プロセス**コマンド echoapp.exe に関連付けられているプロセスで実行されている唯一のスレッドがこれを判断します。 プロセスの実行中のスレッドのスレッド数を実行している同じスレッドであることに注意してください、。 スレッドのコマンドが表示されます。

    ```dbgcmd
    0: kd> !process
    PROCESS ffffe0008096c900
        SessionId: 1  Cid: 0b28    Peb: 7ff7d00df000  ParentCid: 0f34
        DirBase: 1fb746000  ObjectTable: ffffc001db6b52c0  HandleCount:  34.
        Image: echoapp.exe
        VadRoot ffffe000800cf920 Vads 30 Clone 0 Private 135. Modified 8. Locked 0.
        DeviceMap ffffc001d83c6e80
        Token                             ffffc001cf5dc050
        ElapsedTime                       00:00:00.048
        UserTime                          00:00:00.000
        KernelTime                        00:00:00.000
        QuotaPoolUsage[PagedPool]         33824
        QuotaPoolUsage[NonPagedPool]      4464
        Working Set Sizes (now,min,max)  (681, 50, 345) (2724KB, 200KB, 1380KB)
        PeakWorkingSetSize                651
        VirtualSize                       16 Mb
        PeakVirtualSize                   16 Mb
        PageFaultCount                    686
        MemoryPriority                    BACKGROUND
        BasePriority                      8
        CommitCharge                      138

            THREAD ffffe000809a0880  Cid 0b28.1158  Teb: 00007ff7d00dd000 Win32Thread: 0000000000000000 RUNNING on processor 0
    ```

6.  使用して、 **! process 0 0 コマンド**2 つのプロセスのアドレスを特定するには、プロセスが関連して、レコードこれらのプロセス アドレスは、ここです。

    Cmd.exe: \_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_

    EchoApp.exe: \_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_

    ```dbgcmd
    0: kd> !process 0 0 

    …

    PROCESS ffffe0007bbde900
        SessionId: 1  Cid: 0f34    Peb: 7ff72dfa7000  ParentCid: 0c64
        DirBase: 19c5fa000  ObjectTable: ffffc001d8c2f300  HandleCount:  31.
        Image: cmd.exe
    …
    PROCESS ffffe0008096c900
        SessionId: 1  Cid: 0b28    Peb: 7ff7d00df000  ParentCid: 0f34
        DirBase: 1fb746000  ObjectTable: ffffc001db6b52c0  HandleCount:  34.
        Image: echoapp.exe
    …
    ```

    **注**また使用することができます **! 0 17 処理**のすべてのプロセスに関する詳細情報を表示します。 このコマンドの出力を時間のかかることができます。 出力は、Ctrl キーを押しながら F キーを使用して検索できます。



7.  使用して、 **! プロセス**PC を実行している両方のプロセスのプロセス情報を一覧するコマンド。 プロセスのアドレスを指定する、 **! process 0 0**出力を次に示すアドレスではないです。

    この例の出力結果が以前に記録された cmd.exe プロセス ID です。 このプロセス ID のイメージ名は cmd.exe であることに注意してください。

    ```dbgcmd
    0: kd>  !process ffffe0007bbde900
    PROCESS ffffe0007bbde900
        SessionId: 1  Cid: 0f34    Peb: 7ff72dfa7000  ParentCid: 0c64
        DirBase: 19c5fa000  ObjectTable: ffffc001d8c2f300  HandleCount:  31.
        Image: cmd.exe
        VadRoot ffffe0007bb8e7b0 Vads 25 Clone 0 Private 117. Modified 20. Locked 0.
        DeviceMap ffffc001d83c6e80
        Token                             ffffc001d8c48050
        ElapsedTime                       21:33:05.840
        UserTime                          00:00:00.000
        KernelTime                        00:00:00.000
        QuotaPoolUsage[PagedPool]         24656
        QuotaPoolUsage[NonPagedPool]      3184
        Working Set Sizes (now,min,max)  (261, 50, 345) (1044KB, 200KB, 1380KB)
        PeakWorkingSetSize                616
        VirtualSize                       2097164 Mb
        PeakVirtualSize                   2097165 Mb
        PageFaultCount                    823
        MemoryPriority                    FOREGROUND
        BasePriority                      8
        CommitCharge                      381

            THREAD ffffe0007cf34880  Cid 0f34.0f1c  Teb: 00007ff72dfae000 Win32Thread: 0000000000000000 WAIT: (UserRequest) UserMode Non-Alertable
                ffffe0008096c900  ProcessObject
            Not impersonating
    ...
    ```

    この例の出力結果が以前に記録された echoapp.exe プロセス ID です。

    ```dbgcmd
    0: kd>  !process ffffe0008096c900
    PROCESS ffffe0008096c900
        SessionId: 1  Cid: 0b28    Peb: 7ff7d00df000  ParentCid: 0f34
        DirBase: 1fb746000  ObjectTable: ffffc001db6b52c0  HandleCount:  34.
        Image: echoapp.exe
        VadRoot ffffe000800cf920 Vads 30 Clone 0 Private 135. Modified 8. Locked 0.
        DeviceMap ffffc001d83c6e80
        Token                             ffffc001cf5dc050
        ElapsedTime                       00:00:00.048
        UserTime                          00:00:00.000
        KernelTime                        00:00:00.000
        QuotaPoolUsage[PagedPool]         33824
        QuotaPoolUsage[NonPagedPool]      4464
        Working Set Sizes (now,min,max)  (681, 50, 345) (2724KB, 200KB, 1380KB)
        PeakWorkingSetSize                651
        VirtualSize                       16 Mb
        PeakVirtualSize                   16 Mb
        PageFaultCount                    686
        MemoryPriority                    BACKGROUND
        BasePriority                      8
        CommitCharge                      138

            THREAD ffffe000809a0880  Cid 0b28.1158  Teb: 00007ff7d00dd000 Win32Thread: 0000000000000000 RUNNING on processor 0
            IRP List:
                ffffe0007bc5be10: (0006,01f0) Flags: 00060a30  Mdl: 00000000
            Not impersonating
    ...
    ```

8.  レコードのスレッドの最初のアドレスは、次の 2 つのプロセスに関連付けられています。

    Cmd.exe: \_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_

    EchoApp.exe: \_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_

9.  使用して、 **!スレッド**コマンド、現在のスレッドに関する情報を表示します。

    ```dbgcmd
    0: kd>  !Thread
    THREAD ffffe000809a0880  Cid 0b28.1158  Teb: 00007ff7d00dd000 Win32Thread: 0000000000000000 RUNNING on processor 0
    IRP List:
        ffffe0007bc5be10: (0006,01f0) Flags: 00060a30  Mdl: 00000000
    Not impersonating
    DeviceMap                 ffffc001d83c6e80
    Owning Process            ffffe0008096c900       Image:         echoapp.exe
    Attached Process          N/A            Image:         N/A
    ...
    ```

    現在のスレッドに echoapp.exe に関連付けられているスレッドが、想定どおりが実行中の状態。

10. 使用して、 **!スレッド**cmd.exe プロセスに関連付けられているスレッドに関する情報を表示するコマンド。 以前に記録したスレッドのアドレスを提供します。

    ```dbgcmd
    0: kd> !Thread ffffe0007cf34880
    THREAD ffffe0007cf34880  Cid 0f34.0f1c  Teb: 00007ff72dfae000 Win32Thread: 0000000000000000 WAIT: (UserRequest) UserMode Non-Alertable
        ffffe0008096c900  ProcessObject
    Not impersonating
    DeviceMap                 ffffc001d83c6e80
    Owning Process            ffffe0007bbde900       Image:         cmd.exe
    Attached Process          N/A            Image:         N/A
    Wait Start TickCount      4134621        Ticks: 0
    Context Switch Count      4056           IdealProcessor: 0             
    UserTime                  00:00:00.000
    KernelTime                00:00:01.421
    Win32 Start Address 0x00007ff72e9d6e20
    Stack Init ffffd0015551dc90 Current ffffd0015551d760
    Base ffffd0015551e000 Limit ffffd00155518000 Call 0
    Priority 14 BasePriority 8 UnusualBoost 3 ForegroundBoost 2 IoPriority 2 PagePriority 5
    Child-SP          RetAddr           : Args to Child                                                           : Call Site
    ffffd001`5551d7a0 fffff801`eed184fe : fffff801`eef81180 ffffe000`7cf34880 00000000`fffffffe 00000000`fffffffe : nt!KiSwapContext+0x76 [d:\9142\minkernel\ntos\ke\amd64\ctxswap.asm @ 109]
    ffffd001`5551d8e0 fffff801`eed17f79 : ffff03a5`ca56a3c8 000000de`b6a6e990 000000de`b6a6e990 00007ff7`d00df000 : nt!KiSwapThread+0x14e [d:\9142\minkernel\ntos\ke\thredsup.c @ 6347]
    ffffd001`5551d980 fffff801`eecea340 : ffffd001`5551da18 00000000`00000000 00000000`00000000 00000000`00000388 : nt!KiCommitThreadWait+0x129 [d:\9142\minkernel\ntos\ke\waitsup.c @ 619]
    ...
    ```

    このスレッドは cmd.exe を関連付けられ、待機状態にあります。

11. CMD.exe のスレッドを待機中のスレッドにコンテキストを変更するを待機中のスレッドのアドレスを提供します。

    ```dbgcmd
    0: kd> .Thread ffffe0007cf34880
    Implicit thread is now ffffe000`7cf34880
    ```

12. 使用して、 **k**待機中のスレッドに関連付けられている呼び出し履歴を表示するコマンド。

    ```dbgcmd
    0: kd> k
      *** Stack trace for last set context - .thread/.cxr resets it
    # Child-SP          RetAddr           Call Site
    00 ffffd001`5551d7a0 fffff801`eed184fe nt!KiSwapContext+0x76 [d:\9142\minkernel\ntos\ke\amd64\ctxswap.asm @ 109]
    01 ffffd001`5551d8e0 fffff801`eed17f79 nt!KiSwapThread+0x14e [d:\9142\minkernel\ntos\ke\thredsup.c @ 6347]
    02 ffffd001`5551d980 fffff801`eecea340 nt!KiCommitThreadWait+0x129 [d:\9142\minkernel\ntos\ke\waitsup.c @ 619]
    03 ffffd001`5551da00 fffff801`ef02e642 nt!KeWaitForSingleObject+0x2c0 [d:\9142\minkernel\ntos\ke\wait.c @ 683]
    ...
    ```

    スタック要素などを呼び出す**KiCommitThreadWait**このスレッドが実行されていないことが期待どおりに指定します。

**注:**  
スレッドとプロセスの詳細については、次を参照してください。

[スレッドとプロセス](threads-and-processes.md)

[コンテキストを変更します。](changing-contexts.md)



## <a name="span-idsection10irqlregistersandendingthewindbgsessionspanspan-idsection10irqlregistersandendingthewindbgsessionspanspan-idsection10irqlregistersandendingthewindbgsessionspansection-10-irql-registers-and-ending-the-windbg-session"></a><span id="Section_10__IRQL__Registers_and_Ending_the_WinDbg_session"></span><span id="section_10__irql__registers_and_ending_the_windbg_session"></span><span id="SECTION_10__IRQL__REGISTERS_AND_ENDING_THE_WINDBG_SESSION"></span>セクションの 10:IRQL、レジスタと WinDbg のセッションを終了します。

### <a name="span-idirqlregistersmemoryspanspan-idirqlregistersmemoryspanspan-idirqlregistersmemoryspanviewing-the-saved-irql"></a><span id="IRQLRegistersMemory"></span><span id="irqlregistersmemory"></span><span id="IRQLREGISTERSMEMORY"></span>保存した IRQL を表示します。

*セクションの 10 では、IRQL と、regsisters の内容が表示されます。*

**&lt;ホスト システムで**

割り込み要求レベル (IRQL) を使用して、割り込み処理の優先度を管理できます。 各プロセッサには、スレッドを上げたり下げたりする IRQL 設定があります。 プロセッサの IRQL 設定以下で発生する割り込みは、マスクされ、現在の操作には影響しません。 プロセッサの IRQL 設定の上で発生した割り込みは、現在の操作よりも優先されます。 [ **! Irql** ](-irql.md)デバッガー中断が発生する前に拡張機能に、ターゲット コンピューターの現在のプロセッサの割り込み要求レベル (IRQL) が表示されます。 ときに、デバッガーでは、IRQL の変更対象のコンピューターに分割が、IRQL を効果的なデバッガー中断が保存され、によって表示される直前に **! irql**します。

```dbgcmd
0: kd> !irql
Debugger saved IRQL for processor 0x0 -- 2 (DISPATCH_LEVEL)
```

### <a name="span-idviewingtheregistersspanspan-idviewingtheregistersspanspan-idviewingtheregistersspanviewing-the-registers"></a><span id="ViewingTheRegisters"></span><span id="viewingtheregisters"></span><span id="VIEWINGTHEREGISTERS"></span>レジスタを表示します。

**&lt;ホスト システムで**

使用して、現在のプロセッサの現在のスレッドのレジスタの内容を表示、 [ **r (レジスタ)** ](r--registers-.md)コマンド。

```dbgcmd
0: kd> r
rax=000000000000c301 rbx=ffffe00173eed880 rcx=0000000000000001
rdx=000000d800000000 rsi=ffffe00173eed8e0 rdi=ffffe00173eed8f0
rip=fffff803bb757020 rsp=ffffd001f01f8988 rbp=ffffe00173f0b620
 r8=000000000000003e  r9=ffffe00167a4a000 r10=000000000000001e
r11=ffffd001f01f88f8 r12=0000000000000000 r13=ffffd001f01efdc0
r14=0000000000000001 r15=0000000000000000
iopl=0         nv up ei pl nz na pe nc
cs=0010  ss=0018  ds=002b  es=002b  fs=0053  gs=002b             efl=00000202
nt!DbgBreakPointWithStatus:
fffff803`bb757020 cc              int     3
```

また、クリックして、レジスタの内容を表示できる**ビュー** &gt; **登録**します。 詳細については、[ **r (レジスタ)**](r--registers-.md)を参照してください。

レジスタの内容の表示は、アセンブリ言語でコードが実行およびその他のシナリオでのステップするときに役立ちます。 アセンブリ言語の逆アセンブリの詳細については、[x86 注釈付き逆アセンブリ](annotated-x86-disassembly.md)と[x64 注釈付き逆アセンブリ](annotated-x64-disassembly.md)を参照してください。

レジスタの内容については、[x86 アーキテクチャ](x86-architecture.md)と[x64 アーキテクチャ](x64-architecture.md)を参照してください。

### <a name="span-idendingthesessionspanspan-idendingthesessionspanspan-idendingthesessionspanending-the-windbg-session"></a><span id="EndingTheSession"></span><span id="endingthesession"></span><span id="ENDINGTHESESSION"></span>WinDbg のセッションを終了します。

**&lt;ホスト システムで**

ユーザー モードのデバッグ セッションを終了、デバッガーを休止モードに戻る、もう一度実行するターゲット アプリケーションの設定を入力、 **qd** (Quit およびデタッチ) コマンド。

使用してください、 **g**コマンド、コードの実行対象のコンピュータを使用できるようにします。 これを使用して、ブレークポイントをクリアするといった方法も * * bc \\* * * いるため、ターゲット コンピューターが中断してホスト コンピューターのデバッガーに接続しようとしています。 しません。

```dbgcmd
0: kd> qd
```

詳細については、次を参照してください。 [WinDbg でデバッグ セッションを終了する](ending-a-debugging-session-in-windbg.md)デバッグ リファレンス ドキュメント。

## <a name="span-idwindowsdebuggingresourcesspanspan-idwindowsdebuggingresourcesspanspan-idwindowsdebuggingresourcesspansection-11-windows-debugging-resources"></a><span id="WindowsDebuggingResources"></span><span id="windowsdebuggingresources"></span><span id="WINDOWSDEBUGGINGRESOURCES"></span>第 11 条:Windows デバッグ用のリソース


追加情報は、Windows のデバッグで使用できます。 これらの例では、Windows Vista などの Windows の以前のバージョンを使用して、これらの書籍の一部が説明する概念は Windows のほとんどのバージョンに適用可能なことに注意してください。

**ブックの「**

-   Mario Hewardt と Daniel Pravat によって高度な Windows のデバッグ

-   内部の Windows デバッグ:A Practical Guide to デバッグ出力およびトレース戦略によって Tarik Soulami Windows® で

-   E. のある Mark Russinovich、David A. Solomon Alex Ionescu、Windows の内部構造

**ビデオ**

デフラグ ツール WinDbg エピソード 13 ~ 29 の表示します。 <https://channel9.msdn.com/Shows/Defrag-Tools>

**トレーニング ベンダー:**

OSR <https://www.osr.com/>

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>関連トピック


[標準的なデバッグ手法](standard-debugging-techniques.md)

[特殊なデバッグ手法](specialized-debugging-techniques.md)

[Windows のデバッグの概要](getting-started-with-windows-debugging.md)











---
title: ユニバーサルドライバーのデバッグ-ステップバイステップラボ (Echo カーネルモード)
description: このラボでは、WinDbg カーネルデバッガーについて説明します。 WinDbg は、echo カーネルモードサンプルドライバーコードのデバッグに使用されます。
ms.assetid: 3FBC3693-4288-42BA-B1E8-84DC2A9AFFD9
keywords:
- ラボのデバッグ
- ステップバイステップ
- エコー
ms.date: 02/27/2020
ms.localizationpriority: medium
ms.openlocfilehash: ed666748964750f240334a662f1c18b1ba78eb63
ms.sourcegitcommit: f1f641bd759b7bf6e45626ffcc090ffd28337c30
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/28/2020
ms.locfileid: "78166686"
---
# <a name="span-iddebuggerdebug_universal_drivers_-_step_by_step_lab__echo_kernel-mode_spandebug-universal-drivers---step-by-step-lab-echo-kernel-mode"></a><span id="debugger.debug_universal_drivers_-_step_by_step_lab__echo_kernel-mode_"></span>ユニバーサルドライバーのデバッグ-ステップバイステップラボ (カーネルモードのエコー)

このラボでは、WinDbg カーネルデバッガーについて説明します。 WinDbg は、echo カーネルモードサンプルドライバーコードのデバッグに使用されます。

## <a name="span-idlab_objectivesspanspan-idlab_objectivesspanspan-idlab_objectivesspanlab-objectives"></a><span id="Lab_objectives"></span><span id="lab_objectives"></span><span id="LAB_OBJECTIVES"></span>ラボの目標

このラボには、デバッグツールを紹介し、一般的なデバッグコマンドを学習し、ブレークポイントの使用方法を示し、デバッグ拡張機能の使用方法を示す演習が含まれています。

このラボでは、次のことを調べるために、ライブカーネルデバッグ接続が使用されます。

- Windows デバッガーのコマンドを使用する
- 標準コマンド (呼び出し履歴、変数、スレッド、IRQL) を使用する
- 高度なドライバーデバッグコマンドを使用する (! コマンド)
- シンボルを使用する
- ライブデバッグでブレークポイントを設定する
- 呼び出し履歴の表示
- プラグアンドプレイデバイスツリーを表示する
- スレッドとプロセスコンテキストの操作

**メモ** Windows デバッガーを使用する場合、ユーザーモードまたはカーネルモードデバッグの2種類のデバッグを実行できます。

*ユーザーモード*-アプリケーションとサブシステムは、ユーザーモードでコンピューター上で実行されます。 ユーザーモードで実行されるプロセスは、独自の仮想アドレス空間内で実行されます。 システムハードウェア、使用するために割り当てられていないメモリ、システムの整合性を損なう可能性があるシステムのその他の部分など、システムの多くの部分に直接アクセスすることが制限されています。 ユーザーモードで実行されるプロセスはシステムおよびその他のユーザーモードプロセスから効果的に分離されるため、これらのリソースに干渉することはできません。

*カーネルモード*-カーネルモードは、オペレーティングシステムと特権プログラムが実行されるプロセッサアクセスモードです。 カーネルモードコードには、システムの任意の部分にアクセスするアクセス許可があり、ユーザーモードコードのように制限されていません。 ユーザーモードまたはカーネルモードで実行されている他のプロセスの任意の部分にアクセスできます。 コア OS 機能と多くのハードウェアデバイスドライバーは、カーネルモードで実行されます。

このラボでは、多くのデバイスドライバーのデバッグに使用される方法であるため、カーネルモードのデバッグに焦点を当てます。

この演習では、ユーザーモードとカーネルモードの両方のデバッグ中に頻繁に使用されるデバッグコマンドについて説明します。 この演習では、カーネルモードのデバッグに使用されるデバッグ拡張機能 ("! コマンド" とも呼ばれます) についても説明します。

## <a name="span-idlab_setupspanspan-idlab_setupspanspan-idlab_setupspanlab-setup"></a><span id="Lab_setup"></span><span id="lab_setup"></span><span id="LAB_SETUP"></span>ラボのセットアップ

ラボを完了するには、次のハードウェアが必要です。

- Windows 10 を実行するラップトップまたはデスクトップコンピューター (ホスト)
- Windows 10 を実行するラップトップまたはデスクトップコンピューター (ターゲット)
- 2台の Pc を接続するためのネットワークハブ/ルーターとネットワークケーブル
- シンボルファイルをダウンロードするためのインターネットへのアクセス

ラボを完成させるには、次のソフトウェアが必要です。

- Visual Studio 
- Windows 10 用 Windows ソフトウェア開発キット (SDK)
- Windows 10 用 windows Driver Kit (WDK)
- Windows 10 用の echo ドライバーのサンプル

ラボには、次の11個のセクションがあります。

- [セクション 1: カーネルモードの WinDbg セッションに接続する](#connectto)
- [セクション 2: カーネルモードのデバッグコマンドと手法](#kernelmodedebuggingcommandsandtechniques)
- [セクション 3: KMDF Universal Echo Driver をダウンロードしてビルドする](#download)
- [セクション 4: ターゲットシステムに KMDF Echo driver サンプルをインストールする](#install)
- [セクション 5: WinDbg を使用してドライバーに関する情報を表示する](#usewindbgtodisplayinformation)
- [セクション 6: プラグアンドプレイデバイスツリー情報を表示する](#displayingtheplugandplaydevicetree)
- [セクション 7: ブレークポイントとソースコードの操作](#workingwithbreakpoints)
- [セクション 8: 変数と呼び出し履歴を表示する](#viewingvariables)
- [セクション 9: プロセスとスレッドを表示する](#displayingprocessesandthreads)
- [セクション 10: IRQL、登録、および WinDbg セッションの終了](#irqlregistersmemory)
- [セクション 11: Windows デバッグリソース](#windowsdebuggingresources)

## <a name="span-idconnecttospanspan-idconnecttospansection-1-connect-to-a-kernel-mode-windbg-session"></a><span id="connectto"></span><span id="CONNECTTO"></span>セクション 1: カーネルモードの WinDbg セッションに接続する

*セクション1では、ホストとターゲットシステムでネットワークデバッグを構成します。*

このラボの Pc は、カーネルデバッグにイーサネットネットワーク接続を使用するように構成する必要があります。

このラボでは2台の Pc を使用します。 Windows デバッガーは*ホスト*システム上で実行され、Kmdf Echo ドライバーは*ターゲット*システムで実行されます。

 ネットワークハブ/ルーターとネットワークケーブルを使用して、2台の Pc を接続します。

![2つの pc が二重矢印で接続されている](images/debuglab-image-targethostdrawing1.png)

カーネルモードアプリケーションを操作し、WinDbg を使用するには、KDNET over イーサネット転送を使用することをお勧めします。 イーサネットトランスポートプロトコルの使用方法の詳細については、「 [WinDbg を使用したはじめに (カーネルモード)](getting-started-with-windbg--kernel-mode-.md)」を参照してください。 ターゲットコンピューターの設定の詳細については、「[ドライバーの手動展開のためのコンピューターの準備](https://docs.microsoft.com/windows-hardware/drivers)」および「 [KDNET Network カーネルデバッグの自動](setting-up-a-network-debugging-connection-automatically.md)セットアップ」を参照してください。

### <a name="span-idconfigure__kernel_mode_debugging_using_ethernetspanspan-idconfigure__kernel_mode_debugging_using_ethernetspanspan-idconfigure__kernel_mode_debugging_using_ethernetspanconfigure-kernelmode-debugging-using-ethernet"></a><span id="Configure__kernel_mode_debugging_using_ethernet"></span><span id="configure__kernel_mode_debugging_using_ethernet"></span><span id="CONFIGURE__KERNEL_MODE_DEBUGGING_USING_ETHERNET"></span>イーサネットを使用してカーネルモードのデバッグを構成する

ターゲットシステムでカーネルモードのデバッグを有効にするには、次の手順を実行します。

**&lt;-ホストシステム**

1. ホストシステムでコマンドプロンプトを開き、「 **ipconfig** 」と入力して、IP アドレスを決定します。

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

2. ホストシステムの IP アドレスを記録する: \_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_を \_\_\_\_\_\_\_\_\_\_\_\_

**ターゲットシステムで &gt; を -する**

3. ターゲットシステムでコマンドプロンプトを開き、 **ping**コマンドを使用して、2つのシステム間のネットワーク接続を確認します。 サンプル出力に示されている169.182.1.1 ではなく、記録したホストシステムの実際の IP アドレスを使用します。

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

次の手順を実行して、ターゲットシステムでカーネルモードのデバッグを有効にします。

> [!IMPORTANT]
> BCDEdit を使用してブート情報を変更する前に、テスト PC で BitLocker やセキュアブートなどの Windows のセキュリティ機能を一時的に停止することが必要になる場合があります。
> セキュリティ機能が無効になっている場合は、テストが完了し、テスト PC を適切に管理するときに、これらのセキュリティ機能を再び有効にします。

1. ターゲット コンピューターで、管理者としてコマンド プロンプト ウィンドウを開きます。 デバッグを有効にするには、このコマンドを入力します。

    ```console
    C:\> bcdedit /set {default} DEBUG YES
    ```

2. テスト署名を有効にするには、このコマンドを入力します。

    ```console
    C:\> bcdedit /set TESTSIGNING ON 
    ```


3. 次のコマンドを入力して、ホストシステムの IP アドレスを設定します。 前に記録したホストシステムの IP アドレスを使用します。これは、表示されているものではありません。

    ```console
    C:\> bcdedit /dbgsettings net hostip:192.168.1.1 port:50000 key:1.2.3.4
    ```

**警告** 接続のセキュリティを強化し、ランダムなクライアントデバッガー接続要求のリスクを軽減するには、自動生成されたランダムキーの使用を検討してください。 詳細については、「 [KDNET Network カーネルデバッグの自動](setting-up-a-network-debugging-connection-automatically.md)セットアップ」を参照してください。

4. このコマンドを入力して、適切に設定されている dbgsettings であることを確認します。

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

ファイアウォールからポップアップメッセージを受信し、デバッガーを使用する場合は、 **3 つすべて**のチェックボックスをオンにします。

![windows セキュリティの警告-windows ファイアウォールがこのアプリの一部の機能をブロックしました ](images/debuglab-image-firewall-dialog-box.png)

**&lt;-ホストシステム**

1. ホスト コンピューターで、管理者としてコマンド プロンプト ウィンドウを開きます。 Windows キットのインストールの一部としてインストールされた Windows Driver Kit (WDK) の、x64 バージョンの WinDbg を使用します。 既定では、この場所にあります。

    ```console
    C:\> Cd C:\Program Files(x86)\Windows Kits\10\Debuggers\x64 
    ```

> [!NOTE]
> このラボでは、両方の Pc がターゲットとホストの両方で64ビット版の Windows を実行していることを前提としています。
> そうでない場合は、ターゲットが実行されているホストで同じ "ビット" のツールを実行するのが最善の方法です。
たとえば、ターゲットが32ビット Windows を実行している場合は、ホストで32バージョンのデバッガーを実行します。 詳細については、「 [32 ビットまたは64ビットのデバッグツールの選択](choosing-a-32-bit-or-64-bit-debugger-package.md)」を参照してください。
>

2. 次のコマンドを使用して、リモートユーザーデバッグで WinDbg を起動します。 キーとポートの値は、ターゲットで BCDEdit を使用して以前に設定したものと一致します。

    ```console
    WinDbg –k net:port=50000,key=1.2.3.4
    ```

**ターゲットシステムで &gt;を -する**

ターゲットシステムを再起動します。

**&lt;-ホストシステム**

1 ~ 2 分で、デバッグ出力がホストシステムに表示されます。

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

デバッガーコマンドウィンドウは、WinDbg の主要なデバッグ情報ウィンドウです。 このウィンドウでは、デバッガーコマンドを入力し、コマンドの出力を表示できます。

デバッガーコマンドウィンドウが2つのペインに分割されます。 ウィンドウの下部にある小さいウィンドウ (コマンド入力ウィンドウ) にコマンドを入力すると、ウィンドウの上部にある大きなウィンドウにコマンドの出力が表示されます。

コマンド入力ウィンドウで、上方向キーと下方向キーを使用して、コマンド履歴をスクロールします。 コマンドが表示されたら、それを編集するか、enter キーを押して**コマンドを実行**します。

## <a name="span-idkernelmodedebuggingcommandsandtechniquesspanspan-idkernelmodedebuggingcommandsandtechniquesspanspan-idkernelmodedebuggingcommandsandtechniquesspansection-2-kernel-mode-debugging-commands-and-techniques"></a><span id="KernelModeDebuggingCommandsAndTechniques"></span><span id="kernelmodedebuggingcommandsandtechniques"></span><span id="KERNELMODEDEBUGGINGCOMMANDSANDTECHNIQUES"></span>セクション 2: カーネルモードのデバッグコマンドと手法


*セクション2では、デバッグコマンドを使用して、ターゲットシステムに関する情報を表示します。*

**&lt;-ホストシステム**

**でデバッガーマークアップ言語 (DML) を有効にします。 dml\_を優先します。**

一部のデバッグコマンドでは、デバッガーのマークアップ言語を使用してテキストを表示します。これをクリックすると、詳細情報をすばやく収集できます。

1. WinDBg で Ctrl + Break (スクロールロック) を使用して、ターゲットシステムで実行されているコードを中断します。 ターゲットシステムが応答するまでに少し時間がかかる場合があります。

![ライブカーネル接続からのコマンドウィンドウ出力を示す windows デバッガー](images/debuglab-image-winddbg-hh.png)


2. 次のコマンドを入力して、コマンドウィンドウデバッガーで DML を有効にします。

```dbgcmd
0: kd> .prefer_dml 1
DML versions of commands on by default
```

**. Hh を使用してヘルプを表示する**

参照コマンドのヘルプには、 **. hh**コマンドを使用してアクセスできます。

3. 次のコマンドを入力して、のコマンドリファレンスヘルプを表示**します。\_dml**を使用します。

```dbgcmd
0: kd> .hh .prefer_dml
```

デバッガーヘルプファイルには、のヘルプが表示され**ます。\_dml**コマンドを使用します。

![デバッガーヘルプアプリケーションに関するヘルプを表示する\-dml コマンド](images/debuglab-image-prefer-dml-help.png)

**ターゲットシステムで Windows のバージョンを表示する**

5. [WinDbg] ウィンドウで、 [**vertarget (ターゲットコンピューターのバージョンを表示)** ](vertarget--show-target-computer-version-.md)コマンドを入力して、ターゲットシステムの詳細なバージョン情報を表示します。

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

**読み込まれたモジュールを一覧表示する**

6. 適切なカーネルモードプロセスを使用していることを確認するには、[WinDbg] ウィンドウで [ [**lm (List Loaded modules)** ](lm--list-loaded-modules-.md) ] コマンドを入力して、読み込まれたモジュールを表示します。

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

**メモ** 省略された出力は、"... "このラボでは、



7. 特定のモジュールに関する詳細情報を要求するには、表示されているように v (verbose) オプションを使用します。

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

8. シンボルパスと読み込まれたシンボルをまだ設定していないので、デバッガーで使用できる情報は限られています。

## <a name="span-iddownloadspanspan-iddownloadspanspan-iddownloadspansection-3-download-and-build-the-kmdf-universal-echo-driver"></a><span id="Download"></span><span id="download"></span><span id="DOWNLOAD"></span>セクション 3: KMDF universal echo driver をダウンロードしてビルドする

*セクション3では、KMDF universal echo ドライバーをダウンロードしてビルドします。*

通常、WinDbg を使用する場合は、独自のドライバーコードを使用します。 WinDbg 操作を理解するために、KMDF テンプレート "Echo" サンプルドライバーが使用されています。 使用可能なソースコードを使用すると、WinDbg に表示される情報を理解しやすくなります。 また、このサンプルは、ネイティブカーネルモードコードをシングルステップ実行する方法を示すために使用されます。 この手法は、複雑なカーネルモードコードの問題をデバッグする場合に非常に役立ちます。

Echo サンプルオーディオドライバーをダウンロードしてビルドするには、次の手順を実行します。

1.  **GitHub から KMDF Echo サンプルをダウンロードして抽出する**

    ブラウザーを使用して、次のように GitHub の echo サンプルを表示できます。

    [https://github.com/Microsoft/Windows-driver-samples/tree/97cf5197cf5b882b2c689d8dc2b555f2edf8f418/general/echo/kmdf](https://github.com/Microsoft/Windows-driver-samples/blob/97cf5197cf5b882b2c689d8dc2b555f2edf8f418/general/echo/kmdf/ReadMe.md)

    このサンプルについては、「」を参照してください。

    <https://github.com/Microsoft/Windows-driver-samples/blob/97cf5197cf5b882b2c689d8dc2b555f2edf8f418/general/echo/kmdf/ReadMe.md>

    ここでは、すべてのユニバーサルドライバーサンプルを参照できます。

    <https://github.com/Microsoft/Windows-driver-samples>

    KMDF Echo サンプルは、general フォルダーにあります。

    ![github の windows-ドライバーのサンプルは、general フォルダーと download zip ボタンを強調表示しています](images/debuglab-image-github.png)

    a. このラボでは、ユニバーサルドライバーのサンプルを1つの zip ファイルにダウンロードする方法を示します。

    <https://github.com/Microsoft/Windows-driver-samples/archive/master.zip>

    b. マスター .zip ファイルをローカルハードドライブにダウンロードします。

    c. *Windows-driver-samples-master*を右クリックし、 **[すべて展開]** を選択します。 新しいフォルダーを指定するか、抽出されたファイルを格納する既存のフォルダーを参照します。 たとえば、 *C:\\DriverSamples\\* を、ファイルを抽出する新しいフォルダーとして指定できます。

    d. ファイルが抽出されたら、次のサブフォルダーに移動します。

    *C:\\DriverSamples\\全般\\echo\\kmdf*

2.  **Visual Studio でドライバーソリューションを開く**

    Microsoft Visual Studio で、[**ファイル**&gt;] をクリックして &gt;**プロジェクト/ソリューション...** を**開き**、抽出したファイルが格納されているフォルダーに移動します (たとえば、 *C:\\driversamples\\general\\echo\\kmdf*)。 *Kmdfecho*ソリューションファイルをダブルクリックして開きます。

    Visual Studio で、ソリューションエクスプローラーを見つけます。 (まだ開いていない場合は、 **[表示]** メニューの **[ソリューションエクスプローラー]** をクリックします)。ソリューションエクスプローラーには、3つのプロジェクトを持つソリューションが1つ表示されます。

    ![kmdfecho プロジェクトから読み込まれたデバイス .c ファイルを使用した visual studio](images/debuglab-image-echo-visual-studio.png)

3.  **サンプルの構成とプラットフォームを設定する**

    ソリューションエクスプローラーで、 **[ソリューション ' kmdfecho ' (3 プロジェクト)]** を右クリックし、 **[Configuration Manager]** を選択します。 構成とプラットフォームの設定が、3つのプロジェクトで同じであることを確認します。 既定では、構成は "Win10 Debug" に設定され、プラットフォームはすべてのプロジェクトに対して "Win64" に設定されます。 1つのプロジェクトで構成やプラットフォームを変更した場合は、残りの3つのプロジェクトに対しても同じ変更を行う必要があります。

4.  **ランタイムライブラリを設定する**

    ランタイムライブラリを設定します。 echo ドライバーのプロパティページを開き、 **CC++ /** &gt;**コード生成**を見つけます。  ランタイムライブラリを DLL バージョンから非 DLL バージョンに変更します。 この設定がない場合は、MSVC ランタイムをターゲットコンピューターに個別にインストールする必要があります。

    ![ランタイムライブラリ設定を強調表示した echo プロパティページ](images/debuglab-image-echoapp-properties.png)

5.  **ドライバーの署名を確認する**

    また、ドライバーのプロパティで、**ドライバー署名**&gt;**署名モード**が "テスト署名" に設定されていることを確認します。 これは、ドライバーが署名されている必要があるために必要です。

    ![[sign mode] 設定が強調表示されている echo プロパティページ](images/debuglab-image-echoapp-driver-signing.png)

6.  **Visual Studio を使用してサンプルをビルドする**

    Visual Studio で、 **[ビルド]** 、[**ソリューションのビルド**&gt;] の順にクリックします。

    すべて問題なく動作する場合は、3つのプロジェクトすべてのビルドが成功したことを示すメッセージがビルドウィンドウに表示されます。

7.  **ビルドされたドライバーファイルを検索する**

    ファイルエクスプローラーで、サンプルの抽出したファイルが格納されているフォルダーに移動します。 たとえば、 *C:\\DriverSamples\\general\\echo\\kmdf*(前に指定したフォルダーである場合) に移動します。 このフォルダー内では、コンパイルされたドライバーファイルの場所は、 **Configuration Manager**で選択した構成とプラットフォームの設定によって異なります。 たとえば、既定の設定を変更せずに残した場合、コンパイルされたドライバーファイルは、64ビットのデバッグビルドの *\\x64\\debug*という名前のフォルダーに保存されます。

    Autosync ドライバーのビルドファイルが格納されているフォルダーに移動します。

    *C:\\DriverSamples\\全般\\echo\\kmdf\\ドライバー\\AutoSync\\x64\\デバッグ*です。 

    フォルダーには次のファイルが含まれている必要があります。

    | ファイル     | 説明                                                                       |
    |----------|-----------------------------------------------------------------------------------|
    | Echo .sys | ドライバーファイル。                                                                  |
    | Echo .inf | ドライバーのインストールに必要な情報が含まれている情報 (INF) ファイル。 |

    また、echoapp ファイルがビルドされています。 *C:\\DriverSamples\\general\\echo\\kmdf\\exe\\x64\\デバッグ*

    | ファイル        | 説明                                                                       |
    |-------------|-----------------------------------------------------------------------------------|
    | EchoApp | コマンドプロンプト実行可能ファイルは、echo ドライバーと通信します。 |     

8.  USB ドライブを探すか、ネットワーク共有を設定して、ビルドされたドライバーファイルとテスト EchoApp をホストからターゲットシステムにコピーします。

次のセクションでは、コードをターゲットシステムにコピーし、ドライバーをインストールしてテストします。

## <a name="span-idinstallspanspan-idinstallspanspan-idinstallspansection-4-install-the-kmdf-echo-driver-sample-on-the-target-system"></a><span id="Install"></span><span id="install"></span><span id="INSTALL"></span>セクション 4: ターゲットシステムに KMDF echo driver サンプルをインストールする

*セクション4では、devcon を使用して echo サンプルドライバーをインストールします。*

**ターゲットシステムで &gt; を -する**

ドライバーをインストールするコンピューターは、*ターゲットコンピューター*または*テストコンピューター*と呼ばれます。 通常、これは、ドライバーパッケージを開発およびビルドするコンピューターとは別のコンピューターです。 ドライバーを開発してビルドするコンピューターは、*ホストコンピューター*と呼ばれます。

ドライバーパッケージを対象のコンピューターに移動し、ドライバーをインストールするプロセスを、ドライバーの*展開*と呼びます。 サンプル echo ドライバーは、自動または手動でデプロイできます。

ドライバーを手動で展開する前に、テスト署名をオンにして、対象のコンピューターを準備する必要があります。 また、WDK インストールでは、DevCon ツールを探す必要があります。 その後、ビルドされたドライバーのサンプルを実行する準備ができました。

ターゲットシステムにドライバーをインストールするには、次の手順を実行します。

**署名済みドライバーのテストを有効にする**

テスト署名されたドライバーを実行する機能を有効にする:

a. Windows の設定を開きます。

b. 更新とセキュリティ で、**回復** を選択します。

c. 詳細なスタートアップ の **今すぐ再起動** をクリックします。

d. PC が再起動したら、 **[スタートアップオプション]** を選択します。 Windows 10 では、[**トラブルシューティング** > **詳細オプション** > **スタートアップ設定**] を選択し、[再起動] ボタンをクリックします。 

e. **F7**キーを押して [ドライバー署名の強制を無効にする] を選択します。

f. ターゲット コンピューターを再起動します。


**&lt;-ホストシステム**

WDK インストールの Tools フォルダーに移動して、DevCon ツールを見つけます。 たとえば、次のフォルダーを探します。

*C:\\Program Files (x86)\\Windows キット\\10\\ツール\\x64\\devcon .exe*ビルドされたドライバーパッケージのターゲットにフォルダーを作成します (たとえば、 *C:\\EchoDriver*)。 前の手順で説明したように、ホストコンピューター上にある、ビルドされたドライバーからすべてのファイルをコピーし、ターゲットコンピューター上に作成したフォルダーに保存します。

ホストシステムで .cer 証明書を探します。この証明書は、作成されたドライバファイルを含むフォルダ内のホストコンピュータ上の同じフォルダにあります。 ターゲットコンピューターで証明書ファイルを右クリックし、 **[インストール]** をクリックして、画面の指示に従ってテスト証明書をインストールします。

ターゲットコンピューターを設定するための詳細な手順については、「[ドライバーの手動展開のためのコンピューターの準備](../develop/preparing-a-computer-for-manual-driver-deployment.md)」を参照してください。

**ターゲットシステムで &gt; を -する**

**ドライバーをインストールする**

次の手順では、サンプルドライバーをインストールしてテストする方法について説明します。 ここで示しているのは、ドライバーのインストールに使う devcon ツールの一般的な構文です。

*devcon install &lt;INF ファイル&gt; &lt;ハードウェア ID&gt;*

このドライバーのインストールに必要な INF ファイル*は、modem.inf です*。 Inf ファイルには、 *echo*をインストールするためのハードウェア ID が含まれています。 Echo サンプルでは、ハードウェア ID は**root\\echo**です。

ターゲット コンピューターで、管理者としてコマンド プロンプト ウィンドウを開きます。 ドライバーパッケージフォルダーに移動し、次のコマンドを入力します。

**devcon install echo .inf root\\echo***Devcon*が認識されていないことを知らせるエラーメッセージが表示された場合は、そのパスを*devcon*ツールに追加してみてください。 たとえば、 *C:\\ツール*というフォルダーにコピーした場合は、次のコマンドを使用してみてください。

**c:\\ツール\\devcon install echo root\\echo**テストドライバーが署名されていないドライバーであることを示すダイアログボックスが表示されます。 **[かまわず続行]** をクリックして続行します。

![windows セキュリティ警告-windows はこのドライバーソフトウェアの発行元を確認できません](images/debuglab-image-install-security-warning.png)

詳細な手順については、「[ドライバーの展開、テスト、およびデバッグのためのコンピューターの構成](https://docs.microsoft.com/windows-hardware/drivers/gettingstarted/provision-a-target-computer-wdk-8-1)」を参照してください。

サンプルドライバーが正常にインストールされたら、テストする準備ができました。

**デバイスマネージャーのドライバーを確認します。**

ターゲットコンピューターのコマンドプロンプトウィンドウで、「 **devmgmt.msc** open デバイスマネージャー」と入力します。 デバイスマネージャーの [表示] メニューで、[種類別のデバイス] を選択します。 デバイスツリーで、[サンプルデバイス] ノードの [ *SAMPLE WDF Echo Driver* ] を見つけます。

![サンプル wdf echo ドライバーが強調表示されているデバイスマネージャーツリー](images/debuglab-image-device-manager-echo.png)

**ドライバーをテストする**

「 **Echoapp** 」と入力して、ドライバーが機能していることを確認するテスト echo アプリを開始します。

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

## <a name="span-idusewindbgtodisplayinformationspanspan-idusewindbgtodisplayinformationspanspan-idusewindbgtodisplayinformationspansection-5-use-windbg-to-display-information-about-the-driver"></a><span id="UseWinDbgToDisplayInformation"></span><span id="usewindbgtodisplayinformation"></span><span id="USEWINDBGTODISPLAYINFORMATION"></span>セクション 5: WinDbg を使用してドライバーに関する情報を表示する

*セクション5では、シンボルパスを設定し、カーネルデバッガーコマンドを使用して KMDF echo サンプルドライバーに関する情報を表示します。*

次の手順を実行して、ドライバーに関する情報を表示します。

**&lt;-ホストシステム**

1.  デバッガーを閉じた場合は、管理者のコマンドプロンプトウィンドウで次のコマンドを使用して、デバッガーを再度開きます。

    ```dbgcmd
    WinDbg -k net:port=50000,key=1.2.3.4
    ```

2.  Ctrl + Break (スクロールロック) を使用して、ターゲットシステムで実行されているコードを中断します。

**シンボルパスの設定**

1.  WinDbg 環境で Microsoft シンボルサーバーへのシンボルパスを設定するには、 **. symfix**コマンドを使用します。

    ```dbgcmd
    0: kd> .symfix
    ```

2.  ローカルシンボルを使用するようにローカルシンボルの場所を追加するには、 **. sympath +** を使用してパスを追加し、次に「」と入力し**ます。**

    ```dbgcmd
    0: kd> .sympath+ C:\DriverSamples\general\echo\kmdf
    0: kd> .reload /f
    ```

    **メモ** **/F** force オプションを指定した **. reload**コマンドは、指定されたモジュールのすべてのシンボル情報を削除し、シンボルを再読み込みします。 場合によっては、このコマンドによってモジュール自体が再読み込みまたはアンロードされることもあります。



**メモ** WinDbg が提供する高度な機能を使用するには、適切なシンボルを読み込む必要があります。 シンボルが適切に構成されていない場合は、シンボルに依存する機能を使用しようとしたときにシンボルが使用できないことを示すメッセージが表示されます。

```dbgcmd
0:000> dv
Unable to enumerate locals, HRESULT 0x80004005
Private symbols (symbols.pri) are required for locals.
Type “.hh dbgerr005” for details.
```



**注:**  
**シンボルサーバー**

シンボルを操作するために使用できるいくつかの方法があります。 多くの状況では、必要に応じて Microsoft が提供するシンボルサーバーからシンボルにアクセスするように PC を構成できます。 このチュートリアルでは、このアプローチが使用されることを前提としています。 環境内のシンボルが別の場所にある場合は、その場所を使用するようにステップを変更します。 詳細については、「[シンボルストアとシンボルサーバー](symbol-stores-and-symbol-servers.md)」を参照してください。



**注:**  
**ソースコードシンボルの要件を理解する**

ソースのデバッグを実行するには、バイナリのチェック (デバッグ) バージョンを作成する必要があります。 コンパイラは、シンボルファイル (.pdb ファイル) を作成します。 これらのシンボルファイルは、バイナリ命令がソース行にどのように対応しているかをデバッガーで表示します。 実際のソースファイル自体には、デバッガーからもアクセスできる必要があります。

シンボルファイルには、ソースコードのテキストは含まれません。 デバッグの場合は、リンカーでコードを最適化しないことをお勧めします。 ソースのデバッグとローカル変数へのアクセスはより困難になります。また、コードが最適化されている場合は、ほぼ不可能な場合もあります。 ローカル変数またはソース行の表示に問題がある場合は、次のビルドオプションを設定します。

```console
set COMPILE_DEBUG=1
set ENABLE_OPTIMIZER=0
```



1. デバッガーのコマンド領域に次のように入力して、echo ドライバーに関する情報を表示します。

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

   詳細については、「 [**lm**](lm--list-loaded-modules-.md)」を参照してください。

2. \_dml = 1 を優先するように設定したので、出力の一部の要素はホットリンクになります。このリンクをクリックすることができます。 デバッグ出力の [*すべてのグローバルシンボルを参照] リンク*をクリックすると、文字 "a" で始まる項目シンボルに関する情報が表示されます。

   ```dbgcmd
   0: kd> x /D Echo!a*
   ```

3. 結局のところ、echo サンプルには文字 "a" で始まるシンボルは含まれていないため、「`x ECHO!Echo*`」と入力すると、echo で始まる echo ドライバーに関連付けられているすべてのシンボルに関する情報が表示されます。

   ```dbgcmd
   0: kd> x ECHO!Echo*
   fffff801`0bf95690 ECHO!EchoEvtIoQueueContextDestroy (void *)
   fffff801`0bf95000 ECHO!EchoEvtDeviceSelfManagedIoStart (struct WDFDEVICE__ *)
   fffff801`0bf95ac0 ECHO!EchoEvtTimerFunc (struct WDFTIMER__ *)
   fffff801`0bf9b120 ECHO!EchoEvtDeviceSelfManagedIoSuspend (struct WDFDEVICE__ *)
   ...
   ```

   詳細については、「 [**x (シンボルを調べる)** ](x--examine-symbols-.md)」を参照してください。

4. **! Lmi**拡張機能には、モジュールに関する詳細情報が表示されます。 「 **! Lmi echo**」と入力します。 出力は次のようなテキストになります。

   ```dbgcmd
   0: kd> !lmi echo
   Loaded Module Info: [echo] 
            Module: ECHO
      Base Address: fffff8010bf94000
        Image Name: ECHO.sys
   … 
   ```

5. 次に示すように、 **! dh**拡張を使用してヘッダー情報を表示します。

   ```dbgcmd
   0: kd> !dh echo

   File Type: EXECUTABLE IMAGE
   FILE HEADER VALUES
        14C machine (i386)
          6 number of sections
   54AD8A42 time date stamp Wed Jan 07 11:34:26 2015
   ...
   ```

6. **デバッグマスクの設定**

   次のように入力して、既定のデバッグビットマスクを変更します。これにより、ターゲットシステムからのすべてのデバッグメッセージがデバッガーに表示されます。

   ```dbgcmd
   0: kd> ed nt!Kd_DEFAULT_MASK  0xFFFFFFFF
   ```

   一部のドライバーでは、0xFFFFFFFF のマスクが使用されるときに追加情報が表示されます。 表示される情報の量を減らす場合は、マスクを0x00000000 に設定します。

   ```dbgcmd
   0: kd> ed nt!Kd_DEFAULT_MASK  0x00000000
   ```

   Dd コマンドを使用して、すべてのデバッガーメッセージを表示するようにマスクが設定されていることを確認します。 

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


## <a name="span-iddisplayingtheplugandplaydevicetreespanspan-iddisplayingtheplugandplaydevicetreespanspan-iddisplayingtheplugandplaydevicetreespansection-6-displaying-plug-and-play-device-tree-information"></a><span id="DisplayingThePlugAndPlayDeviceTree"></span><span id="displayingtheplugandplaydevicetree"></span><span id="DISPLAYINGTHEPLUGANDPLAYDEVICETREE"></span>セクション 6: プラグアンドプレイデバイスツリー情報の表示

*セクション6では、echo サンプルデバイスドライバーに関する情報と、そのドライバーがプラグアンドプレイデバイスツリーに存在する場所を表示します。*

プラグアンドプレイデバイスツリー内のデバイスドライバーに関する情報は、トラブルシューティングに役立ちます。 たとえば、デバイスドライバーがデバイスツリーに存在しない場合は、デバイスドライバーのインストールに問題がある可能性があります。

デバイスノードデバッグ拡張機能の詳細については、「 [ **! devnode**](-devnode.md)」を参照してください。

**&lt;-ホストシステム**

1. プラグアンドプレイデバイスツリー内のすべてのデバイスノードを表示するには、 **! devnode 0 1**コマンドを入力します。

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

2. Ctrl + F キーを使用して、生成された出力を検索し、デバイスドライバーの名前 ( *echo*) を検索します。

   ![検索対象の echo という用語を示すダイアログボックスが表示されます。](images/debuglab-image-find-dialog.png)

3. Echo デバイスドライバーを読み込む必要があります。 次に示すように、 **! devnode 0 1 echo**コマンドを使用して、echo デバイスドライバーに関連付けられているプラグアンドプレイ情報を表示します。

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

4. 前のコマンドに表示される出力には、ドライバーの実行中のインスタンスに関連付けられている PDO が含まれています。この例では、 *0xffffe0007b71a960*になっています。 **! Devobj** <em>&lt;PDO address&gt;</em>コマンドを入力して、echo デバイスドライバーに関連付けられているプラグアンドプレイ情報を表示します。 ここに示されているものではなく、PC に表示される PDO**アドレスを使用**します。

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

5. **! Devnode 0 1**コマンドに表示される出力には、ドライバーの実行中のインスタンスに関連付けられている PDO アドレスが含まれています。この例では、 *0xffffe0007b71a960*です。 デバイスドライバーに関連付けられているプラグアンドプレイ情報を表示するには、 **! devstack** <em>&lt;PDO address&gt;</em>コマンドを入力します。 次に示すように、コンピューターに表示され**ている PDO アドレスを使用**します。これは、以下に示すものではありません。

   ```dbgcmd
   0: kd> !devstack 0xffffe0007b71a960
     !DevObj           !DrvObj            !DevExt           ObjectName
     ffffe000801fee20  \Driver\ECHO       ffffe0007f72eff0  
   > ffffe0007b71a960  \Driver\PnpManager 00000000  0000000e
   !DevNode ffffe0007b71a630 :
     DeviceInst is "ROOT\SAMPLE\0000"
     ServiceName is "ECHO"
   ```

出力には、デバイスドライバースタックが非常に単純であることが示されています。 Echo ドライバーは、PnPManager ノードの子です。 PnPManager はルートノードです。

\Driver\ECHO

\Driver\PnpManager

この図は、より複雑なデバイスノードツリーを示しています。

![約20個のノードを含むデバイスノードツリー](images/debuglab-image-device-node-tree.png)

**メモ** より複雑なドライバースタックの詳細については、「[ドライバースタック](https://docs.microsoft.com/windows-hardware/drivers/gettingstarted/driver-stacks)と[デバイスノードおよびデバイススタック](https://docs.microsoft.com/windows-hardware/drivers/gettingstarted/device-nodes-and-device-stacks)」を参照してください。

## <a name="span-idworkingwithbreakpointsspanspan-idworkingwithbreakpointsspanspan-idworkingwithbreakpointsspansection-7-working-with-breakpoints-and-source-code"></a><span id="WorkingWithBreakpoints"></span><span id="workingwithbreakpoints"></span><span id="WORKINGWITHBREAKPOINTS"></span>セクション 7: ブレークポイントとソースコードの操作

*セクション7では、カーネルモードのソースコードを使用して、ブレークポイントとシングルステップを設定します。*

**注:**  
**コマンドを使用したブレークポイントの設定**

コードをステップ実行し、変数の値をリアルタイムで確認できるようにするには、ブレークポイントを有効にし、ソースコードへのパスを設定する必要があります。

ブレークポイントは、特定のコード行でコードの実行を停止するために使用されます。 その後、そのポイントからコードをステップ実行して、コードの特定のセクションをデバッグすることができます。

デバッグコマンドを使用してブレークポイントを設定するには、次の**b**コマンドのいずれかを使用します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>bp</p></td>
<td align="left"><p>存在するモジュールがアンロードされるまで、アクティブになるブレークポイントを設定します。</p></td>
</tr>
<tr class="even">
<td align="left"><p>bu</p></td>
<td align="left"><p>モジュールがアンロードされたときに未解決のブレークポイントを設定し、モジュールの再読み込み時に再度有効にします。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>bm.exe</p></td>
<td align="left"><p>シンボルのブレークポイントを設定します。 このコマンドでは、bu または bp が適切に使用されます。また、ワイルドカード * を使用して、(クラス内のすべてのメソッドと同様に) に一致するすべてのシンボルにブレークポイントを設定できます。</p></td>
</tr>
</tbody>
</table>

詳細については、デバッグリファレンスドキュメントの「 [WinDbg でのソースコードのデバッグ](source-window.md)」を参照してください。

**&lt;-ホストシステム**

1.  WinDbg UI を使用して、現在の WinDbg セッションで**デバッグ**&gt;**ソースモード**が有効になっていることを確認します。

2.  次のコマンドを入力して、ソースパスにローカルコードの場所を追加します。

    ```dbgcmd
    .srcpath+ C:\DriverSamples\KMDF_Echo_Sample\driver\AutoSync
    ```

3.  次のコマンドを入力して、シンボルパスにローカルシンボルの場所を追加します。

    ```dbgcmd
    .sympath+ C:\DriverSamples\KMDF_Echo_Sample\driver\AutoSync
    ```

4.  ここでは、 **x**コマンドを使用して、echo ドライバーに関連付けられているシンボルを調べて、ブレークポイントに使用する関数名を決定します。 ワイルドカードまたは Ctrl + F を使用して、 **Deviceadd**関数名を見つけることができます。

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

    上記の出力は、echo ドライバーの**Deviceadd**メソッドが echo であることを示しています *。EchoEvtDeviceAdd*。

    または、ソースコードを確認して、ブレークポイントの目的の関数名を見つけることもできます。

5.  ドライバーの名前と、ブレークポイントを設定する関数名 ( **AddDevice**など) を使用して、ブレークポイントを**bm**コマンドで設定します。その後、感嘆符で区切ります。 **AddDevice**を使用して、読み込まれているドライバーを監視します。

    ```dbgcmd
    0: kd> bm ECHO!EchoEvtDeviceAdd
      1: fffff801`0bf9b1c0 @!"ECHO!EchoEvtDeviceAdd"
    ```

    **注:**  
    &lt;モジュール&gt;のような変数を設定するときに、さまざまな構文を使用できます。シンボル&gt;、&lt;クラス&gt;::&lt;メソッド&gt;、'&lt;ファイル&gt;:&lt;行番号&gt;'、または複数回の繰り返し &lt;条件&gt; &lt;\#&gt;&lt;ます。 詳細については、「 [WinDbg およびその他の Windows デバッガーの条件付きブレークポイント](setting-a-conditional-breakpoint.md)」を参照してください。



6.  現在のブレークポイントを一覧表示して、そのブレークポイントが設定されたことを確認するには、「 **bl** 」コマンドを入力します。

    ```dbgcmd
    0: kd> bl
    1 e fffff801`0bf9b1c0     0001 (0001) ECHO!EchoEvtDeviceAdd
    ```

    上に示した出力の "e" は、ブレークポイント番号1が有効になっていることを示しています。

7.  **移動**コマンド**g**を入力して、ターゲットシステムでコードの実行を再開します。

8.  **ターゲットシステムで &gt; を -する**

    Windows で、アイコンを使用するか、 **mmc devmgmt.msc**を入力して、**デバイスマネージャー**を開きます。 デバイスマネージャーで、 **[サンプル]** ノードを展開します。

9.  KMDF Echo ドライバーエントリを右クリックし、メニューから **[無効化]** を選択します。

10. KMDF Echo driver エントリをもう一度右クリックし、メニューから **[有効化]** を選択します。

11. **&lt;-ホストシステム**

    ドライバーが有効になっている場合、 [*AddDevice*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_add_device)デバッグブレークポイントが起動し、ターゲットシステムでのドライバーコードの実行が停止します。 ブレークポイントにヒットしたら、 *AddDevice*ルーチンの開始時に実行を停止する必要があります。 デバッグコマンドの出力には、"ブレークポイント1ヒット" が表示されます。

    ![サンプルコードのローカルとコマンドウィンドウを示す windbg](images/debuglab-image-breakpoint-echo-deviceadd.png)

12. **P**コマンドを入力するか、または F10 キーを押して、 [*AddDevice*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_add_device)ルーチンが終了するまでコードを1行ずつステップ実行します。 かっこ文字 "}" は、表示されているように強調表示されます。

    ![adddevice ルーチンの開始時に強調表示されている中かっこ文字を示すコードウィンドウ](images/debuglab-image-breakpoint-end-deviceadd.png)

13. 次のセクションでは、DeviceAdd コードが実行された後の変数の状態を確認します。

**注:**  
**ブレークポイントの状態の変更**

次のコマンドを使用して、既存のブレークポイントを変更できます。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>bl</p></td>
<td align="left"><p>ブレークポイントを一覧表示します。</p></td>
</tr>
<tr class="even">
<td align="left"><p>bc</p></td>
<td align="left"><p>リストからブレークポイントを削除します。 すべてのブレークポイントをクリアするには、bc * を使用します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>bd</p></td>
<td align="left"><p>ブレークポイントを無効にします。 すべてのブレークポイントを無効にするには、bd * を使用します。</p></td>
</tr>
<tr class="even">
<td align="left"><p>べき</p></td>
<td align="left"><p>ブレークポイントを有効にします。 すべてのブレークポイントを有効にするには、Use * を使用します。</p></td>
</tr>
</tbody>
</table>



または、[WinDbg] の [&gt; の**ブレークポイント**の**編集**] をクリックして、ブレークポイントを変更することもできます。 [ブレークポイント] ダイアログボックスは、既存のブレークポイントでのみ機能することに注意してください。 新しいブレークポイントは、コマンドラインから設定する必要があります。



**注:**  
**メモリアクセスブレークポイントの設定**

メモリ位置にアクセスしたときに起動するブレークポイントを設定することもできます。 次の構文を使用して、 **ba** (アクセス時の中断) コマンドを使用します。

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
<td align="left"><p>e</p></td>
<td align="left"><p>実行 (CPU がアドレスから命令をフェッチする場合)</p></td>
</tr>
<tr class="even">
<td align="left"><p>r</p></td>
<td align="left"><p>読み取り/書き込み (CPU がそのアドレスに対して読み取りまたは書き込みを行う場合)</p></td>
</tr>
<tr class="odd">
<td align="left"><p>w</p></td>
<td align="left"><p>書き込み (CPU がそのアドレスに書き込む場合)</p></td>
</tr>
</tbody>
</table>



常に4つのデータブレークポイントを設定できます。また、データを適切に配置していることを確認してください。または、ブレークポイントをトリガーしないことに注意してください (単語は2で割り切れるアドレスで終わる必要があります。、、および0または8によって quadwords)。

たとえば、特定のメモリアドレスに読み取り/書き込みブレークポイントを設定するには、次のようなコマンドを使用します。

```dbgcmd
ba r 4 0x0003f7bf0
```



**注:**  
**デバッガーからのコードのステップ実行コマンドウィンドウ**

コードをステップ実行するために使用できるコマンドを次に示します (関連するキーボードショートカットをかっこ内に示します)。

-   ブレークイン (Ctrl + Break)-このコマンドは、システムが実行されていて、WinDbg と通信している限り、システムを中断します (カーネルデバッガーのシーケンスは Ctrl + C です)。

-   カーソル行の前まで実行 (F7 または Ctrl + F10) –実行を中断するソースウィンドウまたは逆アセンブルウィンドウにカーソルを置き、F7 キーを押します。コードの実行は、その時点まで実行されます。 コード実行のフローがカーソルによって示されたポイントに届かない場合 (IF ステートメントが実行されない場合)、コードの実行が示されたポイントに届かなかったため、WinDbg は中断されません。

-   Run (F5) –ブレークポイントが検出されるか、バグチェックなどのイベントが発生するまで実行されます。

-   ステップオーバー (F10) –このコマンドは、一度に1つのステートメントまたは1つの命令を実行します。 呼び出しが検出されると、呼び出されたルーチンを入力せずに、その呼び出しに対してコードの実行が渡されます。 (プログラミング言語が C またC++はであり、WinDbg がソースモードの場合、ソースモードは**デバッグ**&gt;**ソースモード**) を使用して有効または無効にすることができます。

-   ステップイン (F11) –このコマンドは、呼び出しの実行が呼び出されたルーチンに送られる点を除いて、ステップオーバーに似ています。

-   ステップアウト (Shift + F11) –このコマンドは、現在のルーチン (呼び出し履歴の現在の場所) を実行し、現在のルーチンから終了します。 これは、ルーチンを十分に経験している場合に便利です。



詳細については、デバッグリファレンスドキュメントの「 [WinDbg でのソースコードのデバッグ](source-window.md)」を参照してください。

## <a name="span-idviewingvariablesspanspan-idviewingvariablesspanspan-idviewingvariablesspansection-8-viewing-variables-and-call-stacks"></a><span id="ViewingVariables"></span><span id="viewingvariables"></span><span id="VIEWINGVARIABLES"></span>セクション 8: 変数と呼び出し履歴の表示

*セクション8では、変数と呼び出し履歴に関する情報を表示します。*

このラボでは、前に説明したプロセスを使用して、 [*AddDevice*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_add_device)ルーチンで停止していることを前提としています。 出力例を表示するには、必要に応じて、前述の手順を繰り返します。

**&lt;-ホストシステム**

**変数の表示**

ローカル変数を表示するには、[**ビュー**&gt;**ローカル**] メニュー項目を使用します。

![windbg ローカル変数ウィンドウ](images/debuglab-image-display-variables.png)

**グローバル変数**

グローバル変数アドレスの場所を確認するには、「 *? &lt;変数名&gt;* 」と入力します。

**ローカル変数**

**Dv**コマンドを入力すると、指定したフレームのすべてのローカル変数の名前と値を表示できます。

```dbgcmd
0: kd> dv
         Driver = 0x00001fff`7ff9c838
     DeviceInit = 0xffffd001`51978190
         status = 0n0
```

**呼び出し履歴**

**注:**  
呼び出し履歴は、プログラムカウンターの現在の場所に led がある関数呼び出しのチェーンです。 呼び出し履歴の一番上の関数は現在の関数であり、次の関数は、現在の関数を呼び出した関数です。

呼び出し履歴を表示するには、k\* コマンドを使用します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>kb</p></td>
<td align="left"><p>スタックと最初の3つのパラメーターを表示します。</p></td>
</tr>
<tr class="even">
<td align="left"><p>kp</p></td>
<td align="left"><p>スタックとパラメーターの完全な一覧を表示します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>kn</p></td>
<td align="left"><p>を使用すると、その隣にあるフレーム情報を含むスタックを表示できます。</p></td>
</tr>
</tbody>
</table>





**&lt;-ホストシステム**

1. 呼び出し履歴を使用可能な状態にしたままにする場合は、[**表示**&gt; の**呼び出し履歴**] をクリックして表示します。 ウィンドウの上部にある列をクリックして、追加情報の表示を切り替えます。

![windbg 表示呼び出し履歴ウィンドウ](images/debuglab-image-display-callstacks.png)

2. 破損状態のサンプルアダプターコードをデバッグしているときに、 **kn**コマンドを使用して呼び出し履歴を表示します。

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

呼び出し履歴には、カーネル (nt) がプラグアンドプレイコード (PnP) に呼び出されたことが示されます。これは、その後 echo driver **Deviceadd**関数を呼び出した driver framework CODE (WDF) と呼ばれます。

## <a name="span-iddisplayingprocessesandthreadsspanspan-iddisplayingprocessesandthreadsspanspan-iddisplayingprocessesandthreadsspansection-9-displaying-processes-and-threads"></a><span id="DisplayingProcessesAndThreads"></span><span id="displayingprocessesandthreads"></span><span id="DISPLAYINGPROCESSESANDTHREADS"></span>セクション 9: プロセスとスレッドの表示

### <a name="span-idprocessesspanspan-idprocessesspanspan-idprocessesspanprocesses"></a><span id="Processes"></span><span id="processes"></span><span id="PROCESSES"></span>プロセス

*セクション9では、カーネルモードで実行されているプロセスとスレッドに関する情報を表示します。*

**注:**  
プロセス情報は、 [ **! プロセス**](-process.md)デバッガー拡張機能を使用して表示または設定できます。 サウンドが再生されるときに使用されるプロセスを調べるために、ブレークポイントを設定します。



1. **&lt;-ホストシステム**

   **Dv**コマンドを入力して、 **EchoEvtIo**ルーチンに関連付けられているロケール変数を確認します。

   ```dbgcmd
   0: kd> dv ECHO!EchoEvtIo*
   ECHO!EchoEvtIoQueueContextDestroy
   ECHO!EchoEvtIoWrite
   ECHO!EchoEvtIoRead         
   ```

2. **Bc \*** を使用して、前のブレークポイントをクリアします。

   ```dbgcmd
   0: kd> bc *  
   ```

3. 3. 次のコマンドを使用して、 **EchoEvtIo**ルーチンにシンボルのブレークポイントを設定します。

   ```dbgcmd
   0: kd> bm ECHO!EchoEvtIo*
     2: aade5490          @!”ECHO!EchoEvtIoQueueContextDestroy”
     3: aade55d0          @!”ECHO!EchoEvtIoWrite”
     4: aade54c0          @!”ECHO!EchoEvtIoRead”
   ```

4. ブレークポイントを一覧表示して、ブレークポイントが適切に設定されていることを確認します。

   ```dbgcmd
   0: kd> bl
   1 e aabf0490 [c:\Samples\kmdf echo sample\c++\driver\autosync\queue.c @ 197]    0001 (0001) ECHO!EchoEvtIoQueueContextDestroy
   ...
   ```

5. コードの実行を再開するには、「 **g** 」と入力します。

   ```dbgcmd
   0: kd> g
   ```

6. **ターゲットシステムで &gt; を -する**

   ターゲットシステムで EchoApp ドライバーテストプログラムを実行します。

7. **&lt;-ホストシステム**

   テストアプリを実行すると、ドライバーの i/o ルーチンが呼び出されます。 これにより、ブレークポイントが起動され、ターゲットシステムでのドライバーコードの実行が停止します。

   ```dbgcmd
   Breakpoint 2 hit
   ECHO!EchoEvtIoWrite:
   fffff801`0bf95810 4c89442418      mov     qword ptr [rsp+18h],r8
   ```

8. Echoapp の実行に関連する現在のプロセスを表示するには、 **! process**コマンドを使用します。

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

   出力には、プロセスがドライバー書き込みイベントのブレークポイントにヒットしたときに実行されていた echoapp に関連付けられていることが示されています。 詳細については、「 [ **! process**](-process.md)」を参照してください。

9. すべてのプロセスの概要情報を表示するには、 **! process 0 0**を使用します。 出力で、CTRL キーを押しながら F キーを押して、echoapp イメージに関連付けられているプロセスの同じプロセスアドレスを検索します。 次に示す例では、プロセスのアドレスは ffffe0007e6a7780 です。

   ```dbgcmd
   ...

   PROCESS ffffe0007e6a7780
       SessionId: 1  Cid: 0f68    Peb: 7ff7cfe7a000  ParentCid: 0f34
       DirBase: 1f7fb9000  ObjectTable: ffffc001cec82780  HandleCount:  34.
       Image: echoapp.exe

   ...
   ```

10. このラボで後で使用するために echoapp に関連付けられているプロセス ID を記録します。 CTRL + C キーを使用して、後で使用するためにアドレスをコピーバッファーにコピーすることもできます。

    \_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_(echoapp プロセスアドレス)

11. Echoapp が実行を終了するまでコードを実行するには、必要に応じて「 **g** 」をデバッガーに入力します。 読み取りと書き込みイベントのブレークポイントが回数回ヒットします。 Echoapp が終了したら、CTRL + ScrLk (Ctrl + Break) キーを押してデバッガーを中断します。

12. 現在、別のプロセスが実行されていることを確認するには、 **! process**コマンドを使用します。 次に示す出力では、Image 値が*System*のプロセスが*Echo* Image 値と異なります。

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

    上記の出力は、OS を停止したときに、システムプロセス ffffe0007b65d900 が実行されていたことを示しています。

13. ここで、 **! process**コマンドを使用して、前に記録した echoapp に関連付けられているプロセス ID を確認します。 次に示すプロセスアドレスの例ではなく、前に記録した echoapp プロセスアドレスを指定します。

    ```dbgcmd
    0: kd> !process ffffe0007e6a7780
    TYPE mismatch for process object at 82a9acc0
    ```

    Echoapp プロセスが実行されなくなったため、プロセスオブジェクトは使用できなくなりました。

### <a name="span-idthreadsspanspan-idthreadsspanspan-idthreadsspanthreads"></a><span id="Threads"></span><span id="threads"></span><span id="THREADS"></span>レッド

**注:**  
スレッドを表示および設定するコマンドは、プロセスのコマンドとよく似ています。 スレッドを表示するには、 [ **! thread**](-thread.md)コマンドを使用します。 [**スレッド**](-thread--set-register-context-.md)を使用して、現在のスレッドを設定します。



1.  **&lt;-ホストシステム**

    デバッガーに**g**を入力して、ターゲットシステムでコードの実行を再開します。

2.  **ターゲットシステムで &gt; を -する**

    ターゲットシステムで EchoApp ドライバーテストプログラムを実行します。

3.  **&lt;-ホストシステム**

    ブレークポイントにヒットすると、コードの実行は停止します。

    ```dbgcmd
    Breakpoint 4 hit
    ECHO!EchoEvtIoRead:
    aade54c0 55              push    ebp
    ```

4.  実行中のスレッドを表示するには、「 [ **! thread**](-thread.md)」と入力します。 次のような情報が表示されます。

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

    *Echoapp*のイメージ名をメモしておきます。これは、テストアプリに関連付けられているスレッドを調べていることを示しています。

5.  4. **! Process**コマンドを使用して、echoapp に関連付けられているプロセスで実行されている唯一のスレッドであるかどうかを確認します。 プロセスで実行されているスレッドのスレッド番号は、! thread コマンドを表示したスレッドと同じスレッドであることに注意してください。

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

6.  **! Process 0 0 コマンド**を使用して、関連する2つのプロセスのプロセスアドレスを検索し、これらのプロセスアドレスをここに記録します。

    Cmd.exe: \_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_に \_ます。t_36_ \_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_

    EchoApp: \_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_(\_\_\_\_\_t_36_ \_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_

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

    **メモ** また、 **! process 0 17**を使用して、すべてのプロセスに関する詳細情報を表示することもできます。 このコマンドからの出力には時間がかかる場合があります。 Ctrl キーを押しながら F キーを押すと、出力を検索できます。



7.  PC を実行している両方のプロセスのプロセス情報を一覧表示するには、 **! process**コマンドを使用します。 次に示すアドレスではなく、 **! process 0 0**出力からプロセスアドレスを指定します。

    この例の出力は、前に記録された cmd.exe プロセス ID 用です。 このプロセス ID のイメージ名は cmd.exe であることに注意してください。

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

    この例の出力は、前に記録された echoapp プロセス ID を対象としています。

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

8.  ここでは、2つのプロセスに関連付けられている最初のスレッドアドレスを記録します。

    Cmd.exe: \_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_に \_ます。t_36_ \_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_

    EchoApp: \_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_(\_\_\_\_\_t_36_ \_\_\_\_\_\_\_\_\_\_\_\_\_\_\_

9.  を使用します **。** 現在のスレッドに関する情報を表示するスレッドコマンド。

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

    予想どおり、現在のスレッドは echoapp に関連付けられているスレッドであり、実行中の状態です。

10. を使用します **。** Cmd.exe プロセスに関連付けられているスレッドに関する情報を表示するスレッドコマンド。 前に記録したスレッドアドレスを指定します。

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

    このスレッドは cmd.exe に関連付けられており、待機状態になっています。

11. 待機中の CMD.EXE スレッドのスレッドアドレスを指定して、その待機中のスレッドにコンテキストを変更します。

    ```dbgcmd
    0: kd> .Thread ffffe0007cf34880
    Implicit thread is now ffffe000`7cf34880
    ```

12. **K**コマンドを使用して、待機中のスレッドに関連付けられている呼び出し履歴を表示します。

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

    **KiCommitThreadWait**などの呼び出し履歴要素は、このスレッドが想定どおりに実行されていないことを示します。

**注:**  
スレッドとプロセスの詳細については、次の参照情報を参照してください。

[スレッドとプロセス](threads-and-processes.md)

[コンテキストの変更](changing-contexts.md)



## <a name="span-idsection_10__irql__registers_and_ending_the_windbg_sessionspanspan-idsection_10__irql__registers_and_ending_the_windbg_sessionspanspan-idsection_10__irql__registers_and_ending_the_windbg_sessionspansection-10-irql-registers-and-ending-the-windbg-session"></a><span id="Section_10__IRQL__Registers_and_Ending_the_WinDbg_session"></span><span id="section_10__irql__registers_and_ending_the_windbg_session"></span><span id="SECTION_10__IRQL__REGISTERS_AND_ENDING_THE_WINDBG_SESSION"></span>セクション 10: IRQL、登録、および WinDbg セッションの終了

### <a name="span-idirqlregistersmemoryspanspan-idirqlregistersmemoryspanspan-idirqlregistersmemoryspanviewing-the-saved-irql"></a><span id="IRQLRegistersMemory"></span><span id="irqlregistersmemory"></span><span id="IRQLREGISTERSMEMORY"></span>保存された IRQL の表示

*セクション10では、IRQL と、regsisters の内容を表示します。*

**&lt;-ホストシステム**

割り込み要求レベル (IRQL) は、割り込みサービスの優先順位を管理するために使用されます。 各プロセッサには、スレッドが発生させることのできる IRQL の設定があります。 プロセッサの IRQL 設定の下または下で発生する割り込みはマスクされ、現在の操作に干渉することはありません。 プロセッサの IRQL 設定を超える割り込みは、現在の操作よりも優先されます。 [ **! Irql**](-irql.md) extension は、デバッガーが中断される前に、対象のコンピューターの現在のプロセッサに割り込み要求レベル (irql) を表示します。 対象のコンピューターがデバッガーに分割されると、IRQL は変わりますが、デバッガーの中断直前に有効だった IRQL は保存され、 **! irql**によって表示されます。

```dbgcmd
0: kd> !irql
Debugger saved IRQL for processor 0x0 -- 2 (DISPATCH_LEVEL)
```

### <a name="span-idviewingtheregistersspanspan-idviewingtheregistersspanspan-idviewingtheregistersspanviewing-the-registers"></a><span id="ViewingTheRegisters"></span><span id="viewingtheregisters"></span><span id="VIEWINGTHEREGISTERS"></span>レジスタの表示

**&lt;-ホストシステム**

[**R (register)** ](r--registers-.md)コマンドを使用して、現在のプロセッサの現在のスレッドのレジスタの内容を表示します。

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

または、[&gt;**レジスタ**の**表示**] をクリックしてレジスタの内容を表示することもできます。 詳細については、「 [**r (レジスタ)** ](r--registers-.md)」を参照してください。

レジスタの内容を表示することは、アセンブリ言語コードの実行やその他のシナリオでステップ実行するときに役立ちます。 アセンブリ言語の逆アセンブリの詳細については、「[注釈付き X86 逆アセンブリ](annotated-x86-disassembly.md)」および「[注釈付き x64 逆アセンブル](annotated-x64-disassembly.md)」を参照してください。

レジスタの内容の詳細については、「 [X86 アーキテクチャ](x86-architecture.md)と[x64 アーキテクチャ](x64-architecture.md)」を参照してください。

### <a name="span-idendingthesessionspanspan-idendingthesessionspanspan-idendingthesessionspanending-the-windbg-session"></a><span id="EndingTheSession"></span><span id="endingthesession"></span><span id="ENDINGTHESESSION"></span>WinDbg セッションを終了しています

**&lt;-ホストシステム**

ユーザーモードのデバッグセッションを終了し、デバッガーを休止モードに戻して、ターゲットアプリケーションを再度実行するように設定するには、 **qd** (Quit および Detach) コマンドを入力します。

使用できるように、ターゲットコンピューターにコードを実行させるには、必ず**g**コマンドを使用してください。 また、 **bc \*** を使用してブレークポイントをクリアし、対象のコンピュータが中断してホストコンピュータデバッガーに接続しようとしないようにすることをお勧めします。

```dbgcmd
0: kd> qd
```

詳細については、デバッグリファレンスドキュメントの「 [WinDbg でのデバッグセッションの終了](ending-a-debugging-session-in-windbg.md)」を参照してください。

## <a name="span-idwindowsdebuggingresourcesspanspan-idwindowsdebuggingresourcesspanspan-idwindowsdebuggingresourcesspansection-11-windows-debugging-resources"></a><span id="WindowsDebuggingResources"></span><span id="windowsdebuggingresources"></span><span id="WINDOWSDEBUGGINGRESOURCES"></span>セクション 11: Windows デバッグリソース


詳細については、「Windows デバッグ」を参照してください。 これらの書籍には、windows Vista などの古いバージョンの Windows を例で使用するものがありますが、ここで説明する概念は、Windows のほとんどのバージョンに適用されます。

**参考**

-   Mario Hewardt と Daniel Pravat による高度な Windows デバッグ

-   Windows のデバッグ: Tarik Soulami による Windows®でのデバッグとトレースの方法に関する実用的なガイド

-   Windows の内部構造をマーク Russinovich、David A ソロモン、Alex Ionescu

**ビデオ**

デフラグツールでは、WinDbg エピソード13-29 が表示され <https://channel9.msdn.com/Shows/Defrag-Tools>

**ベンダーのトレーニング:**

OSR <https://www.osr.com/>

## <a name="span-idrelated_topicsspanrelated-topics"></a><span id="related_topics"></span>関連トピック


[標準的なデバッグ手法](standard-debugging-techniques.md)

[特化されたデバッグ手法](specialized-debugging-techniques.md)

[Windows のデバッグの概要](getting-started-with-windows-debugging.md)











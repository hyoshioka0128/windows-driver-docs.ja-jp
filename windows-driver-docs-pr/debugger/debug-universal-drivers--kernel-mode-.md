---
title: デバッグドライバー-ステップバイステップラボ (Sysvad カーネルモード)
description: このラボでは、Sysvad audio カーネルモードデバイスドライバーをデバッグする方法を示すハンズオン演習を提供します。
ms.assetid: 4A31451C-FC7E-4C5F-B4EB-FBBAC8DADF9E
keywords:
- ラボのデバッグ
- ステップバイステップ
- SYSVAD
ms.date: 07/20/2020
ms.localizationpriority: medium
ms.openlocfilehash: 9969117b36fa135378653580b41fe26991181ba7
ms.sourcegitcommit: a0e6830b125a86ac0a0da308d5bf0091e968b787
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/21/2020
ms.locfileid: "86557782"
---
# <a name="span-iddebuggerdebug_universal_drivers__kernel-mode_spandebug-drivers---step-by-step-lab-sysvad-kernel-mode"></a><span id="debugger.debug_universal_drivers__kernel-mode_"></span>デバッグドライバー-ステップバイステップラボ (Sysvad カーネルモード)

このラボでは、Sysvad audio カーネルモードデバイスドライバーをデバッグする方法を示すハンズオン演習を提供します。

Microsoft Windows デバッガー (WinDbg) は、ユーザーモードおよびカーネルモードのデバッグを実行するために使用できる強力な Windows ベースのデバッグツールです。 WinDbg は、Windows カーネル、カーネルモードドライバー、およびシステムサービスのソースレベルのデバッグだけでなく、ユーザーモードのアプリケーションとドライバーにも対応しています。

WinDbg では、ソースコードをステップ実行したり、ブレークポイントを設定したり、変数 (C++ オブジェクトを含む)、スタックトレース、およびメモリを表示したりできます。 デバッガーコマンドウィンドウを使用すると、ユーザーはさまざまなコマンドを発行できます。

## <a name="span-idlab_setupspanlab-setup"></a><span id="lab_setup"></span>ラボのセットアップ

ラボを完了するには、次のハードウェアが必要です。

-   Windows 10 を実行するラップトップまたはデスクトップコンピューター (ホスト)
-   Windows 10 を実行するラップトップまたはデスクトップコンピューター (ターゲット)
-   2台の Pc を接続するためのネットワークハブ/ルーターとネットワークケーブル
-   シンボルファイルをダウンロードするためのインターネットへのアクセス

ラボを完成させるには、次のソフトウェアが必要です。

-   Microsoft Visual Studio 2017
-   Windows 10 用 Windows ソフトウェア開発キット (SDK)
-   Windows 10 用 windows Driver Kit (WDK)
-   Windows 10 用のサンプル Sysvad audio driver

WDK のダウンロードとインストールの詳細については、「 [Windows Driver Kit (wdk) のダウンロード](https://docs.microsoft.com/windows-hardware/drivers/download-the-wdk)」を参照してください。

## <a name="span-idsysvad_debugging_walkthrough_overviewspansysvad-debugging-walkthrough"></a><span id="sysvad_debugging_walkthrough_overview"></span>Sysvad デバッグのチュートリアル


このラボでは、カーネルモードドライバーのデバッグプロセスについて説明します。 演習では、Syvad 仮想オーディオドライバーのサンプルを使用します。 Syvad audio ドライバーは実際のオーディオハードウェアとは通信しないため、ほとんどのデバイスで使用できます。 このラボでは、次のタスクについて説明します。

-   [セクション 1: カーネルモードの WinDbg セッションに接続する](#connectto)
-   [セクション 2: カーネルモードのデバッグコマンドと手法](#kernelmodedebuggingcommandsandtechniques)
-   [セクション 3: Sysvad オーディオドライバーをダウンロードしてビルドする](#download)
-   [セクション 4: ターゲットシステムに Sysvad audio driver をインストールする](#install)
-   [セクション 5: WinDbg を使用してドライバーに関する情報を表示する](#usewindbgtodisplayinformation)
-   [セクション 6: プラグアンドプレイデバイスツリー情報を表示する](#displayingtheplugandplaydevicetree)
-   [セクション 7: ブレークポイントとソースコードの操作](#workingwithbreakpoints)
-   [セクション 8: 変数の確認](#lookingatvariables)
-   [セクション 9: 呼び出し履歴を表示する](#viewingcallstacks)
-   [セクション 10: プロセスとスレッドを表示する](#displayingprocessesandthreads)
-   [セクション 11: IRQL、レジスタ、および逆アセンブリ](#irqlregistersmemory)
-   [セクション 12: メモリの操作](#workingwithmemory)
-   [セクション 13: WinDbg セッションを終了する](#endingthesession)
-   [セクション 14: Windows デバッグリソース](#windowsdebuggingresources)

## <a name="span-idecho_driver_labspanecho-driver-lab"></a><span id="echo_driver_lab"></span>Echo ドライバーラボ


Echo ドライバーは、Sysvad audio ドライバーよりも単純なドライバーです。 WinDbg を初めて使用する場合は、最初に「[ユニバーサルドライバーのデバッグ-ステップバイステップラボ (Echo カーネルモード)](debug-universal-drivers---step-by-step-lab--echo-kernel-mode-.md)」を完了することを検討してください。 このラボでは、そのラボのセットアップの指示を再利用します。そのため、ラボが完成したら、セクション1と2をスキップできます。

## <a name="span-idconnecttospansection-1-connect-to-a-kernel-mode-windbg-session"></a><span id="connectto"></span>セクション 1: カーネルモードの WinDbg セッションに接続する


*セクション1では、ホストとターゲットシステムでネットワークデバッグを構成します。*

このラボの Pc は、カーネルデバッグにイーサネットネットワーク接続を使用するように構成する必要があります。

このラボでは2台のコンピューターを使用します。 WinDbg は*ホスト*システム上で実行され、Sysvad ドライバーは*ターゲット*システムで実行されます。

 ネットワークハブ/ルーターとネットワークケーブルを使用して、2台の Pc を接続します。

![2つの pc が二重矢印で接続されている](images/debuglab-image-targethostdrawing1.png)

カーネルモードのアプリケーションを操作し、WinDbg を使用するには、KDNET over イーサネット転送を使用することをお勧めします。 イーサネットトランスポートプロトコルの使用方法の詳細については、「 [WinDbg を使用したはじめに (カーネルモード)](getting-started-with-windbg--kernel-mode-.md)」を参照してください。 ターゲットコンピューターの設定の詳細については、「[ドライバーの手動展開のためのコンピューターの準備](https://docs.microsoft.com/windows-hardware/drivers)」および「 [KDNET Network カーネルデバッグの自動](setting-up-a-network-debugging-connection-automatically.md)セットアップ」を参照してください。

### <a name="span-idconfigure__kernel_mode_debugging_using_ethernetspanconfigure-kernelmode-debugging-using-ethernet"></a><span id="configure__kernel_mode_debugging_using_ethernet"></span>イーサネットを使用してカーネルモードのデバッグを構成する

ターゲットシステムでカーネルモードのデバッグを有効にするには、次の手順を実行します。

**&lt;-ホストシステム上**

1. ホストシステムでコマンドプロンプトを開き、「 **ipconfig/all** 」と入力して IP アドレスを決定します。

```console
C:\>ipconfig /all
Windows IP Configuration

 Host Name . . . . . . . . . . . . : TARGETPC
...

Ethernet adapter Ethernet:
   Connection-specific DNS Suffix  . :
   Link-local IPv6 Address . . . . . : fe80::c8b6:db13:d1e8:b13b3
   Autoconfiguration IPv4 Address. . : 169.182.1.1
   Subnet Mask . . . . . . . . . . . : 255.255.0.0
   Default Gateway . . . . . . . . . :
```

2. ホストシステムの IP アドレスを記録します。\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_

3. ホストシステムのホスト名を記録します。\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_

**-&gt;ターゲットシステム上**

4. ターゲットシステムでコマンドプロンプトを開き、 **ping**コマンドを使用して、2つのシステム間のネットワーク接続を確認します。 サンプル出力に示されている169.182.1.1 ではなく、記録したホストシステムの実際の IP アドレスを使用します。

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

KDNET ユーティリティを使用してターゲットシステムでカーネルモードのデバッグを有効にするには、次の手順を実行します。

1. ホストシステムで、WDK KDNET ディレクトリに移動します。 既定では、この場所にあります。

   C:\Program Files (x86) \Windows Kits\10\Debuggers\x64

> [!NOTE]
> このラボでは、両方の Pc がターゲットとホストの両方で64ビットバージョンの Windowson を実行していることを前提としています。 そうでない場合は、ターゲットが実行されているホストで同じ "ビット" のツールを実行するのが最善の方法です。 たとえば、ターゲットが32ビット Windows を実行している場合は、ホストで32バージョンのデバッガーを実行します。 詳細については、「 [32 ビットまたは64ビットのデバッグツールの選択](choosing-a-32-bit-or-64-bit-debugger-package.md)」を参照してください。
> 

2. これらの2つのファイルを検索し、それらをネットワーク共有またはサムドライブにコピーして、ターゲットコンピューターで使用できるようにします。

    kdnet.exe

    VerifiedNICList.xml


3. ターゲット コンピューターで、管理者としてコマンド プロンプト ウィンドウを開きます。 次のコマンドを入力して、ターゲット PC の NIC がサポートされされていることを確認します。

```console
C:\KDNET>kdnet

Network debugging is supported on the following NICs:
busparams=0.25.0, Intel(R) 82579LM Gigabit Network Connection, KDNET is running on this NIC.kdnet.exe
```

4. 次のコマンドを入力して、ホストシステムの IP アドレスを設定します。 サンプル出力に示されている169.182.1.1 ではなく、記録したホストシステムの実際の IP アドレスを使用します。 50010など、使用するターゲット/ホストペアごとに一意のポートアドレスを選択します。

```console
C:\>kdnet 169.182.1.1 50010

Enabling network debugging on Intel(R) 82577LM Gigabit Network Connection.
Key=2steg4fzbj2sz.23418vzkd4ko3.1g34ou07z4pev.1sp3yo9yz874p
```

> [!IMPORTANT]
> BCDEdit を使用してブート情報を変更する前に、テスト PC で BitLocker やセキュアブートなどの Windows のセキュリティ機能を一時的に停止することが必要になる場合があります。
> セキュリティ機能が無効になっている場合は、テストが完了し、テスト PC を適切に管理するときに、これらのセキュリティ機能を再び有効にします。
>

5. 次のコマンドを入力して、dbgsettings が適切に設定されていることを確認します。

```console
C:\> bcdedit /dbgsettings
busparams               0.25.0
key                     2steg4fzbj2sz.23418vzkd4ko3.1g34ou07z4pev.1sp3yo9yz874p
debugtype               NET
hostip                  169.182.1.1
port                    50010
dhcp                    Yes
The operation completed successfully.
```

自動生成された一意キーをテキストファイルにコピーして、ホスト PC に入力しなくても済むようにします。 キーを含むテキストファイルをホストシステムにコピーします。

**メモ**   
**ファイアウォールとデバッガー**

ファイアウォールからポップアップメッセージを受信し、デバッガーを使用する場合は、 **3 つすべて**のチェックボックスをオンにします。

![windows セキュリティの警告-windows ファイアウォールがこのアプリの一部の機能をブロックしました](images/debuglab-image-firewall-dialog-box.png)
 

**&lt;-ホストシステム上**

1. ホスト コンピューターで、管理者としてコマンド プロンプト ウィンドウを開きます。 WinDbg.exe ディレクトリに移動します。 Windows キットの一部としてインストールされた Windows Driver Kit (WDK) に含まれる WinDbg.exe の x64 バージョンを使います。

```console
C:\> Cd C:\Program Files (x86)\Windows Kits\10\Debuggers\x64 
```

2. 次のコマンドを使用して、リモートユーザーデバッグで WinDbg を起動します。 キーとポートの値は、ターゲットで BCDEdit を使用して以前に設定したものと一致します。

```console
C:\> WinDbg –k net:port=50010,key=2steg4fzbj2sz.23418vzkd4ko3.1g34ou07z4pev.1sp3yo9yz874p
```

**-&gt;ターゲットシステム上**

ターゲットシステムを再起動します。

**&lt;-ホストシステム上**

1 ~ 2 分で、デバッグ出力がホストシステムに表示されます。

![ライブカーネル接続からのコマンドウィンドウ出力を示す windows デバッガー](images/debuglab-image-winddbg-hh.png)

デバッガーコマンドウィンドウは、WinDbg の主要なデバッグ情報ウィンドウです。 このウィンドウでは、デバッガーコマンドを入力し、コマンドの出力を表示できます。

デバッガーコマンドウィンドウが2つのペインに分割されます。 ウィンドウの下部にある小さいウィンドウ (コマンド入力ウィンドウ) にコマンドを入力すると、ウィンドウの上部にある大きなウィンドウにコマンドの出力が表示されます。

コマンド入力ウィンドウで、上方向キーと下方向キーを使用して、コマンド履歴をスクロールします。 コマンドが表示されたら、それを編集するか、enter キーを押して**コマンドを実行**します。

## <a name="span-idkernelmodedebuggingcommandsandtechniquesspansection-2-kernel-mode-debugging-commands-and-techniques"></a><span id="kernelmodedebuggingcommandsandtechniques"></span>セクション 2: カーネルモードのデバッグコマンドと手法


*セクション2では、デバッグコマンドを使用して、ターゲットシステムに関する情報を表示します。*

**&lt;-ホストシステム上**

**でデバッガーマークアップ言語 (DML) を有効にします。 dml を優先します \_**

一部のデバッグコマンドでは、デバッガーのマークアップ言語を使用してテキストを表示します。これをクリックすると、詳細情報をすばやく収集できます。

1. WinDBg で Ctrl + Break (スクロールロック) を使用して、ターゲットシステムで実行されているコードを中断します。 ターゲットシステムが応答するまでに少し時間がかかる場合があります。
2. 次のコマンドを入力して、コマンドウィンドウデバッガーで DML を有効にします。

```dbgcmd
0: kd> .prefer_dml 1
DML versions of commands on by default
```

**. Hh を使用してヘルプを表示する**

参照コマンドのヘルプには、 **. hh**コマンドを使用してアクセスできます。

3. 次のコマンドを入力して、のコマンドリファレンスヘルプを表示**します。 \_ dml を優先**します。
   ```dbgcmd
   0: kd> .hh .prefer_dml
   ```

デバッガーヘルプファイルには、[ ** \_ dml を優先**] コマンドのヘルプが表示されます。

![デバッガーヘルプアプリケーションのヘルプを表示します。 dml コマンドを使用します。 \-](images/debuglab-image-prefer-dml-help.png)

**ターゲットシステムで Windows のバージョンを表示する**

5. [WinDbg] ウィンドウで、 [**vertarget (ターゲットコンピューターのバージョンを表示)**](vertarget--show-target-computer-version-.md)コマンドを入力して、ターゲットシステムの詳細なバージョン情報を表示します。

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

6. 適切なカーネルモードプロセスを使用していることを確認するには、[WinDbg] ウィンドウで [ [**lm (List Loaded modules)**](lm--list-loaded-modules-.md) ] コマンドを入力して、読み込まれたモジュールを表示します。

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

**メモ**   省略された出力は、"... "このラボでは、

 

シンボルパスと読み込まれたシンボルをまだ設定していないので、デバッガーで使用できる情報は限られています。

## <a name="span-iddownloadspansection-3-download-and-build-the-sysvad-audio-driver"></a><span id="download"></span>セクション 3: Sysvad オーディオドライバーをダウンロードしてビルドする


*セクション3では、Sysvad オーディオドライバーをダウンロードしてビルドします。*

通常、WinDbg を使用する場合は、独自のドライバーコードを使用します。 オーディオドライバーのデバッグに慣れるには、Sysvad virtual audio サンプルドライバーを使用します。 このサンプルは、ネイティブカーネルモードコードをシングルステップ実行する方法を示すために使用されます。 この手法は、複雑なカーネルモードコードの問題をデバッグする場合に非常に役立ちます。

Sysvad サンプルオーディオドライバーをダウンロードしてビルドするには、次の手順を実行します。

1.  **GitHub から Sysvad audio サンプルをダウンロードして抽出する**

    ブラウザーを使用して、Sysvad サンプルと Readme.md ファイルをここに表示できます。

    [https://github.com/Microsoft/Windows-driver-samples/tree/master/audio/sysvad](https://github.com/Microsoft/Windows-driver-samples/blob/97cf5197cf5b882b2c689d8dc2b555f2edf8f418/general/echo/kmdf/ReadMe.md)

    ![一般的なフォルダーとダウンロード用 zip ボタンを示す github リポジトリ](images/sysvad-lab-github.png)

    このラボでは、ユニバーサルドライバーのサンプルを1つの zip ファイルにダウンロードする方法を示します。

    a. master.zip ファイルをローカルハードドライブにダウンロードします。

    <https://github.com/Microsoft/Windows-driver-samples/archive/master.zip>

    b. *Windows-driver-samples-master.zip*を右クリックし、[**すべて展開**] を選択します。 新しいフォルダーを指定するか、抽出されたファイルを格納する既存のフォルダーを参照します。 たとえば、ファイルを抽出する新しいフォルダーとして*C: \\ WDK \_ サンプル \\ *を指定できます。

    c. ファイルが抽出されたら、次のサブフォルダーに移動します。

    *C: \\ WDK \_ サンプル \\ Sysvad*

2.  **Visual Studio でドライバーソリューションを開く**

    Visual Studio で、[**ファイル**] [開く] [ &gt; **Open** &gt; **プロジェクト/ソリューション...** ] の順にクリックし、抽出したファイルが格納されているフォルダーに移動します (例: *C: \\ WDK \_ Samples \\ Sysvad*)。 *Syvad*ソリューションファイルをダブルクリックします。

    Visual Studio で、ソリューションエクスプローラーを見つけます。 (まだ開いていない場合は、[**表示**] メニューの [**ソリューションエクスプローラー** ] をクリックします)。ソリューションエクスプローラーでは、いくつかのプロジェクトを含む1つのソリューションと、サンプル変更に含まれるものを随時確認できます。 
        
    ![sysvad プロジェクトから読み込まれたデバイス .c ファイルを使用した visual studio](images/sysvad-lab-visual-studio-solution.png)

3.  **サンプルの構成とプラットフォームを設定する**

    ソリューションエクスプローラーで、[**ソリューション ' sysvad ' (7 プロジェクト)**] を右クリックし、[ **Configuration Manager**] を選択します。 4つのプロジェクトの構成とプラットフォームの設定が同じであることを確認します。 既定では、構成は "Win10 Debug" に設定され、プラットフォームはすべてのプロジェクトに対して "Win64" に設定されます。 1つのプロジェクトで構成やプラットフォームを変更した場合は、残りの3つのプロジェクトに対しても同じ変更を行う必要があります。

    **メモ**   このラボでは、64ビットの Windows が使用されていることを前提としています。 32ビットの Windows を使用している場合は、32ビットのドライバーをビルドします。

     

4.  **ドライバーの署名を確認する**

    TabletAudioSample を見つけます。 Sysvad ドライバーのプロパティページを開き、**ドライバー署名** &gt; **署名モード**が [*テスト署名*] に設定されていることを確認します。

5.  **Visual Studio を使用してサンプルをビルドする**

    Visual Studio で **、[ビルド**] [ソリューションのビルド] の順にクリックし &gt; **Build Solution**ます。

    ビルドウィンドウに、6つのプロジェクトすべてのビルドが成功したことを示すメッセージが表示されます。

6.  **ビルドされたドライバーファイルを検索する**

    ファイルエクスプローラーで、サンプルの抽出したファイルが格納されているフォルダーに移動します。 たとえば、前に指定したフォルダーである場合は、 *C: \\ WDK \_ Samples \\ Sysvad*に移動します。 このフォルダー内では、コンパイルされたドライバーファイルの場所は、 **Configuration Manager**で選択した構成とプラットフォームの設定によって異なります。 たとえば、既定の設定を変更せずに残した場合、コンパイルされたドライバーファイルは、64ビットのデバッグビルドの* \\ x64 \\ Debug*という名前のフォルダーに保存されます。

    TabletAudioSample ドライバーのビルドファイルが格納されているフォルダーに移動します。

    *C: \\WDK \_ サンプル \\ Sysvad \\ TabletAudioSample \\ x64 \\ Debug*。 フォルダーには TabletAudioSample が含まれます。SYS ドライバー、シンボル pdp ファイル、および inf ファイル。 また、SwapAPO と KeywordDetectorContosoAdapter dll およびシンボルファイルを検索する必要があります。

    ドライバーをインストールするには、次のファイルが必要です。

    | ファイル名                         | 説明                                                                       |
    |-----------------------------------|-----------------------------------------------------------------------------------|
    | TabletAudioSample.sys             | ドライバーファイル。                                                                  |
    | TabletAudioSample             | ドライバーシンボルファイル。                                                           |
    | tabletaudiosample             | ドライバーのインストールに必要な情報が含まれている情報 (INF) ファイル。 |
    | KeywordDetectorContosoAdapter  | キーワード検出機能のサンプルです。                                                        |
    | KeywordDetectorContosoAdapter | Sample キーワード検出シンボルファイル。                                          |
    | lSwapAPO.dll                      | APOs を管理するための UI のサンプルドライバー拡張機能。                                |
    | lSwapAPO .pdb                      | APO UI シンボルファイル。                                                           |
    | TabletAudioSample             | TabletAudioSample 証明書ファイル。                                           |

     

7.  USB ドライブを探すか、ネットワーク共有をセットアップして、ホストからターゲットシステムに構築されたドライバーファイルをコピーします。

次のセクションでは、コードをターゲットシステムにコピーし、ドライバーをインストールしてテストします。

## <a name="span-idinstallspansection-4-install-the-sysvad-audio-driver-sample-on-the-target-system"></a><span id="install"></span>セクション 4: ターゲットシステムに Sysvad audio driver サンプルをインストールする

*セクション4では、devcon を使用して Sysvad audio ドライバーをインストールします。*

**-&gt;ターゲットシステム上**

ドライバーをインストールするコンピューターは、*ターゲットコンピューター*または*テストコンピューター*と呼ばれます。 通常、これは、ドライバーパッケージを開発およびビルドするコンピューターとは別のコンピューターです。 ドライバーを開発してビルドするコンピューターは、*ホストコンピューター*と呼ばれます。

ドライバーパッケージを対象のコンピューターに移動し、ドライバーをインストールするプロセスを、ドライバーの*展開*と呼びます。

ドライバーを展開する前に、テスト署名をオンにして、対象のコンピューターを準備する必要があります。  その後、ビルドされたドライバーのサンプルをターゲットシステムで実行する準備ができました。

ターゲットシステムにドライバーをインストールするには、次の手順を実行します。

1.  **署名済みドライバーのテストを有効にする**

    署名済みドライバーのテストを実行する機能を有効にするには、次のようにします。

    1. Windows の設定を開きます。

    2. [**更新とセキュリティ**] で、[**回復**] を選択します。

    3. [**詳細なスタートアップ**] の [**今すぐ再起動**] をクリックします。

    4. PC が再起動したら、[**トラブルシューティング**] を選択します。

    5. [**詳細オプション**]、[**スタートアップの設定**] の順に選択し、[**再起動**] をクリックします。

    6. **F7**キーを押して [ドライバー署名の強制を無効にする] を選択します。

    7. 新しい値が設定された状態で PC が起動します。


3.  **-&gt;ターゲットシステム上**

    **ドライバーのインストール**

    次の手順では、サンプルドライバーをインストールしてテストする方法について説明します。

    このドライバーのインストールに必要な INF ファイルは*TabletAudioSample*です。 ターゲット コンピューターで、管理者としてコマンド プロンプト ウィンドウを開きます。 ドライバーパッケージフォルダーに移動し、TabletAudioSample ファイルを右クリックして、[**インストール**] を選択します。

    ダイアログ ボックスには、テスト ドライバーが署名されていないドライバーであることが示されます。 **[かまわず続行]** をクリックして続行します。

    ![windows セキュリティ警告-windows は発行元を確認できません](images/debuglab-image-install-security-warning.png)

    >[!TIP]
    > インストールに問題がある場合は、次のファイルで詳細を確認してください。
    `%windir%\inf\setupapi.dev.log`
    >
     
    詳細な手順については、「[ドライバーの展開、テスト、およびデバッグのためのコンピューターの構成](https://docs.microsoft.com/windows-hardware/drivers/gettingstarted/provision-a-target-computer-wdk-8-1)」を参照してください。

    INF ファイルには、 *tabletaudiosample.sys*をインストールするためのハードウェア ID が含まれています。 Syvad サンプルでは、ハードウェア ID は次のとおりです。`root\sysvad_TabletAudioSample`

4.  **デバイスマネージャーのドライバーを確認します。**

    ターゲットコンピューターのコマンドプロンプトウィンドウで、「 **devmgmt.msc** 」と入力してデバイスマネージャーを開きます。 デバイスマネージャーで、[表示] メニューの [**種類別のデバイス**] を選択します。

    デバイスツリーで、[オーディオデバイス] ノードの [*仮想オーディオデバイス (WDM)-タブレットのサンプル*] を見つけます。 通常は、[**サウンド、ビデオ、およびゲームコントローラー** ] ノードの下にあります。 インストールされてアクティブになっていることを確認します。

    デバイスマネージャーで、PC 上の実際のハードウェアのドライバーを強調表示します。 次に、ドライバーを右クリックし、[無効] をクリックしてドライバーを無効にします。

    [オーディオハードウェアドライバー] のデバイスマネージャーを確認すると、無効になっていることを示す下矢印が表示されます。

    ![仮想オーディオデバイスのタブレットサンプルが強調表示されているデバイスマネージャーツリー](images/sysvad-lab-audio-device-manager.png)

    サンプルドライバーが正常にインストールされたら、テストする準備ができました。

**Sysvad オーディオドライバーをテストする**

1. ターゲットコンピューターのコマンドプロンプトウィンドウで、「 **devmgmt.msc** 」と入力してデバイスマネージャーを開きます。 デバイスマネージャーで、[**表示**] メニューの [**種類別のデバイス**] を選択します。 デバイスツリーで、[*仮想オーディオデバイス (WDM)-タブレットのサンプル*] を見つけます。

2. コントロールパネルを開き、[**ハードウェアとサウンド**] [ &gt; **オーディオデバイスの管理**] に移動します。 [サウンド] ダイアログボックスで、[*仮想オーディオデバイス (WDM)-タブレットサンプル*] というラベルの付いたスピーカーアイコンを選択し、[**既定値に設定**] をクリックします。ただし、[ **OK**] はクリックしないでください。 これにより、[サウンド] ダイアログボックスが開いたままになります。
3. 対象のコンピューターで MP3 またはその他のオーディオファイルを見つけ、ダブルクリックして再生します。 次に、[サウンド] ダイアログボックスで、*仮想オーディオデバイス (WDM) のサンプル*ドライバーに関連付けられているボリュームレベルインジケーターにアクティビティがあることを確認します。

## <a name="span-idusewindbgtodisplayinformationspansection-5-use-windbg-to-display-information-about-the-driver"></a><span id="usewindbgtodisplayinformation"></span>セクション 5: WinDbg を使用してドライバーに関する情報を表示する


*セクション5では、シンボルパスを設定し、カーネルデバッガーコマンドを使用して Sysvad サンプルドライバーに関する情報を表示します。*

シンボルを使用すると、WinDbg は変数名などの追加情報を表示できますが、デバッグ時には非常に便利です。 WinDbg では、ソースレベルのデバッグに Microsoft Visual Studio デバッグシンボル形式が使用されます。 PDB シンボルファイルがあるモジュールから、任意のシンボルまたは変数にアクセスできます。

デバッガーを読み込むには、次の手順を実行します。

**&lt;-ホストシステム上**

1.  デバッガーを閉じた場合は、管理者のコマンドプロンプトウィンドウで次のコマンドを使用して、デバッガーを再度開きます。 キーとポートを、以前に構成したものに置き換えます。

    ```console
    C:\> WinDbg –k net:port=50010,key=2steg4fzbj2sz.23418vzkd4ko3.1g34ou07z4pev.1sp3yo9yz874p
    ```

2.  Ctrl + Break (スクロールロック) を使用して、ターゲットシステムで実行されているコードを中断します。

**シンボルパスを設定する**

1.  WinDbg 環境で Microsoft シンボルサーバーへのシンボルパスを設定するには、 **. symfix**コマンドを使用します。

    ```dbgcmd
    0: kd> .symfix
    ```

2.  ローカルシンボルを使用するようにローカルシンボルの場所を追加するには、 **. sympath +** を使用してパスを追加し、次に「」と入力し**ます。**

    ```dbgcmd
    0: kd> .sympath+ C:\WDK_Samples\Sysvad
    0: kd> .reload /f
    ```

    **メモ**    **/F** force オプションを指定した **. reload**コマンドは、指定されたモジュールのすべてのシンボル情報を削除し、シンボルを再読み込みします。 場合によっては、このコマンドによってモジュール自体が再読み込みまたはアンロードされることもあります。

     

**メモ**   WinDbg が提供する高度な機能を使用するには、適切なシンボルを読み込む必要があります。 シンボルが適切に構成されていない場合は、シンボルに依存する機能を使用しようとしたときにシンボルが使用できないことを示すメッセージが表示されます。

```dbgcmd
0:000> dv
Unable to enumerate locals, HRESULT 0x80004005
Private symbols (symbols.pri) are required for locals.
Type “.hh dbgerr005” for details.
```

 

**メモ**   
**シンボルサーバー**

シンボルを操作するために使用できるいくつかの方法があります。 多くの状況では、必要に応じて Microsoft が提供するシンボルサーバーからシンボルにアクセスするように PC を構成できます。 このチュートリアルでは、このアプローチが使用されることを前提としています。 環境内のシンボルが別の場所にある場合は、その場所を使用するようにステップを変更します。 詳細については、「[シンボルストアとシンボルサーバー](symbol-stores-and-symbol-servers.md)」を参照してください。

 

**メモ**   
**ソースコードシンボルの要件を理解**する

ソースのデバッグを実行するには、バイナリのチェック (デバッグ) バージョンを作成する必要があります。 コンパイラは、シンボルファイル (.pdb ファイル) を作成します。 これらのシンボルファイルは、バイナリ命令がソース行にどのように対応しているかをデバッガーで表示します。 実際のソースファイル自体には、デバッガーからもアクセスできる必要があります。

シンボルファイルには、ソースコードのテキストは含まれません。 デバッグの場合は、リンカーでコードを最適化しないことをお勧めします。 ソースのデバッグとローカル変数へのアクセスはより困難になります。また、コードが最適化されている場合は、ほぼ不可能な場合もあります。 ローカル変数またはソース行の表示に問題がある場合は、次のビルドオプションを設定します。

COMPILE_DEBUG の設定 = 1

ENABLE_OPTIMIZER の設定 = 0

 

1.  デバッガーのコマンド領域に次のように入力して、Sysvad ドライバーに関する情報を表示します。

    ```dbgcmd
    0: kd> lm m tabletaudiosample v
    Browse full module list
    start             end                 module name
    fffff801`14b40000 fffff801`14b86000   tabletaudiosample   (private pdb symbols)  C:\Debuggers\sym\TabletAudioSample.pdb\E992C4803EBE48C7B23DC1596495CE181\TabletAudioSample.pdb
        Loaded symbol image file: tabletaudiosample.sys
        Image path: \SystemRoot\system32\drivers\tabletaudiosample.sys
        Image name: tabletaudiosample.sys
        Browse all global symbols  functions  data
        Timestamp:        Thu Dec 10 12:20:26 2015 (5669DE8A)
        CheckSum:         0004891E
    ...  
    ```

    詳細については、「 [**lm**](lm--list-loaded-modules-.md)」を参照してください。

2.  デバッグ出力の [**すべてのグローバルシンボルを参照**] リンクをクリックすると、文字 a で始まる項目シンボルに関する情報が表示されます。
3.  DML が有効になっているため、出力の一部の要素はホットリンクで、クリックすることができます。 文字 a で始まる項目シンボルに関する情報を表示するには、デバッグ出力の [*データ*] リンクをクリックします。

    ```dbgcmd
    0: kd> x /D /f tabletaudiosample!a*
     A B C D E F G H I J K L M N O P Q R S T U V W X Y Z

    fffff806`9adb1000 tabletaudiosample!AddDevice (struct _DRIVER_OBJECT *, struct _DEVICE_OBJECT *)
    ```

    詳細については、「 [**x (シンボルを調べる)**](x--examine-symbols-.md)」を参照してください。

4.  **! Lmi**拡張機能には、モジュールに関する詳細情報が表示されます。 「 **! Lmi tabletaudiosample**」と入力します。 出力は次のようなテキストになります。

    ```dbgcmd
    0: kd> !lmi tabletaudiosample
    Loaded Module Info: [tabletaudiosample] 
             Module: tabletaudiosample
       Base Address: fffff8069ad90000
         Image Name: tabletaudiosample.sys
       Machine Type: 34404 (X64)
         Time Stamp: 58ebe848 Mon Apr 10 13:17:12 2017
               Size: 48000
           CheckSum: 42df7
    Characteristics: 22  
    Debug Data Dirs: Type  Size     VA  Pointer
                 CODEVIEW    a7,  e5f4,    d1f4 RSDS - GUID: {5395F0C5-AE50-4C56-AD31-DD5473BD318F}
                   Age: 1, Pdb: C:\Windows-driver-samples-master\audio\sysvad\TabletAudioSample\x64\Debug\TabletAudioSample.pdb
                       ??   250,  e69c,    d29c [Data not mapped]
         Image Type: MEMORY   - Image read successfully from loaded memory.
        Symbol Type: PDB      - Symbols loaded successfully from image header.
                     C:\Program Files (x86)\Windows Kits\10\Debuggers\x64\sym\TabletAudioSample.pdb\5395F0C5AE504C56AD31DD5473BD318F1\TabletAudioSample.pdb
           Compiler: Resource - front end [0.0 bld 0] - back end [14.0 bld 24210]
        Load Report: private symbols & lines, not source indexed 
                     C:\Program Files (x86)\Windows Kits\10\Debuggers\x64\sym\TabletAudioSample.pdb\5395F0C5AE504C56AD31DD5473BD318F1\TabletAudioSample.pdb
    ```

5.  次に示すように、 **! dh**拡張を使用してヘッダー情報を表示します。

    ```dbgcmd
    0: kd> !dh tabletaudiosample 

    File Type: EXECUTABLE IMAGE
    FILE HEADER VALUES
        8664 machine (X64)
           9 number of sections
    5669DE8A time date stamp Thu Dec 10 12:20:26 2015

           0 file pointer to symbol table
           0 number of symbols
          F0 size of optional header
          22 characteristics
                Executable
                App can handle >2gb addresses
    ...
    ```

## <a name="span-iddisplayingtheplugandplaydevicetreespansection-6-displaying-plug-and-play-device-tree-information"></a><span id="displayingtheplugandplaydevicetree"></span>セクション 6: プラグアンドプレイデバイスツリー情報の表示


*セクション6では、Sysvad サンプルデバイスドライバーに関する情報と、それがプラグアンドプレイデバイスツリーに存在する場所を表示します。*

プラグアンドプレイデバイスツリー内のデバイスドライバーに関する情報は、トラブルシューティングに役立ちます。 たとえば、デバイスドライバーがデバイスツリーに存在しない場合は、デバイスドライバーのインストールに問題がある可能性があります。

デバイスノードデバッグ拡張機能の詳細については、「 [**! devnode**](-devnode.md)」を参照してください。

**&lt;-ホストシステム上**

1. プラグアンドプレイデバイスツリー内のすべてのデバイスノードを表示するには、 **! devnode 0 1**コマンドを入力します。 このコマンドの実行には 1 ~ 2 分かかる場合があります。 その間、 \* WinDbg の状態領域に "Busy" と表示されます。

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
   ...
   ```

2. Ctrl + F キーを使用して、生成された出力を検索し、デバイスドライバーの名前*sysvad*を探します。

   ![検索対象の用語 sysvad を示すダイアログボックスが表示されます。](images/sysvad-lab-audio-find-dialog.png)

   という名前のデバイスノードエントリ `sysvad_TabletAudioSample` が、Syvad の! devnode 出力に表示されます。

   ```dbgcmd
     DevNode 0xffffe00086e68190 for PDO 0xffffe00089c575a0
       InstancePath is "ROOT\sysvad_TabletAudioSample\0000"
       ServiceName is "sysvad_tabletaudiosample"
       State = DeviceNodeStarted (0x308)
   ...
   ```

   PDO アドレスと DevNode アドレスが表示されていることに注意してください。

3. コマンドを使用し `!devnode 0 1 sysvad_TabletAudioSample` て、Sysvad デバイスドライバーに関連付けられているプラグアンドプレイ情報を表示します。

   ```dbgcmd 
   0: kd> !devnode 0 1 sysvad_TabletAudioSample
   Dumping IopRootDeviceNode (= 0xffffe00082df8d30)
   DevNode 0xffffe00086e68190 for PDO 0xffffe00089c575a0
     InstancePath is "ROOT\sysvad_TabletAudioSample\0000"
     ServiceName is "sysvad_tabletaudiosample"
     State = DeviceNodeStarted (0x308)
     Previous State = DeviceNodeEnumerateCompletion (0x30d)
     DevNode 0xffffe000897fb650 for PDO 0xffffe00089927e30
       InstancePath is "SWD\MMDEVAPI\{0.0.0.00000000}.{64097438-cdc0-4007-a19e-62e789062e20}"
       State = DeviceNodeStarted (0x308)
       Previous State = DeviceNodeStartPostWork (0x307)
     DevNode 0xffffe00086d2f5f0 for PDO 0xffffe00089939ae0
       InstancePath is "SWD\MMDEVAPI\{0.0.0.00000000}.{78880f4e-9571-44a4-a9df-960bde446487}"
       State = DeviceNodeStarted (0x308)
       Previous State = DeviceNodeStartPostWork (0x307)
     DevNode 0xffffe00089759bb0 for PDO 0xffffe000875aa060
       InstancePath is "SWD\MMDEVAPI\{0.0.0.00000000}.{7cad07f2-d0a0-4b9b-8100-8dc735e9c447}"
       State = DeviceNodeStarted (0x308)
       Previous State = DeviceNodeStartPostWork (0x307)
     DevNode 0xffffe00087735010 for PDO 0xffffe000872068c0
       InstancePath is "SWD\MMDEVAPI\{0.0.0.00000000}.{fc38551b-e69f-4b86-9661-ae6da78bc3c6}"
       State = DeviceNodeStarted (0x308)
       Previous State = DeviceNodeStartPostWork (0x307)
     DevNode 0xffffe00088457670 for PDO 0xffffe0008562b830
       InstancePath is "SWD\MMDEVAPI\{0.0.1.00000000}.{0894b831-c9fe-4c56-86a6-092380fc5628}"
       State = DeviceNodeStarted (0x308)
       Previous State = DeviceNodeStartPostWork (0x307)
     DevNode 0xffffe000893dbb70 for PDO 0xffffe00089d68060
       InstancePath is "SWD\MMDEVAPI\{0.0.1.00000000}.{15eb6b5c-aa54-47b8-959a-0cff2c1500db}"
       State = DeviceNodeStarted (0x308)
       Previous State = DeviceNodeStartPostWork (0x307)
     DevNode 0xffffe00088e6f250 for PDO 0xffffe00089f6e990
       InstancePath is "SWD\MMDEVAPI\{0.0.1.00000000}.{778c07f0-af9f-43f2-8b8d-490024f87239}"
       State = DeviceNodeStarted (0x308)
       Previous State = DeviceNodeStartPostWork (0x307)
     DevNode 0xffffe000862eb4b0 for PDO 0xffffe000884443a0
       InstancePath is "SWD\MMDEVAPI\{0.0.1.00000000}.{e4b72c7c-be50-45df-94f5-0f2922b85983}"
       State = DeviceNodeStarted (0x308)
       Previous State = DeviceNodeStartPostWork (0x307)
   ```

4. 前のコマンドに表示される出力には、ドライバーの実行中のインスタンスに関連付けられている PDO が含まれています。この例では、 *0xffffe00089c575a0*です。 Sysvad デバイスドライバーに関連付けられているプラグアンドプレイ情報を表示するには、 **! devobj**<em> &lt; &gt; PDO address</em>コマンドを入力します。 ここに示されているものではなく、PC に表示される PDO**アドレスを使用**します。

   ```dbgcmd 
   0: kd> !devobj 0xffffe00089c575a0
   Device object (ffffe00089c575a0) is for:
   0000004e \Driver\PnpManager DriverObject ffffe00082d47e60
   Current Irp 00000000 RefCount 65 Type 0000001d Flags 00001040
   SecurityDescriptor ffffc102b0f6d171 DevExt 00000000 DevObjExt ffffe00089c576f0 DevNode ffffe00086e68190 
   ExtensionFlags (0000000000)  
   Characteristics (0x00000180)  FILE_AUTOGENERATED_DEVICE_NAME, FILE_DEVICE_SECURE_OPEN
   AttachedDevice (Upper) ffffe00088386a50 \Driver\sysvad_tabletaudiosample
   Device queue is not busy.
   ```

5. **! Devobj**コマンドに表示される出力には、接続されているデバイスの名前、Driver sysvad tabletaudiosample が含まれてい \\ \\ \_ ます。 **! Drvobj**コマンドとビットマスク2を使用して、接続されているデバイスに関連付けられている情報を表示します。

   ```dbgcmd 
   0: kd> !drvobj \Driver\sysvad_tabletaudiosample 2
   Driver object (ffffe0008834f670) is for:
   \Driver\sysvad_tabletaudiosample
   DriverEntry:   fffff80114b45310  tabletaudiosample!FxDriverEntry
   DriverStartIo: 00000000 
   DriverUnload:  fffff80114b5fea0                tabletaudiosample!DriverUnload
   AddDevice:     fffff80114b5f000  tabletaudiosample!AddDevice

   Dispatch routines:
   [00] IRP_MJ_CREATE                      fffff80117b49a20             portcls!DispatchCreate
   [01] IRP_MJ_CREATE_NAMED_PIPE           fffff8015a949a00          nt!IopInvalidDeviceRequest
   [02] IRP_MJ_CLOSE                       fffff80115e26f90                ks!DispatchCleanup
   [03] IRP_MJ_READ                        fffff80115e32710                ks!DispatchRead
   [04] IRP_MJ_WRITE                       fffff80115e327e0              ks!DispatchWrite
   [05] IRP_MJ_QUERY_INFORMATION           fffff8015a949a00         nt!IopInvalidDeviceRequest
   [06] IRP_MJ_SET_INFORMATION             fffff8015a949a00              nt!IopInvalidDeviceRequest
   [07] IRP_MJ_QUERY_EA                    fffff8015a949a00         nt!IopInvalidDeviceRequest
   [08] IRP_MJ_SET_EA                      fffff8015a949a00              nt!IopInvalidDeviceRequest
   [09] IRP_MJ_FLUSH_BUFFERS               fffff80115e32640  ks!DispatchFlush
   [0a] IRP_MJ_QUERY_VOLUME_INFORMATION    fffff8015a949a00           nt!IopInvalidDeviceRequest
   [0b] IRP_MJ_SET_VOLUME_INFORMATION      fffff8015a949a00               nt!IopInvalidDeviceRequest
   [0c] IRP_MJ_DIRECTORY_CONTROL           fffff8015a949a00           nt!IopInvalidDeviceRequest
   [0d] IRP_MJ_FILE_SYSTEM_CONTROL         fffff8015a949a00         nt!IopInvalidDeviceRequest
   [0e] IRP_MJ_DEVICE_CONTROL              fffff80115e27480               ks!DispatchDeviceIoControl
   [0f] IRP_MJ_INTERNAL_DEVICE_CONTROL     fffff8015a949a00   nt!IopInvalidDeviceRequest
   [10] IRP_MJ_SHUTDOWN                    fffff8015a949a00      nt!IopInvalidDeviceRequest
   [11] IRP_MJ_LOCK_CONTROL                fffff8015a949a00  nt!IopInvalidDeviceRequest
   [12] IRP_MJ_CLEANUP                     fffff8015a949a00           nt!IopInvalidDeviceRequest
   [13] IRP_MJ_CREATE_MAILSLOT             fffff8015a949a00               nt!IopInvalidDeviceRequest
   [14] IRP_MJ_QUERY_SECURITY              fffff80115e326a0 ks!DispatchQuerySecurity
   [15] IRP_MJ_SET_SECURITY                fffff80115e32770      ks!DispatchSetSecurity
   [16] IRP_MJ_POWER                       fffff80117b3dce0            portcls!DispatchPower
   [17] IRP_MJ_SYSTEM_CONTROL              fffff80117b13d30              portcls!PcWmiSystemControl
   [18] IRP_MJ_DEVICE_CHANGE               fffff8015a949a00 nt!IopInvalidDeviceRequest
   [19] IRP_MJ_QUERY_QUOTA                 fffff8015a949a00  nt!IopInvalidDeviceRequest
   [1a] IRP_MJ_SET_QUOTA                   fffff8015a949a00       nt!IopInvalidDeviceRequest
   [1b] IRP_MJ_PNP                         fffff80114b5f7d0 tabletaudiosample!PnpHandler
   ```

6. **! Devstack**<em> &lt; &gt; PDO address</em>コマンドを入力して、デバイスドライバーに関連付けられているプラグアンドプレイ情報を表示します。 **! Devnode 0 1**コマンドに表示される出力には、ドライバーの実行中のインスタンスに関連付けられている PDO アドレスが含まれています。 この例では、 *0xffffe00089c575a0*です。 次に示すように、コンピューターに表示され**ている PDO アドレスを使用**します。これは、以下に示すものではありません。

   ```dbgcmd
   0: kd> !devstack 0xffffe00089c575a0
     !DevObj           !DrvObj            !DevExt           ObjectName
     ffffe00088d212e0  \Driver\ksthunk    ffffe00088d21430  0000007b
     ffffe00088386a50  \Driver\sysvad_tabletaudiosampleffffe00088386ba0  0000007a
   > ffffe00089c575a0  \Driver\PnpManager 00000000  0000004e
   !DevNode ffffe00086e68190 :
     DeviceInst is "ROOT\sysvad_TabletAudioSample\0000"
     ServiceName is "sysvad_tabletaudiosample"
   ```

出力には、farily 単純なデバイスドライバースタックがあることが示されています。 Sysvad \_ TabletAudioSample ドライバーは、PnPManager ノードの子です。 PnPManager はルートノードです。

この図は、より複雑なデバイスノードツリーを示しています。

![約20個のノードを含むデバイスノードツリー](images/debuglab-image-device-node-tree.png)

**メモ**   より複雑なドライバースタックの詳細については、「[ドライバースタック](https://docs.microsoft.com/windows-hardware/drivers/gettingstarted/driver-stacks)と[デバイスノードおよびデバイススタック](https://docs.microsoft.com/windows-hardware/drivers/gettingstarted/device-nodes-and-device-stacks)」を参照してください。

 

## <a name="span-idworkingwithbreakpointsspansection-7-working-with-breakpoints"></a><span id="workingwithbreakpoints"></span>セクション 7: ブレークポイントの操作


*セクション7では、ブレークポイントを使用して特定の時点でコードの実行を停止します。*

**コマンドを使用したブレークポイントの設定**

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

 

1.  Windbg UI を使用して、 **Debug** &gt; 現在の windbg セッションでデバッグ**ソースモード**が有効になっていることを確認します。

2.  次のコマンドを入力して、ソースパスにローカルコードの場所を追加します。

    ```dbgcmd
    .sympath+ C:\WDK_Samples\Sysvad
    ```

3.  次のコマンドを入力して、シンボルパスにローカルシンボルの場所を追加します。

    ```dbgcmd
    .sympath+ C:\WDK_Samples\Sysvad
    ```

4.  **デバッグマスクの設定**

    ドライバーを操作するときは、表示される可能性があるすべてのメッセージを表示すると便利な場合があります。 次のように入力して、既定のデバッグビットマスクを変更します。これにより、ターゲットシステムからのすべてのデバッグメッセージがデバッガーに表示されます。

    ```dbgcmd
    0: kd> ed nt!Kd_DEFAULT_MASK 0xFFFFFFFF
    ```

5.  ドライバーの名前を使用し**て、ブレーク**ポイントを設定します。次に、ブレークポイントを設定する関数名 (AddDevice) を感嘆符で区切って指定します。

    ```dbgcmd
    0: kd> bm tabletaudiosample!AddDevice
    breakpoint 1 redefined
      1: fffff801`14b5f000 @!"tabletaudiosample!AddDevice"
    ```

    モジュールのような変数の設定と組み合わせて、さまざまな構文を使用できます &lt; &gt; 。 &lt;symbol &gt; 、 &lt; class &gt; :: &lt; method &gt; 、' &lt; .cpp &gt; : &lt; line number &gt; '、または回数をスキップ &lt; &gt; &lt; \# &gt; します。 詳細については、「[ブレークポイントの使用](using-breakpoints.md)」を参照してください。

6.  現在のブレークポイントを一覧表示して、そのブレークポイントが設定されたことを確認するには、「 **bl** 」コマンドを入力します。

    ```dbgcmd
    0: kd> bl
    1 e fffff801`14b5f000     0001 (0001) tabletaudiosample!AddDevice
    ```

7.  移動コマンド**g**を入力して、ターゲットシステムでコードの実行を再開します。

8.  **-&gt;ターゲットシステム上**

    Windows で、アイコンを使用するか、 **mmc devmgmt.msc**を入力して、デバイスマネージャーを開きます。 **デバイスマネージャー** [**サウンド、ビデオ、およびゲームコントローラー]** ノードを展開します。 仮想オーディオドライバーのエントリを右クリックし、メニューから [**無効**] を選択します。

9.  仮想オーディオドライバーのエントリをもう一度右クリックし、メニューから [**有効化**] を選択します。
10. **&lt;-ホストシステム上**

    これにより、AddDevice を呼び出すドライバーが Windows によって再読み込みされます。 これにより、AddDevice デバッグブレークポイントが起動され、ターゲットシステムでのドライバーコードの実行が停止します。

    ```dbgcmd
    Breakpoint 1 hit
    tabletaudiosample!AddDevice:
    fffff801`14baf000 4889542410      mov     qword ptr [rsp+10h],rdx
    ```

    ソースパスが適切に設定されている場合は、AddDevice のルーチンで停止する必要があります。

    ```dbgcmd
    {
        PAGED_CODE();

        NTSTATUS        ntStatus;
        ULONG           maxObjects;

        DPF(D_TERSE, ("[AddDevice]"));

        maxObjects = g_MaxMiniports;
        
        #ifdef SYSVAD_BTH_BYPASS
        // 
        // Allow three (3) Bluetooth hands-free profile devices.
        //
        maxObjects += g_MaxBthHfpMiniports * 3; 
        #endif // SYSVAD_BTH_BYPASS

        // Tell the class driver to add the device.
        //
        ntStatus = 
            PcAddAdapterDevice
            ( 
                DriverObject,
                PhysicalDeviceObject,
                PCPFNSTARTDEVICE(StartDevice),
                maxObjects,
                0
            );
        return ntStatus;
    } // AddDevice
    ```

11. **P**コマンドを入力するか、F10 キーを押して、コードを1行ずつステップ実行します。 Sysvad AddDevice コードを PpvUtilCall、PnpCallAddDevice、PipCallDriverAddDevice Windows コードにステップアウトすることができます。 **P コマンドに**数値を指定して、 *p 5*などの複数行を順方向に進めることができます。

12. コードのステップ実行が完了したら、移動コマンド**g**を使用して、ターゲットシステムで実行を再開します。

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
<td align="left"><p>。</p></td>
<td align="left"><p>書き込み (CPU がそのアドレスに書き込む場合)</p></td>
</tr>
</tbody>
</table>

 

常に4つのデータブレークポイントを設定できます。また、データを正しく調整していることを確認するか、ブレークポイントをトリガーしないことを確認してください (単語は2に割り切れ、dword は4で割り切れる必要があり、quadwords は0または8になります)。

たとえば、特定のメモリアドレスに読み取り/書き込みブレークポイントを設定するには、次のようなコマンドを使用します。

```dbgcmd
ba r 4 fffff800`7bc9eff0
```

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

 

または、[ **edit** &gt; **ブレークポイント**の編集] をクリックして、ブレークポイントを変更することもできます。 [ブレークポイント] ダイアログボックスは、既存のブレークポイントでのみ機能することに注意してください。 新しいブレークポイントは、コマンドラインから設定する必要があります。

**MixerVolume にブレークポイントを設定する**

デバイスドライバーが読み込まれた後、さまざまなイベントに応答するために、オーディオドライバーコードのさまざまな部分が呼び出されます。 次のセクションでは、ユーザーが仮想オーディオドライバーのボリュームコントロールを調整したときに起動するブレークポイントを設定します。

MixerVolume にブレークポイントを設定するには、次の手順を実行します。

1.  **&lt;-ホストシステム上**

    ボリュームを変更するメソッドを見つけるには、x コマンドを使用して、文字列ボリュームを含む CAdapterCommon 内のシンボルを一覧表示します。

    ```dbgcmd
    kd> x tabletaudiosample!CAdapterCommon::*
    ...
    fffff800`7bce26a0 tabletaudiosample!CAdapterCommon::MixerVolumeWrite (unsigned long, unsigned long, long)
    …
    ```

    CTRL + F キーを使用して、ボリュームの出力を上方向に検索し、MixerVolumeWrite メソッドを見つけます。

2.  Bc を使用して、前のブレークポイントをクリアし \* ます。
3.  次のコマンドを使用して、CAdapterCommon:: MixerVolumeWrite ルーチンにシンボルのブレークポイントを設定します。

    ```dbgcmd
    kd> bm tabletaudiosample!CAdapterCommon::MixerVolumeWrite
      1: fffff801`177b26a0 @!"tabletaudiosample!CAdapterCommon::MixerVolumeWrite"
    ```

4.  ブレークポイントを一覧表示して、ブレークポイントが適切に設定されていることを確認します。

    ```dbgcmd
    kd> bl
    1 e fffff801`177b26a0 [c:\WDK_Samples\audio\sysvad\common.cpp @ 1668]    0001 (0001) tabletaudiosample!CAdapterCommon::MixerVolumeWrite
    ```

5.  移動コマンド**g**を入力して、ターゲットシステムでコードの実行を再開します。

6.  [コントロールパネル] で **、[ハードウェアとサウンド**] を選択し &gt; **Sound**ます。 [**シンクの説明のサンプル**] を右クリックし、[**プロパティ**] を選択します。 [**レベル**] タブを選択します。スライダーの音量を調整します。

7.  これにより、SetMixerVolume デバッグブレークポイントが起動され、ターゲットシステムでのドライバーコードの実行が停止します。

    ```dbgcmd
    kd> g
    Breakpoint 1 hit
    tabletaudiosample!CAdapterCommon::MixerVolumeWrite:
    fffff801`177b26a0 44894c2420      mov     dword ptr [rsp+20h],r9d
    ```

    この行では、共通の .cpp の

    ```dbgcmd
    {
        if (m_pHW)
        {
            m_pHW->SetMixerVolume(Index, Channel, Value);
        }
    } // MixerVolumeWrite
    ```

8.  現在の変数とその値を表示するには、dv コマンドを使用します。 変数の詳細については、このラボの次のセクションで説明します。

    ```dbgcmd
    2: kd> dv
               this = 0x00000000`00000010
             ulNode = 0x344
          ulChannel = 0x210a45f8
            lVolume = 0n24
    ```

9.  **F10**キーを押してコードを1ステップずつ実行します。

10. **F5**キーを押して、MixerVolumeWrite コードの実行を完了します。

**概要-デバッガーからコードをステップ実行コマンドウィンドウ**

コードをステップ実行するために使用できるコマンドを次に示します (関連するキーボードショートカットをかっこ内に示します)。

-   ブレークイン (Ctrl + Break)-このコマンドは、システムが実行されていて、WinDbg と通信している限り、システムを中断します (カーネルデバッガーのシーケンスは Ctrl + C です)。

-   ステップオーバー (F10) –このコマンドは、一度に1つのステートメントまたは1つの命令を実行します。 呼び出しが検出されると、呼び出されたルーチンを入力せずに、その呼び出しに対してコードの実行が渡されます。 (プログラミング言語が C または C++ で、WinDbg がソースモードの場合、**デバッグ** &gt; を使用してソースモードを有効または無効にすることができます。**ソースモード**)。

-   ステップイン (F11) –このコマンドは、呼び出しの実行が呼び出されたルーチンに送られる点を除いて、ステップオーバーに似ています。

-   ステップアウト (Shift + F11) –このコマンドは、現在のルーチン (呼び出し履歴の現在の場所) を実行し、現在のルーチンから終了します。 これは、ルーチンを十分に経験している場合に便利です。

-   カーソル行の前まで実行 (F7 または Ctrl + F10) –実行を中断するソースウィンドウまたは逆アセンブルウィンドウにカーソルを置き、F7 キーを押します。コードの実行は、その時点まで実行されます。 コード実行のフローがカーソルによって示されたポイントに届かない場合 (たとえば、IF ステートメントが実行されない場合)、コードの実行が示されたポイントに届かなかったため、WinDbg は中断されません。

-   Run (F5) –ブレークポイントが検出されるか、バグチェックなどのイベントが発生するまで実行されます。

**詳細オプション**

-   命令を現在の行に設定する (Ctrl + Shift + I) –ソースウィンドウでは、行にカーソルを置き、このキーボードショートカットを入力します。コードの実行は、続行するとすぐに開始されます (F5 キーまたは F10 キーを使用するなど)。 これは、シーケンスを再試行する場合に便利ですが、注意が必要です。 たとえば、レジスタと変数は、コードの実行によって自然に到達した場合のようには設定されません。

-   Eip レジスタの直接設定--eip レジスタに値を指定すると、F5 キー (または F10 キー、F11 キーなど) を押すとすぐに、そのアドレスから実行が開始されます。 これは、カーソルが指定された現在の行に対する設定命令に似ていますが、アセンブリ命令のアドレスを指定する点が異なります。

コマンドラインからではなく、UI をステップ実行する方が簡単なので、この方法をお勧めします。 必要に応じて、コマンドラインで次のコマンドを使用してソースファイルをステップ実行できます。

-   . lines-ソース行情報を有効にします。

-   bp main-モジュールの先頭に最初のブレークポイントを設定します。

-   l + t ステップはソース行によって実行されます。

-   [**デバッグ** &gt; **ソースモード**] を選択してソースモードにします。 `L+t` コマンドでは不十分です。

-   l + s-ソース行がプロンプトに表示されます。

-   g-"main" が入力されるまでプログラムを実行します。

-   p-1 つのソース行を実行します。

詳細については、デバッグリファレンスドキュメントの「 [WinDbg でのソースコードのデバッグ](source-window.md)」を参照してください。

**コードにブレークポイントを設定する**

コードにブレークポイントを設定するには、 `DebugBreak()` ステートメントを追加し、プロジェクトをリビルドして、ドライバーを再インストールします。 このブレークポイントは、ドライバーが有効になるたびに起動されるため、実稼働コードではなく、初期の開発段階で使用する手法になります。 この手法は、ブレークポイントコマンドを使用してブレークポイントを動的に設定するほど柔軟ではありません。

ヒント: さらにラボ作業を行うためにブレークポイントを追加して、Sysvad ドライバーのコピーを保持することができます。

1.  ステートメントをサンプルコードに追加して、AddDevice メソッドが実行されるたびに中断が発生するように設定し `DebugBreak()` ます。

    ```dbgcmd
    ...
        // Insert the DebugBreak() statment before the  PcAddAdapterDevice is called.
        //

        DebugBreak()
        
        // Tell the class driver to add the device.
        //
        ntStatus = 
            PcAddAdapterDevice
            ( 
                DriverObject,
                PhysicalDeviceObject,
                PCPFNSTARTDEVICE(StartDevice),
                maxObjects,
                0
            );

        return ntStatus;
    } // AddDevice
    ```

2.  前述のすべての手順に従って Microsoft Visual Studio でドライバーをリビルドし、ターゲットコンピューターに再インストールします。 更新されたドライバーをインストールする前に、既存のドライバーをアンインストールしてください。
3.  前のブレークポイントをクリアし、デバッガーがターゲット PC にアタッチされていることを確認します。

4.  コードが実行され、ステートメントに到達すると `DebugBreak` 、実行が停止し、メッセージが表示されます。

    ```dbgcmd
    KERNELBASE!DebugBreak:
    77b3b770 defe     __debugbreak
    ```

## <a name="span-idlookingatvariablesspanspan-idlookingatvariablesspanspan-idlookingatvariablesspansection-8-display-variables"></a><span id="LookingAtVariables"></span><span id="lookingatvariables"></span><span id="LOOKINGATVARIABLES"></span>セクション 8: 変数を表示する


*セクション8では、デバッガーコマンドを使用して変数を表示します。*

コードが実行されるときに変数を調べて、コードが想定どおりに動作していることを確認すると便利です。 このラボでは、オーディオドライバーがサウンドを生成するときに変数を調べます。

1.  **Dv**コマンドを使用して、tabletaudiosample! に関連付けられているロケール変数を調べます。CMiniportWaveRT:: New \* 。

    ```dbgcmd
    kd> dv tabletaudiosample!CMiniportWaveRT::New*
    ```

2.  前のブレークポイントをクリアする

    ```dbgcmd
    bc *
    ```

3.  次のコマンドを使用して、CMiniportWaveCyclicStreamMSVAD ルーチンにシンボルのブレークポイントを設定します。

    ```dbgcmd
    0: kd> bm tabletaudiosample!CMiniportWaveRT::NewStream
      1: fffff801`177dffc0 @!"tabletaudiosample!CMiniportWaveRT::NewStream"
    ```

4.  移動コマンド**g**を入力して、ターゲットシステムでコードの実行を再開します。

5.  **-&gt;ターゲットシステム上**

    小さいメディアファイル (.wav ファイル拡張子の付いた Windows 通知サウンドファイルなど) を探し、ファイルをクリックして再生します。 たとえば、Windows Media ディレクトリにある Ring05 を使用できます。 \\

6.  **&lt;-ホストシステム上**

    メディアファイルが再生されると、ブレークポイントが起動し、ターゲットシステムでのドライバーコードの実行が停止します。

    ```dbgcmd
    Breakpoint 1 hit
    tabletaudiosample!CMiniportWaveRT::NewStream:
    fffff801`177dffc0 44894c2420      mov     dword ptr [rsp+20h],r9d
    ```

    ソースコードウィンドウで、NewStream 関数への入り口の中かっこを強調表示する必要があります。

    ```dbgcmd
    /*++

    Routine Description:

      The NewStream function creates a new instance of a logical stream 
      associated with a specified physical channel. Callers of NewStream should 
      run at IRQL PASSIVE_LEVEL.

    Arguments:

      OutStream -

      OuterUnknown -

      Pin - 

      Capture - 

      DataFormat -

    Return Value:

      NT status code.

    --*/
    {

    ...
    ```

7.  **ローカル変数**

    **Dv**コマンドを入力すると、指定したフレームのすべてのローカル変数の名前と値を表示できます。

    ```dbgcmd
    0: kd> dv
                    this = 0xffffe000`4436f8e0
               OutStream = 0xffffe000`49d2f130
            OuterUnknown = 0xffffe000`4436fa30
                     Pin = 0
                 Capture = 0x01 '
              DataFormat = 0xffffe000`44227790
    signalProcessingMode = {487E9220-E000-FFFF-30F1-D24900E0FFFF}
                ntStatus = 0n1055
                  stream = 0x00000000`00000200
    ```

8.  **DML を使用して変数を表示する**

    DML を使用して変数を調べるには、下線付きの要素をクリックします。 Click アクションは、入れ子になったデータ構造をドリルダウンできるようにする[**dx (Display NatVis Expression)**](dx--display-visualizer-variables-.md)コマンドを構築します。

    ```dbgcmd
    0: kd> dx -r1 (*((tabletaudiosample!CMiniportWaveRT *)0xffffe001d10b8380))
    (*((tabletaudiosample!CMiniportWaveRT *)0xffffe001d10b8380)) :  [Type: CMiniportWaveRT]
        [+0x020] m_lRefCount      : 0
        [+0x028] m_pUnknownOuter  : 0xffffe001d1477e50 : [Type: IUnknown *]
        [+0x030] m_ulLoopbackAllocated : 0x2050
        [+0x034] m_ulSystemAllocated : 0x180
        [+0x038] m_ulOffloadAllocated : 0x0
        [+0x03c] m_dwCaptureAllocatedModes : 0x0

    0: kd> dx -r1 (*((tabletaudiosample!_GUID *)0xffffd001c8acd348))
    (*((tabletaudiosample!_GUID *)0xffffd001c8acd348)) : {487E9220-E000-FFFF-30F1-D24900E0FFFF} [Type: _GUID]
        [<Raw View>]    

    0: kd> dx -r1 -n (*((tabletaudiosample!_GUID *)0xffffd001c8acd348))
    (*((tabletaudiosample!_GUID *)0xffffd001c8acd348)) :  [Type: _GUID]
        [+0x000] Data1            : 0x487e9220
        [+0x004] Data2            : 0xe000
        [+0x006] Data3            : 0xffff
        [+0x008] Data4            :  [Type: unsigned char [8]]

    0: kd> dx -r1 -n (*((tabletaudiosample!unsigned char (*)[8])0xffffd001c8acd350))
    (*((tabletaudiosample!unsigned char (*)[8])0xffffd001c8acd350)) :  [Type: unsigned char [8]]
        [0]              : 0x30
        [1]              : 0xf1
        [2]              : 0xd2
        [3]              : 0x49
        [4]              : 0x0
        [5]              : 0xe0
        [6]              : 0xff
        [7]              : 0xff
    ```

9.  **グローバル変数**

    グローバル変数のメモリ位置を確認するには、「?」と入力し**ます。 &lt;変数名 &gt; **。

    ```dbgcmd
    0: kd> ? signalProcessingMode
    Evaluate expression: -52768896396472 = ffffd001`c8acd348
    ```

10. これにより、変数のメモリ位置 (この場合は*ffffd001 \` c8acd348*) が返されます。 メモリ位置の内容を表示するには、前のコマンドで返されたメモリ位置を使用して**dd**コマンドを入力し、その場所の値をダンプします。

    ```dbgcmd
    0: kd> dd ffffd001`c8acd348
    ffffd001`c8acd348  487e9220 ffffe000 49d2f130 ffffe000
    ffffd001`c8acd358  4837c468 ffffe000 18221570 ffffc000
    ffffd001`c8acd368  4436f8e0 ffffe000 487e9220 ffffe000
    ffffd001`c8acd378  18ab145b fffff801 4837c420 ffffe000
    ffffd001`c8acd388  4436f8e0 ffffe000 49d2f130 ffffe000
    ffffd001`c8acd398  4436fa30 ffffe000 00000000 00000000
    ffffd001`c8acd3a8  00000001 00000000 44227790 ffffe000
    ffffd001`c8acd3b8  18adc7f9 fffff801 495972a0 ffffe000
    ```

11. **Dd**コマンドで変数名を使用することもできます。

    ```dbgcmd
    0: kd> dd signalProcessingMode
    ffffd001`c8acd348  487e9220 ffffe000 49d2f130 ffffe000
    ffffd001`c8acd358  4837c468 ffffe000 18221570 ffffc000
    ffffd001`c8acd368  4436f8e0 ffffe000 487e9220 ffffe000
    ffffd001`c8acd378  18ab145b fffff801 4837c420 ffffe000
    ffffd001`c8acd388  4436f8e0 ffffe000 49d2f130 ffffe000
    ffffd001`c8acd398  4436fa30 ffffe000 00000000 00000000
    ffffd001`c8acd3a8  00000001 00000000 44227790 ffffe000
    ffffd001`c8acd3b8  18adc7f9 fffff801 495972a0 ffffe000
    ```

12. **変数の表示**

    **View** &gt; ローカル変数を表示するには **、[ローカル**の表示] メニュー項目を使用します。 また、このインターフェイスでは、より複雑なデータ構造をドリルダウンすることもできます。

    ![サンプルコードのローカルとコマンドウィンドウを示す windbg](images/sysvad-lab-display-variables.png)

13. F または F10 キーを使用して、ntStatus = IsFormatSupported (Pin、Capture、DataFormat) を強調表示するまで、コード内の約10行を順方向に移動します。コード行。

    ```cpp
        PAGED_CODE();

        ASSERT(OutStream);
        ASSERT(DataFormat);

        DPF_ENTER(("[CMiniportWaveRT::NewStream]"));

        NTSTATUS                    ntStatus = STATUS_SUCCESS;
        PCMiniportWaveRTStream      stream = NULL;
        GUID                        signalProcessingMode = AUDIO_SIGNALPROCESSINGMODE_DEFAULT;
        
        *OutStream = NULL;

         //
        // If the data format attributes were specified, extract them.
        //
        if ( DataFormat->Flags & KSDATAFORMAT_ATTRIBUTES )
        {
            // The attributes are aligned (QWORD alignment) after the data format
            PKSMULTIPLE_ITEM attributes = (PKSMULTIPLE_ITEM) (((PBYTE)DataFormat) + ((DataFormat->FormatSize + FILE_QUAD_ALIGNMENT) & ~FILE_QUAD_ALIGNMENT));
            ntStatus = GetAttributesFromAttributeList(attributes, attributes->Size, &signalProcessingMode);
        }

        // Check if we have enough streams.
        //
        if (NT_SUCCESS(ntStatus))
        {
            ntStatus = ValidateStreamCreate(Pin, Capture, signalProcessingMode);
        }

        // Determine if the format is valid.
        //
        if (NT_SUCCESS(ntStatus))
        {
            ntStatus = IsFormatSupported(Pin, Capture, DataFormat);
        }

    ...
    ```

14. **Dv**コマンドを使用して、指定したフレームのすべてのローカル変数の名前と値を表示します。 予想どおり、値は、このコマンドを最後に実行したときとは異なることに注意してください。これは、ローカル変数を変更するコードが実行され、一部の変数が現在のフレームに含まれていないか、その値が変更されたためです。

    ```dbgcmd
    2: kd> dv
                    this = 0xffffe001`d1182000
               OutStream = 0xffffe001`d4776d20
            OuterUnknown = 0xffffe001`d4776bc8
                     Pin = 0
                 Capture = 0x00 '
              DataFormat = 0xffffe001`cd7609b0
    signalProcessingMode = {4780004E-7133-41D8-8C74-660DADD2C0EE}
                ntStatus = 0n0
                  stream = 0x00000000`00000000
    ```

## <a name="span-idviewingcallstacksspansection-9-view-call-stacks"></a><span id="viewingcallstacks"></span>セクション 9: 呼び出し履歴を表示する


*セクション9では、呼び出し履歴を表示して、呼び出し元/calle コードを確認します。*

呼び出し履歴は、プログラムカウンターの現在の場所に led がある関数呼び出しのチェーンです。 呼び出し履歴の一番上の関数は現在の関数であり、次の関数は、現在の関数を呼び出した関数です。

呼び出し履歴を表示するには、k コマンドを使用し \* ます。

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

 

呼び出し履歴を使用可能な状態にしたままにする場合は、[呼び出し履歴の**表示**] をクリックし &gt; **Call stack**て表示します。 ウィンドウの上部にある列をクリックして、追加情報の表示を切り替えます。

![windbg 呼び出し履歴ウィンドウ](images/sysvad-lab-call-stack.png)

この出力は、ブレーク状態でサンプルアダプターコードをデバッグしているときの呼び出し履歴を示しています。

```dbgcmd
0: kd> kb
# RetAddr           : Args to Child                                                           : Call Site
00 fffff800`7a0fa607 : ffffe001`d1182000 ffffe001`d4776d20 ffffe001`d4776bc8 ffffe001`00000000 : tabletaudiosample!CMiniportWaveRT::NewStream+0x1dc [c:\data1\threshold\audio\endpointscommon\minwavert.cpp @ 597]
01 fffff800`7a0fb2c3 : 00000000`00000000 ffffe001`d122bb10 ffffe001`ceb81750 ffffe001`d173f058 : portcls!CPortPinWaveRT::Init+0x2e7
02 fffff800`7a0fc7f9 : ffffe001`d4776bc0 00000000`00000000 ffffe001`d10b8380 ffffe001`d122bb10 : portcls!CPortFilterWaveRT::NewIrpTarget+0x193
03 fffff800`7a180552 : 00000000`00000000 ffffe001`d10b8380 ffffe001`d122bb10 ffffe001`d4565600 : portcls!xDispatchCreate+0xd9
04 fffff800`7a109a9a : ffffe001`d10b84d0 ffffe001`d10b8380 00000000`00000000 ffffe001`00000000 : ks!KsDispatchIrp+0x272
05 fffff800`7bd314b1 : ffffe001`d122bb10 ffffd001`c3098590 ffffe001`d122bd90 ffffe001`ce80da70 : portcls!DispatchCreate+0x7a
06 fffff803`cda1bfa8 : 00000000`00000024 00000000`00000000 00000000`00000000 ffffe001`d122bb10 : ksthunk!CKernelFilterDevice::DispatchIrp+0xf9
07 fffff803`cda7b306 : 00000000`000001f0 ffffe001`d48ce690 ffffe001`d13d6400 ffffe001`d13d64c0 : nt!IopParseDevice+0x7c8
08 fffff803`cda12916 : 00000000`000001f0 ffffd001`c30988d0 ffffe001`d13d6490 fffff803`cda7b250 : nt!IopParseFile+0xb6
09 fffff803`cda1131c : ffffe001`d2ccb001 ffffd001`c30989e0 00ffffe0`00000040 ffffe001`cd127dc0 : nt!ObpLookupObjectName+0x776
0a fffff803`cd9fedb8 : ffffe001`00000001 ffffe001`d48ce690 00000000`00000000 00000000`00000000 : nt!ObOpenObjectByNameEx+0x1ec
0b fffff803`cd9fe919 : 000000ee`6d1fc8d8 000000ee`6d1fc788 000000ee`6d1fc7e0 000000ee`6d1fc7d0 : nt!IopCreateFile+0x3d8
0c fffff803`cd752fa3 : ffffc000`1f296870 fffff803`cd9d9fbd ffffd001`c3098be8 00000000`00000000 : nt!NtCreateFile+0x79
0d 00007fff`69805b74 : 00007fff`487484e6 0000029b`00000003 00000000`0000012e 00000000`00000000 : nt!KiSystemServiceCopyEnd+0x13
0e 00007fff`487484e6 : 0000029b`00000003 00000000`0000012e 00000000`00000000 00000000`00000000 : 0x00007fff`69805b74
0f 0000029b`00000003 : 00000000`0000012e 00000000`00000000 00000000`00000000 00000000`00000000 : 0x00007fff`487484e6
10 00000000`0000012e : 00000000`00000000 00000000`00000000 00000000`00000000 00000000`00000080 : 0x0000029b`00000003
11 00000000`00000000 : 00000000`00000000 00000000`00000000 00000000`00000080 00000000`00000000 : 0x12e
```

DML を使用して、コードを詳しく調べることができます。 最初の00エントリをクリックすると、[[**ローカルコンテキストの設定**](-frame--set-local-context-.md)] コマンドを使用してコンテキストが設定され、[ [**Dv (ローカル変数の表示)**](dv--display-local-variables-.md) ] コマンドによってローカル変数が表示されます。

```dbgcmd
0: kd> .frame 0n0;dv /t /v
00 ffffd001`c30981d0 fffff800`7a0fa607 tabletaudiosample!CMiniportWaveRT::NewStream+0x1dc [c:\data1\threshold\audio\endpointscommon\minwavert.cpp @ 597]
ffffd001`c30982b0 class CMiniportWaveRT * this = 0xffffe001`d1182000
ffffd001`c30982b8 struct IMiniportWaveRTStream ** OutStream = 0xffffe001`d4776d20
ffffd001`c30982c0 struct IPortWaveRTStream * OuterUnknown = 0xffffe001`d4776bc8
ffffd001`c30982c8 unsigned long Pin = 0
ffffd001`c30982d0 unsigned char Capture = 0x00 '
ffffd001`c30982d8 union KSDATAFORMAT * DataFormat = 0xffffe001`cd7609b0
ffffd001`c3098270 struct _GUID signalProcessingMode = {4780004E-7133-41D8-8C74-660DADD2C0EE}
ffffd001`c3098210 long ntStatus = 0n0
ffffd001`c3098218 class CMiniportWaveRTStream * stream = 0x00000000`00000000
```

## <a name="span-iddisplayingprocessesandthreadsspansection-10-display-processes-and-threads"></a><span id="displayingprocessesandthreads"></span>セクション 10: プロセスとスレッドを表示する


*セクション10では、デバッガーコマンドを使用して、プロセスとスレッドを表示します。*

**処理**

現在のプロセスコンテキストを変更するには、プロセスのプロセスコマンドを使用します。 &lt; &gt; 次の例では、プロセスを識別し、それにコンテキストを切り替える方法を示します。

-   コマンドを使用して、 `!process` サウンドの再生に関係している現在のプロセスを表示します。

    詳細については、「! process」を参照してください[ **。**](-process.md)

出力には、プロセスが audiodg.exe に関連付けられていることが示されています。 このトピックの前のセクションで説明したブレークポイントにまだある場合は、現在のプロセスを audiodg.exe のイメージに関連付ける必要があります。

**&lt;-ホストシステム上**

```dbgcmd
0: kd> !process
PROCESS ffffe001d147c840
    SessionId: 0  Cid: 10f0    Peb: ee6cf8a000  ParentCid: 0434
    DirBase: d2122000  ObjectTable: ffffc0001f191ac0  HandleCount: <Data Not Accessible>
    Image: audiodg.exe
    VadRoot ffffe001d4222f70 Vads 70 Clone 0 Private 504. Modified 16. Locked 0.
    DeviceMap ffffc00019113080
    Token                             ffffc0001f1d4060
    ElapsedTime                       <Invalid>
    UserTime                          00:00:00.000
    KernelTime                        00:00:00.000
    QuotaPoolUsage[PagedPool]         81632
    QuotaPoolUsage[NonPagedPool]      9704
    Working Set Sizes (now,min,max)  (2154, 1814, 2109) (8616KB, 7256KB, 8436KB)
    PeakWorkingSetSize                2101
    VirtualSize                       2097192 Mb
    PeakVirtualSize                   2097192 Mb
    PageFaultCount                    2336
    MemoryPriority                    BACKGROUND
    BasePriority                      8
    CommitCharge                      1573

        THREAD ffffe001d173e840  Cid 10f0.1dac  Teb: 000000ee6cf8b000 Win32Thread: ffffe001d1118cf0 WAIT: (UserRequest) UserMode Non-Alertable
            ffffe001d16c4dd0  NotificationEvent
            ffffe001d08b0840  ProcessObject

        THREAD ffffe001ceb77080  Cid 10f0.16dc  Teb: 000000ee6cf8d000 Win32Thread: 0000000000000000 WAIT: (WrQueue) UserMode Alertable
            ffffe001cf2d1840  QueueObject

        THREAD ffffe001d112c840  Cid 10f0.0a4c  Teb: 000000ee6cf8f000 Win32Thread: 0000000000000000 WAIT: (WrQueue) UserMode Alertable
            ffffe001cf2d1840  QueueObject

        THREAD ffffe001d16c7840  Cid 10f0.13c4  Teb: 000000ee6cf91000 Win32Thread: 0000000000000000 WAIT: (WrQueue) UserMode Alertable
            ffffe001cf2d1840  QueueObject

        THREAD ffffe001cec67840  Cid 10f0.0dbc  Teb: 000000ee6cf93000 Win32Thread: 0000000000000000 WAIT: (WrQueue) UserMode Alertable
            ffffe001d173e5c0  QueueObject

        THREAD ffffe001d1117840  Cid 10f0.1d6c  Teb: 000000ee6cf95000 Win32Thread: 0000000000000000 WAIT: (WrQueue) UserMode Alertable
            ffffe001d173e5c0  QueueObject

        THREAD ffffe001cdeae840  Cid 10f0.0298  Teb: 000000ee6cf97000 Win32Thread: 0000000000000000 RUNNING on processor 2
```

このプロセスに関連付けられているスレッドの1つが実行中状態であることに注意してください。 このスレッドは、ブレークポイントにヒットしたときのメディアクリップの再生をサポートしていました。

すべてのプロセスの概要情報を表示するには、 **! process 0 0**コマンドを使用します。 コマンドの出力で、CTRL + F キーを使用して、audiodg.exe イメージに関連付けられているプロセスのプロセス ID を検索します。 次に示す例では、プロセス ID は*ffffe001d147c840*です。

このラボで後ほど使用するために、PC の audiodg.exe に関連付けられているプロセス ID を記録します。 \_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_

```dbgcmd
...

PROCESS ffffe001d147c840
    SessionId: 0  Cid: 10f0    Peb: ee6cf8a000  ParentCid: 0434
    DirBase: d2122000  ObjectTable: ffffc0001f191ac0  HandleCount: <Data Not Accessible>
    Image: audiodg.exe
...
```

デバッガーに g を入力して、メディアクリップの再生が完了するまでコードを実行します。 次に、Ctrl + ScrLk (Ctrl + Break) キーを押してデバッガーを中断し、! process コマンドを使用して、現在は別のプロセスを実行していることを確認します。

```dbgcmd
!process
PROCESS ffffe001cd0ad040
    SessionId: none  Cid: 0004    Peb: 00000000  ParentCid: 0000
    DirBase: 001aa000  ObjectTable: ffffc00017214000  HandleCount: <Data Not Accessible>
    Image: System
    VadRoot ffffe001d402b820 Vads 438 Clone 0 Private 13417. Modified 87866. Locked 64.
    DeviceMap ffffc0001721a070
    Token                             ffffc00017216a60
    ElapsedTime                       05:04:54.716
    UserTime                          00:00:00.000
    KernelTime                        00:00:20.531
    QuotaPoolUsage[PagedPool]         0
    QuotaPoolUsage[NonPagedPool]      0
    Working Set Sizes (now,min,max)  (1720, 50, 450) (6880KB, 200KB, 1800KB)
    PeakWorkingSetSize                15853
    VirtualSize                       58 Mb
    PeakVirtualSize                   74 Mb
    PageFaultCount                    46128
   MemoryPriority                    BACKGROUND
    BasePriority                      8
    CommitCharge                      66

        THREAD ffffe001cd0295c0  Cid 0004.000c  Teb: 0000000000000000 Win32Thread: 0000000000000000 WAIT: (Executive) KernelMode Non-Alertable
            fffff803cd8e0120  SynchronizationEvent

        THREAD ffffe001cd02a6c0  Cid 0004.0010  Teb: 0000000000000000 Win32Thread: 0000000000000000 WAIT: (Executive) KernelMode Non-Alertable
            fffff803cd8e0ba0  Semaphore Limit 0x7fffffff
...
```

上記の出力は、 *ffffe001cd0ad040*の異なるシステムプロセスが実行されていることを示しています。 イメージ名は、audiodg.exe ではなく、システムを示します。

ここで、! process コマンドを使用して、audiodg.exe に関連付けられているプロセスに切り替えます。 この例では、プロセス ID は*ffffe001d147c840*です。 例のプロセス ID を、前に記録したプロセス ID に置き換えます。

```dbgcmd
0: kd> !process  ffffe001d147c840
PROCESS ffffe001d147c840
    SessionId: 0  Cid: 10f0    Peb: ee6cf8a000  ParentCid: 0434
    DirBase: d2122000  ObjectTable: ffffc0001f191ac0  HandleCount: <Data Not Accessible>
    Image: audiodg.exe
    VadRoot ffffe001d4222f70 Vads 60 Clone 0 Private 299. Modified 152. Locked 0.
    DeviceMap ffffc00019113080
    Token                             ffffc0001f1d4060
    ElapsedTime                       1 Day 01:53:14.490
    UserTime                          00:00:00.031
    KernelTime                        00:00:00.031
    QuotaPoolUsage[PagedPool]         81552
    QuotaPoolUsage[NonPagedPool]      8344
    Working Set Sizes (now,min,max)  (1915, 1814, 2109) (7660KB, 7256KB, 8436KB)
    PeakWorkingSetSize                2116
    VirtualSize                       2097189 Mb
    PeakVirtualSize                   2097192 Mb
    PageFaultCount                    2464
    MemoryPriority                    BACKGROUND
    BasePriority                      8
    CommitCharge                      1418

        THREAD ffffe001d173e840  Cid 10f0.1dac  Teb: 000000ee6cf8b000 Win32Thread: ffffe001d1118cf0 WAIT: (UserRequest) UserMode Non-Alertable
            ffffe001d16c4dd0  NotificationEvent
            ffffe001d08b0840  ProcessObject
        Not impersonating
        DeviceMap                 ffffc00019113080
        Owning Process            ffffe001d147c840       Image:         audiodg.exe
        Attached Process          N/A            Image:         N/A
        Wait Start TickCount      338852         Ticks: 197682 (0:00:51:28.781)
        Context Switch Count      36             IdealProcessor: 0             
        UserTime                  00:00:00.015
        KernelTime                00:00:00.000
        Win32 Start Address 0x00007ff7fb928de0
        Stack Init ffffd001c2ec6dd0 Current ffffd001c2ec60c0
        Base ffffd001c2ec7000 Limit ffffd001c2ec1000 Call 0
        Priority 8 BasePriority 8 UnusualBoost 0 ForegroundBoost 0 IoPriority 2 PagePriority 5
        Kernel stack not resident.

        THREAD ffffe001d115c080  Cid 10f0.15b4  Teb: 000000ee6cf9b000 Win32Thread: 0000000000000000 WAIT: (WrQueue) UserMode Alertable
            ffffe001d0bf0640  QueueObject
        Not impersonating
        DeviceMap                 ffffc00019113080
        Owning Process            ffffe001d147c840       Image:         audiodg.exe
        Attached Process          N/A            Image:         N/A
        Wait Start TickCount      338852         Ticks: 197682 (0:00:51:28.781)
        Context Switch Count      1              IdealProcessor: 0             
        UserTime                  00:00:00.000
        KernelTime                00:00:00.000
        Win32 Start Address 0x00007fff6978b350
        Stack Init ffffd001c3143dd0 Current ffffd001c3143520
        Base ffffd001c3144000 Limit ffffd001c313e000 Call 0
        Priority 8 BasePriority 8 UnusualBoost 0 ForegroundBoost 0 IoPriority 2 PagePriority 5
        Kernel stack not resident.

        THREAD ffffe001d3a27040  Cid 10f0.17f4  Teb: 000000ee6cf9d000 Win32Thread: 0000000000000000 WAIT: (WrQueue) UserMode Alertable
            ffffe001d173e5c0  QueueObject
        Not impersonating
        DeviceMap                 ffffc00019113080
        Owning Process            ffffe001d147c840       Image:         audiodg.exe
        Attached Process          N/A            Image:         N/A
        Wait Start TickCount      518918         Ticks: 17616 (0:00:04:35.250)
        Context Switch Count      9              IdealProcessor: 1             
        UserTime                  00:00:00.000
        KernelTime                00:00:00.000
        Win32 Start Address 0x00007fff6978b350
        Stack Init ffffd001c70c6dd0 Current ffffd001c70c6520
        Base ffffd001c70c7000 Limit ffffd001c70c1000 Call 0
        Priority 9 BasePriority 8 UnusualBoost 0 ForegroundBoost 0 IoPriority 2 PagePriority 5
        Kernel stack not resident.
```

このコードはアクティブでないため、すべてのスレッドが想定どおり待機状態になっています。

**スレッド**

スレッドを表示および設定するコマンドは、プロセスのコマンドとよく似ています。 スレッドを表示するには、 [**! thread**](-thread.md)コマンドを使用します。 [**スレッド**](-thread--set-register-context-.md)を使用して、現在のスレッドを設定します。

メディアプレーヤーに関連付けられているスレッドを探索するには、もう一度メディアクリップを再生します。 前のセクションで説明したブレークポイントがまだ配置されている場合は、audiodg.exe のコンテキストで停止します。

現在のスレッドの簡単な情報を表示するには、! スレッド-1 0 を使用します。 スレッドアドレス、スレッドとプロセス Id、スレッド環境ブロック (TEB) アドレス、スレッドが実行するために作成された Win32 関数のアドレス (存在する場合)、およびスレッドのスケジュールの状態が表示されます。

```dbgcmd
0: kd> !thread -1 0
THREAD ffffe001d3a27040  Cid 10f0.17f4  Teb: 000000ee6cf9d000 Win32Thread: 0000000000000000 RUNNING on processor 0
```

実行中のスレッドに関する詳細情報を表示するには、「 [**! thread**](-thread.md)」と入力します。 次のような情報が表示されます。

```dbgcmd
0: kd> !thread
THREAD ffffe001d3a27040  Cid 10f0.17f4  Teb: 000000ee6cf9d000 Win32Thread: 0000000000000000 RUNNING on processor 0
IRP List:
    ffffe001d429e580: (0006,02c8) Flags: 000008b4  Mdl: 00000000
Not impersonating
DeviceMap                 ffffc00019113080
Owning Process            ffffe001d147c840       Image:         audiodg.exe
Attached Process          N/A            Image:         N/A
Wait Start TickCount      537630         Ticks: 0
Context Switch Count      63             IdealProcessor: 1             
UserTime                  00:00:00.000
KernelTime                00:00:00.015
Win32 Start Address 0x00007fff6978b350
Stack Init ffffd001c70c6dd0 Current ffffd001c70c6520
Base ffffd001c70c7000 Limit ffffd001c70c1000 Call 0
Priority 8 BasePriority 8 UnusualBoost 0 ForegroundBoost 0 IoPriority 2 PagePriority 5
Child-SP          RetAddr           : Args to Child                                                           : Call Site
ffffd001`c70c62a8 fffff800`7a0fa607 : ffffe001`d4aec5c0 ffffe001`cdefd3d8 ffffe001`d4aec5c0 ffffe001`cdefd390 : tabletaudiosample!CMiniportWaveRT::NewStream [c:\data1\threshold\audio\endpointscommon\minwavert.cpp @ 562]
ffffd001`c70c62b0 fffff800`7a0fb2c3 : 00000000`00000000 ffffe001`d429e580 ffffe001`d4ea47b0 ffffe001`cdefd3d8 : portcls!CPortPinWaveRT::Init+0x2e7
ffffd001`c70c6340 fffff800`7a0fc7f9 : ffffe001`d4aec430 00000000`00000000 ffffe001`d10b8380 ffffe001`d429e580 : portcls!CPortFilterWaveRT::NewIrpTarget+0x193
ffffd001`c70c63c0 fffff800`7a180552 : 00000000`00000000 ffffe001`d10b8380 ffffe001`d429e580 ffffe001`d4565600 : portcls!xDispatchCreate+0xd9
ffffd001`c70c6450 fffff800`7a109a9a : ffffe001`d10b84d0 ffffe001`d10b8380 00000000`00000000 ffffe001`00000000 : ks!KsDispatchIrp+0x272
ffffd001`c70c6510 fffff800`7bd314b1 : ffffe001`d429e580 ffffd001`c70c6590 ffffe001`d429e800 ffffe001`ce80da70 : portcls!DispatchCreate+0x7a
ffffd001`c70c6540 fffff803`cda1bfa8 : 00000000`00000025 00000000`00000000 00000000`00000000 ffffe001`d429e580 : ksthunk!CKernelFilterDevice::DispatchIrp+0xf9
ffffd001`c70c65a0 fffff803`cda7b306 : 00000000`000002fc ffffe001`d5e0d510 00000000`00000000 ffffe001`d3341bd0 : nt!IopParseDevice+0x7c8
ffffd001`c70c6770 fffff803`cda12916 : 00000000`000002fc ffffd001`c70c68d0 ffffe001`d3341ba0 fffff803`cda7b250 : nt!IopParseFile+0xb6
ffffd001`c70c67d0 fffff803`cda1131c : ffffe001`ceb6c601 ffffd001`c70c69e0 00000000`00000040 ffffe001`cd127dc0 : nt!ObpLookupObjectName+0x776
ffffd001`c70c6970 fffff803`cd9fedb8 : ffff8ab8`00000001 ffffe001`d5e0d510 00000000`00000000 00000000`00000000 : nt!ObOpenObjectByNameEx+0x1ec
ffffd001`c70c6a90 fffff803`cd9fe919 : 000000ee`6d37c6e8 00000004`6d37c500 000000ee`6d37c5f0 000000ee`6d37c5e0 : nt!IopCreateFile+0x3d8
ffffd001`c70c6b40 fffff803`cd752fa3 : fffff6fb`7da05360 fffff6fb`40a6c0a8 fffff681`4d815760 ffff8ab8`92895e23 : nt!NtCreateFile+0x79
ffffd001`c70c6bd0 00007fff`69805b74 : 00007fff`487484e6 0000029b`00000003 00000000`0000012e 00000000`00000000 : nt!KiSystemServiceCopyEnd+0x13 (TrapFrame @ ffffd001`c70c6c40)
000000ee`6d37c568 00007fff`487484e6 : 0000029b`00000003 00000000`0000012e 00000000`00000000 00000000`00000000 : 0x00007fff`69805b74
000000ee`6d37c570 0000029b`00000003 : 00000000`0000012e 00000000`00000000 00000000`00000000 00000000`00000000 : 0x00007fff`487484e6
000000ee`6d37c578 00000000`0000012e : 00000000`00000000 00000000`00000000 00000000`00000000 00000000`00000080 : 0x0000029b`00000003
000000ee`6d37c580 00000000`00000000 : 00000000`00000000 00000000`00000000 00000000`00000080 00000000`00000000 : 0x12e
```

K コマンドを使用して、スレッドに関連付けられている呼び出し履歴を表示します。

```dbgcmd
0: kd> k
# Child-SP          RetAddr           Call Site
00 ffffd001`c70c62a8 fffff800`7a0fa607 tabletaudiosample!CMiniportWaveRT::NewStream [c:\data1\threshold\audio\endpointscommon\minwavert.cpp @ 562]
01 ffffd001`c70c62b0 fffff800`7a0fb2c3 portcls!CPortPinWaveRT::Init+0x2e7
02 ffffd001`c70c6340 fffff800`7a0fc7f9 portcls!CPortFilterWaveRT::NewIrpTarget+0x193
03 ffffd001`c70c63c0 fffff800`7a180552 portcls!xDispatchCreate+0xd9
04 ffffd001`c70c6450 fffff800`7a109a9a ks!KsDispatchIrp+0x272
05 ffffd001`c70c6510 fffff800`7bd314b1 portcls!DispatchCreate+0x7a
06 ffffd001`c70c6540 fffff803`cda1bfa8 ksthunk!CKernelFilterDevice::DispatchIrp+0xf9
07 ffffd001`c70c65a0 fffff803`cda7b306 nt!IopParseDevice+0x7c8
08 ffffd001`c70c6770 fffff803`cda12916 nt!IopParseFile+0xb6
09 ffffd001`c70c67d0 fffff803`cda1131c nt!ObpLookupObjectName+0x776
0a ffffd001`c70c6970 fffff803`cd9fedb8 nt!ObOpenObjectByNameEx+0x1ec
0b ffffd001`c70c6a90 fffff803`cd9fe919 nt!IopCreateFile+0x3d8
0c ffffd001`c70c6b40 fffff803`cd752fa3 nt!NtCreateFile+0x79
0d ffffd001`c70c6bd0 00007fff`69805b74 nt!KiSystemServiceCopyEnd+0x13
0e 000000ee`6d37c568 00007fff`487484e6 0x00007fff`69805b74
0f 000000ee`6d37c570 0000029b`00000003 0x00007fff`487484e6
10 000000ee`6d37c578 00000000`0000012e 0x0000029b`00000003
11 000000ee`6d37c580 00000000`00000000 0x12e
```

デバッガーに g を入力して、メディアクリップの再生が完了するまでコードを実行します。 次に、Ctrl + ScrLk (Ctrl + Break) キーを押して、デバッガーを中断します。次に、! thread コマンドを使用して、別のスレッドが実行されていることを確認します。

```dbgcmd
0: kd> !thread
THREAD ffffe001ce80b840  Cid 17e4.01ec  Teb: 00000071fa9b9000 Win32Thread: ffffe001d41690d0 RUNNING on processor 0
Not impersonating
DeviceMap                 ffffc0001974e2c0
Owning Process            ffffe001d1760840       Image:         rundll32.exe
Attached Process          N/A            Image:         N/A
Wait Start TickCount      538040         Ticks: 0
Context Switch Count      3181840        IdealProcessor: 0             
UserTime                  00:00:08.250
KernelTime                00:00:10.796
Win32 Start Address 0x00007ff6d2f24270
Stack Init ffffd001cd16afd0 Current ffffd001cd16a730
Base ffffd001cd16b000 Limit ffffd001cd165000 Call 0
Priority 8 BasePriority 8 UnusualBoost 0 ForegroundBoost 0 IoPriority 2 PagePriority 5

Child-SP          RetAddr           : Args to Child                                                           : Call Site
fffff803`cf373d18 fffff800`7a202852 : fffff803`cf373e60 00000000`00000001 ffffe001`cf4ed330 00000000`0000ffff : nt!DbgBreakPointWithStatus
fffff803`cf373d20 fffff803`cd6742c6 : ffffe001`cf4ed2f0 fffff803`cf373e60 00000000`00000001 00000000`0004e4b8 : kdnic!TXSendCompleteDpc+0x142
fffff803`cf373d60 fffff803`cd74d495 : 00000000`00000000 fffff803`cd923180 fffff803`cde1f4b0 fffff901`40669010 : nt!KiRetireDpcList+0x5f6
fffff803`cf373fb0 fffff803`cd74d2a0 : 00000000`00000090 0000000e`0000006a 00000000`00000092 00000000`00000000 : nt!KxRetireDpcList+0x5 (TrapFrame @ fffff803`cf373e70)
ffffd001`cd16a6c0 fffff803`cd74bd75 : 00000000`00000000 fffff803`cd74a031 00000000`00000000 00000000`00000000 : nt!KiDispatchInterruptContinue
ffffd001`cd16a6f0 fffff803`cd74a031 : 00000000`00000000 00000000`00000000 ffffe001`cff4d2a0 fffff803`cd67738e : nt!KiDpcInterruptBypass+0x25
ffffd001`cd16a700 fffff960`50cdb5a4 : fffff901`400006d0 00000000`00000001 fffff901`40000d60 ffffd001`cd16a9f0 : nt!KiInterruptDispatchNoLockNoEtw+0xb1 (TrapFrame @ ffffd001`cd16a700)
ffffd001`cd16a890 fffff960`50c66b2f : 00000000`00000000 fffff901`40669010 fffff901`42358580 fffff901`40000d60 : win32kfull!Win32FreePoolImpl+0x34
ffffd001`cd16a8c0 fffff960`50c68cd6 : 00000000`00000000 ffffd001`cd16a9f0 fffff901`400006d0 fffff901`400c0460 : win32kfull!EXLATEOBJ::vAltUnlock+0x1f
ffffd001`cd16a8f0 fffff803`cd752fa3 : 00000000`00000000 00000000`00000000 ffffe001`ce80b840 00000000`00000000 : win32kfull!NtGdiAlphaBlend+0x1d16
ffffd001`cd16add0 00007fff`674c1494 : 00007fff`674b1e97 0000a7c6`daee0559 00000000`00000001 0000020b`741f3c50 : nt!KiSystemServiceCopyEnd+0x13 (TrapFrame @ ffffd001`cd16ae40)
00000071`fa74c9a8 00007fff`674b1e97 : 0000a7c6`daee0559 00000000`00000001 0000020b`741f3c50 00000000`00ffffff : 0x00007fff`674c1494
00000071`fa74c9b0 0000a7c6`daee0559 : 00000000`00000001 0000020b`741f3c50 00000000`00ffffff 00000000`00000030 : 0x00007fff`674b1e97
00000071`fa74c9b8 00000000`00000001 : 0000020b`741f3c50 00000000`00ffffff 00000000`00000030 00000000`01010bff : 0x0000a7c6`daee0559
00000071`fa74c9c0 0000020b`741f3c50 : 00000000`00ffffff 00000000`00000030 00000000`01010bff 00000000`00000000 : 0x1
00000071`fa74c9c8 00000000`00ffffff : 00000000`00000030 00000000`01010bff 00000000`00000000 00000000`000000c0 : 0x0000020b`741f3c50
00000071`fa74c9d0 00000000`00000030 : 00000000`01010bff 00000000`00000000 00000000`000000c0 00000000`00000030 : 0xffffff
00000071`fa74c9d8 00000000`01010bff : 00000000`00000000 00000000`000000c0 00000000`00000030 00000071`00000030 : 0x30
00000071`fa74c9e0 00000000`00000000 : 00000000`000000c0 00000000`00000030 00000071`00000030 00000071`01ff8000 : 0x1010bff
```

イメージ名は rundll32.exe であり、実際にはメディアクリップの再生に関連付けられているイメージ名ではありません。

**メモ**   現在のスレッドを設定するには、「スレッドスレッド番号」と入力します。 &lt; &gt;

スレッドとプロセスの詳細については、次の参照情報を参照してください。

[スレッドとプロセス](threads-and-processes.md)

[コンテキストの変更](changing-contexts.md)

 

## <a name="span-idirqlregistersmemoryspansection-11-irql-registers-and-disassembly"></a><span id="irqlregistersmemory"></span>セクション 11: IRQL、レジスタ、および逆アセンブリ


### <a name="span-idview_the_saved_irqlspanview-the-saved-irql"></a><span id="view_the_saved_irql"></span>保存された IRQL を表示する

*セクション11では、IRQL と、regsisters の内容を表示します。*

**&lt;-ホストシステム上**

割り込み要求レベル (IRQL) は、割り込みサービスの優先順位を管理するために使用されます。 各プロセッサには、スレッドが発生させることのできる IRQL の設定があります。 プロセッサの IRQL 設定の下または下で発生する割り込みはマスクされ、現在の操作に干渉することはありません。 プロセッサの IRQL 設定を超える割り込みは、現在の操作よりも優先されます。 [**! Irql**](-irql.md) extension は、デバッガーが中断される前に、対象のコンピューターの現在のプロセッサに割り込み要求レベル (irql) を表示します。 対象のコンピューターがデバッガーに分割されると、IRQL は変わりますが、デバッガーの中断直前に有効だった IRQL は保存され、! irql によって表示されます。

```dbgcmd
0: kd> !irql
Debugger saved IRQL for processor 0x0 -- 2 (DISPATCH_LEVEL)
```

### <a name="span-idviewingtheregistersspanview-the-registers-and-disassembly"></a><<span id="viewingtheregisters"></span>レジスタと逆アセンブリの表示

**レジスタを表示する**

[**R (register)**](r--registers-.md)コマンドを使用して、現在のプロセッサの現在のスレッドのレジスタの内容を表示します。

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

または、[レジスタの**表示**] をクリックしてレジスタの内容を表示することもでき &gt; **Registers**ます。

![約12レジスタを示す windbg レジスタウィンドウ](images/sysvad-lab-audio-display-registers.png)

レジスタの内容を表示することは、アセンブリ言語コードの実行やその他のシナリオでステップ実行するときに役立ちます。 詳細については、「 [**r (レジスタ)**](r--registers-.md)」を参照してください。

レジスタの内容の詳細については、「 [X86 アーキテクチャ](x86-architecture.md)と[x64 アーキテクチャ](x64-architecture.md)」を参照してください。

**逆アセンブリ**

実行中のコードを逆アセンブルして、実行されているアセンブリ言語コードを表示する**View**には、[ &gt; **逆アセンブル**の表示] をクリックします。

![[windbg 逆アセンブリ] ウィンドウ](images/sysvad-lab-audio-disassembly-window.png)

アセンブリ言語の逆アセンブリの詳細については、「[注釈付き X86 逆アセンブリ](annotated-x86-disassembly.md)」および「[注釈付き x64 逆アセンブル](annotated-x64-disassembly.md)」を参照してください。

## <a name="span-idworkingwithmemoryspansection-12-work-with-memory"></a><span id="workingwithmemory"></span>セクション 12: メモリの操作


*セクション12では、デバッガーコマンドを使用してメモリの内容を表示します。*

**メモリの表示**

場合によっては、メモリを調べて問題を特定したり、変数やポインターなどを検査したりすることが必要になる場合があります。 次のいずれかの**d \* &lt; &gt; アドレス**コマンドを入力すると、メモリを表示できます。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>db</p></td>
<td align="left"><p>バイト値と ASCII 文字でデータを表示します。</p></td>
</tr>
<tr class="even">
<td align="left"><p>dd</p></td>
<td align="left"><p>データを double 型のワード (4 バイト) として表示します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>du</p></td>
<td align="left"><p>データを Unicode 文字として表示します。</p></td>
</tr>
<tr class="even">
<td align="left"><p>dw</p></td>
<td align="left"><p>データをワード値 (2 バイト) および ASCII 文字として表示します。</p></td>
</tr>
</tbody>
</table>

 

**メモ**   無効なアドレスを表示しようとすると、その内容は疑問符 (?) として表示されます。

 

または、[メモリの**表示**] をクリックしてメモリを表示することもでき &gt; **Memory**ます。 **表示形式**のプルダウンを使用して、メモリの表示方法を変更します。

![windbg ビューメモリウィンドウ](images/sysvad-lab-audio-memory-display.png)

1.  ボリュームコントロールに関連付けられているデータを表示するには、bm コマンドを使用して、PropertyHandlerAudioEngineVolumeLevel ルーチンで起動するようにブレークポイントを設定します。 新しいブレークポイントを設定する前に、bc を使用して前のすべてのブレークポイントをクリアし \* ます。

    ```dbgcmd
    kd> bc *
    ```

2.  Bm コマンドを使用して、PropertyHandlerAudioEngineVolumeLevel ルーチンで起動するようにブレークポイントを設定します。

    ```dbgcmd
    kd> bm tabletaudiosample!CMiniportWaveRT::SetDeviceChannelVolume
      1: fffff80f`02c3a4b0 @!"tabletaudiosample!CMiniportWaveRT::SetDeviceChannelVolume"
    ```

3.  ブレークポイントを一覧表示して、ブレークポイントが適切に設定されていることを確認します。

    ```dbgcmd
    kd> bl
      1: fffff80f`02c3a4b0 @!"tabletaudiosample!CMiniportWaveRT::SetDeviceChannelVolume"
    ```

4.  **G**コマンドを使用して、コードの実行を再開します。

    ターゲットシステムで、システムトレイのボリュームを調整します。 これにより、ブレークポイントが起動されます。

    ```dbgcmd
    Breakpoint 1 hit
    tabletaudiosample!CMiniportWaveRT::SetDeviceChannelVolume:
    fffff80f`02c3a4b0 44894c2420      mov     dword ptr [rsp+20h],r9d
    ```

5.  ローカル**View** &gt; 変数を表示するには、[**ローカル**の表示] メニュー項目を使用します。 IVolume 変数の現在の値を確認します。

6.  サンプルコードの IVolume 変数のデータ型と現在の値を表示するには、 **dt**コマンドと変数の名前を入力します。

    ```dbgcmd
    kd> dt lVolume
    Local var @ 0xa011ea50 Type long
    0n-6291456
    ```

7.  ブレークポイントは、SetDeviceChannelVolume を入力したときにヒットします。

    ```dbgcmd
    STDMETHODIMP_(NTSTATUS) CMiniportWaveRT::SetDeviceChannelVolume(_In_  ULONG _ulNodeId, _In_ UINT32 _uiChannel, _In_  LONG  _Volume)
    {
        NTSTATUS ntStatus = STATUS_INVALID_DEVICE_REQUEST;

        PAGED_CODE ();

        DPF_ENTER(("[CMiniportWaveRT::SetEndpointChannelVolume]"));
        IF_TRUE_ACTION_JUMP(_ulNodeId != KSNODE_WAVE_AUDIO_ENGINE, ntStatus = STATUS_INVALID_DEVICE_REQUEST, Exit);

        // Snap the volume level to our range of steppings.
        LONG lVolume = VOLUME_NORMALIZE_IN_RANGE(_Volume); 

        ntStatus = SetChannelVolume(_uiChannel, lVolume);
    Exit:
        return ntStatus;
    }
    ```

8.  [**Dt (Display Type)**](dt--display-type-.md)コマンドを使用して、ivolume のメモリ位置に値を表示しようとしています。

    ```dbgcmd
    kd> dt dt lVolume
    Local var @ 0xffffb780b7eee664 Type long
    0n0
    ```

    変数はまだ定義されていないため、情報は含まれません。

9.  F10 キーを押して、SetDeviceChannelVolume のコードの最後の行に進みます。

    ```dbgcmd
        return ntStatus;
    ```

10. [ [**Dt (Display Type)**](dt--display-type-.md) ] コマンドを使用して、ivolume のメモリ位置に値を表示します。

    ```dbgcmd
    kd> dt lVolume
    Local var @ 0xffffb780b7eee664 Type long
    0n-6291456
    ```

    変数がアクティブになったので、この例では6291456の値が表示されます。

11. また、を使用して、IVolume のメモリの場所を表示することもできます[**。(式の評価)**](---evaluate-expression-.md)メニュー.

    ```dbgcmd
    kd> ? lVolume
    Evaluate expression: -79711507126684 = ffffb780`b7eee664
    ```

12. 表示されるアドレスは、 *ffffb780 \` B7eee664*は lvolume 変数のアドレスです。 Dd コマンドを使用して、その場所のメモリの内容を表示します。

    ```dbgcmd
    kd>  dd ffffb780`b7eee664
    ffffb780`b7eee664  ffa00000 00000018 00000000 c52d7008
    ffffb780`b7eee674  ffffc98e e0495756 fffff80e c52d7008
    ffffb780`b7eee684  ffffc98e 00000000 fffff80e 00000000
    ffffb780`b7eee694  ffffc98e ffa00000 ffffb780 b7eee710
    ffffb780`b7eee6a4  ffffb780 00000000 00000000 c7477260
    ffffb780`b7eee6b4  ffffc98e b7eee7a0 ffffb780 b7eee6f0
    ffffb780`b7eee6c4  ffffb780 e04959ca fffff80e 00000000
    ffffb780`b7eee6d4  00000000 00000028 00000000 00000002
    ```

13. 範囲パラメーター L4 を指定すると、アドレスの最初の4バイトを表示できます。

    ```dbgcmd
    kd> dd ffffb780`b7eee664 l4
    ffffb780`b7eee664  ffa00000 00000018 00000000 c52d7008
    ```

14. 表示されるさまざまな種類のメモリ出力を確認するには、 **du**、 **da** 、および**db**コマンドを入力します。

    ```dbgcmd
    kd> du ffffb780`b7eee664 
    ffffb780`b7eee664  ""

    kd> a ffffb780`b7eee664 
    ffffb780`b7eee664  ""

    kd> db 0xffffae015ff97664 
    ffffae01`5ff97664  00 80 bc ff 18 00 00 00-00 00 00 00 08 50 e0 51  .............P.Q
    ffffae01`5ff97674  00 c0 ff ff 56 57 da 56-0e f8 ff ff 08 50 e0 51  ....VW.V.....P.Q
    ffffae01`5ff97684  00 c0 ff ff 00 00 00 00-0e f8 ff ff 00 00 00 00  ................
    ffffae01`5ff97694  00 c0 ff ff aa 80 bc ff-01 ae ff ff 10 77 f9 5f  .............w._
    ffffae01`5ff976a4  01 ae ff ff 40 00 00 00-00 e6 ff ff 10 dc 30 55  ....@.........0U
    ffffae01`5ff976b4  00 c0 ff ff a0 77 f9 5f-01 ae ff ff f0 76 f9 5f  .....w._.....v._
    ffffae01`5ff976c4  01 ae ff ff ca 59 da 56-0e f8 ff ff 00 00 00 00  .....Y.V........
    ffffae01`5ff976d4  00 00 00 00 28 00 00 00-00 00 00 00 02 00 00 00  ....(...........
    ```

    Df float オプションを使用して、データを単精度浮動小数点数 (4 バイト) として表示します。

    ```dbgcmd
    df ffffb780`b7eee664 
    ffffb780`b7eee664          -1.#QNAN   3.3631163e-044                0        -2775.002
    ffffb780`b7eee674          -1.#QNAN  -5.8032637e+019         -1.#QNAN        -2775.002
    ffffb780`b7eee684          -1.#QNAN                0         -1.#QNAN                0
    ffffb780`b7eee694          -1.#QNAN         -1.#QNAN         -1.#QNAN  -2.8479408e-005
    ```

**メモリへの書き込み**

メモリの読み取りに使用されるコマンドと同様に、e コマンドを使用して \* メモリの内容を変更できます。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">コマンド</th>
<th align="left">説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>ea</p></td>
<td align="left"><p>ASCII 文字列 (NULL で終わっていない)</p></td>
</tr>
<tr class="even">
<td align="left"><p>eu</p></td>
<td align="left"><p>Unicode 文字列 (NULL で終わらない)</p></td>
</tr>
<tr class="odd">
<td align="left"><p>週間</p></td>
<td align="left"><p>単語の値 (2 バイト)</p></td>
</tr>
<tr class="even">
<td align="left"><p>eza</p></td>
<td align="left"><p>NULL で終わる ASCII 文字列</p></td>
</tr>
<tr class="odd">
<td align="left"><p>ezu</p></td>
<td align="left"><p>NULL で終わる Unicode 文字列</p></td>
</tr>
<tr class="even">
<td align="left"><p>e)</p></td>
<td align="left"><p>バイト値</p></td>
</tr>
<tr class="odd">
<td align="left"><p>ed</p></td>
<td align="left"><p>ダブルワード値 (4 バイト)</p></td>
</tr>
</tbody>
</table>

 

次の例は、メモリを上書きする方法を示しています。

1.  まず、サンプルコードで使用している lVolume のアドレスを見つけます。

    ```dbgcmd
    kd> ? lVolume
    Evaluate expression: -79711507126684 = ffffb780`b7eee664
    ```

2.  **Eb**コマンドを使用して、そのメモリアドレスを新しい文字で上書きします。

    ```dbgcmd
    kd> eb 0xffffb780`b7eee664 11 11 11 11 11
    ```

3.  メモリの場所を表示し、 **db**コマンドを入力して文字が上書きされていることを確認します。

    ```dbgcmd
    kd> db 0xffffb780`b7eee664
    ffffb780`b7eee664  11 11 11 11 11 00 00 00-00 00 00 00 08 70 2d c5  .............p-.
    ffffb780`b7eee674  8e c9 ff ff 56 57 49 e0-0e f8 ff ff 08 70 2d c5  ....VWI......p-.
    ffffb780`b7eee684  8e c9 ff ff 00 00 00 00-0e f8 ff ff 00 00 00 00  ................
    ffffb780`b7eee694  8e c9 ff ff 00 00 a0 ff-80 b7 ff ff 10 e7 ee b7  ................
    ffffb780`b7eee6a4  80 b7 ff ff 00 00 00 00-00 00 00 00 60 72 47 c7  ............`rG.
    ffffb780`b7eee6b4  8e c9 ff ff a0 e7 ee b7-80 b7 ff ff f0 e6 ee b7  ................
    ffffb780`b7eee6c4  80 b7 ff ff ca 59 49 e0-0e f8 ff ff 00 00 00 00  .....YI.........
    ffffb780`b7eee6d4  00 00 00 00 28 00 00 00-00 00 00 00 02 00 00 00  ....(...........
    ```

または、[ウォッチ] ウィンドウまたは [ローカル] ウィンドウでメモリの内容を変更することもできます。 [ウォッチ] ウィンドウには、現在のフレームのコンテキスト外の変数が表示される場合があります。 コンテキストに含まれていない場合、変更は関係ありません。

## <a name="span-idendingthesessionspansection-13-end-the-windbg-session"></a><span id="endingthesession"></span>セクション 13: WinDbg セッションを終了する


**&lt;-ホストシステム上**

ユーザーモードのデバッグセッションを終了し、デバッガーを休止モードに戻して、ターゲットアプリケーションを再度実行するように設定するには、 **qd** (Quit および Detach) コマンドを入力します。

使用できるように、ターゲットコンピューターにコードを実行させるには、必ず**g**コマンドを使用してください。 また、* * bc * * * を使用してブレークポイントを削除することもでき \\ ます。これにより、対象のコンピュータが中断せずにホストコンピュータデバッガーに接続しようとすることができなくなります。

```dbgcmd
0: kd> qd
```

詳細については、デバッグリファレンスドキュメントの「 [WinDbg でのデバッグセッションの終了](ending-a-debugging-session-in-windbg.md)」を参照してください。

## <a name="span-idwindowsdebuggingresourcesspansection-14-windows-debugging-resources"></a><span id="windowsdebuggingresources"></span>セクション 14: Windows デバッグリソース


詳細については、「Windows デバッグ」を参照してください。 これらの書籍には、windows Vista などの古いバージョンの Windows を例で使用するものがありますが、ここで説明する概念は、Windows のほとんどのバージョンに適用されます。

**書籍**

-   Mario Hewardt と Daniel Pravat による*高度な Windows デバッグ*

-   *Windows のデバッグ: Tarik Soulami による windows®でのデバッグとトレースの方法に関する実用的なガイド*

-   *Windows の内部構造*をマーク Russinovich、David A ソロモン、Alex Ionescu

**ビデオ**

デフラグツールでは、WinDbg エピソード13-29 が表示されます。<https://channel9.msdn.com/Shows/Defrag-Tools>

**ベンダーのトレーニング:**

OSR<https://www.osr.com/>


## <a name="see-also"></a>参照

[Windows のデバッグの概要](getting-started-with-windows-debugging.md) 

 






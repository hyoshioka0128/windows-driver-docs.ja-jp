---
title: ステップ バイ ステップのラボ (Sysvad カーネル モード) - ドライバのデバッグします。
description: このラボでは、ハンズオン演習で Sysvad オーディオのカーネル モード デバイス ドライバーをデバッグする方法を紹介を提供します。
ms.assetid: 4A31451C-FC7E-4C5F-B4EB-FBBAC8DADF9E
keywords:
- ラボをデバッグします。
- ステップ バイ ステップ
- SYSVAD
ms.date: 02/21/2019
ms.localizationpriority: medium
ms.openlocfilehash: c44da033442bc81d65d1ba5ec7e439454fb7308a
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67361446"
---
# <a name="span-iddebuggerdebuguniversaldriverskernel-modespandebug-drivers---step-by-step-lab-sysvad-kernel-mode"></a><span id="debugger.debug_universal_drivers__kernel-mode_"></span>ステップ バイ ステップのラボ (Sysvad カーネル モード) - ドライバのデバッグします。

このラボでは、ハンズオン演習で Sysvad オーディオのカーネル モード デバイス ドライバーをデバッグする方法を紹介を提供します。

Microsoft Windows デバッガー (WinDbg) は、強力な Windows ベース デバッグ ツール ユーザー モードおよびカーネル モードのデバッグを実行に使用できます。 WinDbg では、Windows のカーネル、カーネル モード ドライバー、およびシステムのサービスだけでなくユーザー モード アプリケーションとドライバーのソース レベルのデバッグを提供します。

WinDbg ステップにより、ブレークポイントの設定のソース コード (C++ オブジェクトを含む) の変数、スタック トレース、およびメモリを表示します。 デバッガー コマンド ウィンドウは、さまざまなコマンドを発行するユーザーを使用できます。

## <a name="span-idlabsetupspanlab-setup"></a><span id="lab_setup"></span>ラボのセットアップ

次のハードウェア ラボを完成させることができる必要があります。

-   ラップトップまたはデスクトップ コンピューター (ホスト) Windows 10 を実行しています。
-   ラップトップまたはデスクトップ コンピューター (ターゲット) Windows 10 を実行しています。
-   ネットワーク ハブまたはルーターと 2 台の Pc に接続するネットワーク ケーブル
-   シンボル ファイルをダウンロードにインターネットへのアクセス

次のソフトウェアのラボを完成させることができる必要があります。

-   Microsoft Visual Studio 2017
-   Windows 10 用 Windows ソフトウェア開発キット (SDK)
-   Windows 10 用 Windows Driver Kit (WDK)
-   Windows 10 用サンプル Sysvad オーディオ ドライバー

ダウンロードして、WDK をインストールする方法については、次を参照してください。 [Windows Driver Kit (WDK) のダウンロード](https://docs.microsoft.com/windows-hardware/drivers/download-the-wdk)します。

## <a name="span-idsysvaddebuggingwalkthroughoverviewspansysvad-debugging-walkthrough"></a><span id="sysvad_debugging_walkthrough_overview"></span>Sysvad デバッグ チュートリアル


このラボでは、カーネル モード ドライバーをデバッグするプロセスを説明します。 演習では、Syvad 仮想オーディオ ドライバーのサンプルを使用します。 Syvad オーディオ ドライバーは、実際のオーディオ ハードウェアで作用せず、ために、ほとんどのデバイスで使用できます。 ラボでは、次のタスクについて説明します。

-   [セクション 1:カーネル モード WinDbg セッションに接続します。](#connectto)
-   [セクション 2: カーネル モードのデバッグ コマンドや技法](#kernelmodedebuggingcommandsandtechniques)
-   [セクション 3:ダウンロードして Sysvad オーディオ ドライバーのビルド](#download)
-   [セクション 4:ターゲット システム上の Sysvad オーディオ ドライバーをインストールします。](#install)
-   [セクション 5:WinDbg を使用して、ドライバーに関する情報を表示するには](#usewindbgtodisplayinformation)
-   [セクション 6:プラグ アンド プレイ デバイス ツリーの情報を表示します。](#displayingtheplugandplaydevicetree)
-   [セクション 7:ブレークポイントとソース コードを使用します。](#workingwithbreakpoints)
-   [セクション 8:変数を確認します。](#lookingatvariables)
-   [セクション 9:呼び出し履歴の表示](#viewingcallstacks)
-   [セクションの 10:表示のプロセスとスレッド](#displayingprocessesandthreads)
-   [第 11 条:IRQL、レジスタとの逆アセンブル](#irqlregistersmemory)
-   [セクション 12:メモリを使用します。](#workingwithmemory)
-   [セクション 13:WinDbg のセッションを終了します。](#endingthesession)
-   [セクション 14:Windows デバッグ用のリソース](#windowsdebuggingresources)

## <a name="span-idechodriverlabspanecho-driver-lab"></a><span id="echo_driver_lab"></span>エコー ドライバー ラボ


エコー ドライバーは、単純なドライバー Sysvad オーディオ ドライバー、です。 WinDbg に慣れていない場合は、最初に実行してくださいたい、[ユニバーサル ドライバーのデバッグのステップ バイ ステップのラボ (エコー カーネル モード)](debug-universal-drivers---step-by-step-lab--echo-kernel-mode-.md)します。 このラボでは、その演習を完了している場合は、1 と 2 次のセクションを省略できますのでからこの演習では、セットアップの指示が再利用します。

## <a name="span-idconnecttospansection-1-connect-to-a-kernel-mode-windbg-session"></a><span id="connectto"></span>セクション 1:カーネル モード WinDbg セッションに接続します。


*セクション 1 では、ネットワークのホストとターゲット システム上でデバッグを構成します。*

このラボでの Pc は、カーネル デバッグをイーサネット ネットワーク接続を使用するように構成する必要があります。

この演習では、2 台のコンピューターを使用します。 WinDbg 上で実行、*ホスト*実行されるシステムと Sysvad ドライバー、*ターゲット*システム。

 ネットワーク ハブまたはルーターとのネットワーク ケーブルを使用して、2 台の Pc を接続します。

![二重矢印で接続されている 2 台の pc](images/debuglab-image-targethostdrawing1.png)

カーネル モードのアプリケーションを使用し、WinDbg を使用して、イーサネット転送を KDNET を使用することをお勧めします。 イーサネット トランスポート プロトコルを使用する方法については、次を参照してください。 [WinDbg (カーネル モード) の概要](getting-started-with-windbg--kernel-mode-.md)します。 ターゲット コンピューターの設定に関する詳細については、次を参照してください。[手動ドライバーの展開のコンピューターを準備する](https://docs.microsoft.com/windows-hardware/drivers)と[設定を KDNET ネットワーク カーネル デバッグを自動的に](setting-up-a-network-debugging-connection-automatically.md)します。

### <a name="span-idconfigurekernelmodedebuggingusingethernetspanconfigure-kernelmode-debugging-using-ethernet"></a><span id="configure__kernel_mode_debugging_using_ethernet"></span>イーサネットを使用してカーネル – モードのデバッグを構成します。

カーネル モードでは、ターゲット システムでのデバッグを有効にするには、次の手順を実行します。

**&lt;ホスト システムで**

1. ホスト システムと種類でコマンド プロンプトを開き**ipconfig/all**その IP アドレスを確認します。

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

2. ホスト システムの IP アドレスを記録します。 \_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_

3. ホスト システムのホスト名を記録します。 \_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_

**-&gt; ターゲット システム**

4. ターゲット システムでコマンド プロンプトを開きを使用して、 **ping**コマンドを 2 つのシステム間のネットワーク接続を確認します。 169.182.1.1 サンプル出力に表示されるのではなく、記録したホスト システムの実際の IP アドレスを使用します。

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

カーネル モードで、次の手順を実行、ターゲット システムでデバッグを有効にするのにには、KDNET ユーティリティを使用します。

1. ホスト システムでは、WDK KDNET ディレクトリを見つけます。 既定ではこちらです。

   C:\Program Files (x86)\Windows Kits\10\Debuggers\x64

> [!NOTE]
> このラボでは、両方の Pc が実行されていること、64 ビット バージョンは、参照のターゲットとホストの両方を前提としています。 場合はそうでない、最適な方法では、ターゲットを実行しているホストでツールの同じ「ビット数」を実行します。 たとえば、ターゲットが実行されている 32 ビット Windows では、ホスト上で 32 のバージョンのデバッガーを実行している場合です。 詳細については、次を参照してください。 [32 ビットまたは 64 ビット デバッグ ツールを選択する](choosing-a-32-bit-or-64-bit-debugger-package.md)します。
> 

2. これら 2 つのファイルし、ネットワーク共有にコピーまたはつまみのドライブでは、ターゲット コンピューター上で使用できるようにします。

    kdnet.exe

    VerifiedNICList.xml


3. ターゲット コンピューターで、管理者としてコマンド プロンプト ウィンドウを開きます。 ターゲット PC に NIC がサポートされていることを確認するには、このコマンドを入力します。

```console
C:\KDNET>kdnet

Network debugging is supported on the following NICs:
busparams=0.25.0, Intel(R) 82579LM Gigabit Network Connection, KDNET is running on this NIC.kdnet.exe
```

4. ホスト システムの IP アドレスを設定するには、このコマンドを入力します。 169.182.1.1 サンプル出力に表示されるのではなく、記録したホスト システムの実際の IP アドレスを使用します。 50010 など、使用するターゲット/ホスト ペアごとに一意のポート アドレスを選択します。

```console
C:\>kdnet 169.182.1.1 50010

Enabling network debugging on Intel(R) 82577LM Gigabit Network Connection.
Key=2steg4fzbj2sz.23418vzkd4ko3.1g34ou07z4pev.1sp3yo9yz874p
```

> [!IMPORTANT]
> BCDEdit を使用してブート情報を変更する前に、テスト用のコンピューターの BitLocker とセキュア ブートなどの Windows セキュリティ機能を一時的に中断する必要があります。
> テストが完了すると、これらのセキュリティ機能を再度有効にし、適切なセキュリティ機能を無効にするテスト PC を管理します。
>

5. Dbgsettings が正しく設定されていることを確認するには、このコマンドを入力します。

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

自動コピーでは、ホスト PC 上で入力することを回避するために、テキスト ファイルに一意のキーが生成されます。 ホスト システムにキーを使用して経由でのテキスト ファイルをコピーします。

**注**  
**ファイアウォールとデバッガー**

確認の場合は、ファイアウォールからポップアップ メッセージを受信して、デバッガーを使用する、 **3 つすべて**ボックス。

![windows セキュリティの警告 - windows ファイアウォールがこのアプリの一部の機能をブロックします。](images/debuglab-image-firewall-dialog-box.png)
 

**&lt;ホスト システムで**

1. ホスト コンピューターで、管理者としてコマンド プロンプト ウィンドウを開きます。 WinDbg.exe ディレクトリに移動します。 Windows キットの一部としてインストールされた Windows Driver Kit (WDK) に含まれる WinDbg.exe の x64 バージョンを使います。

```console
C:\> Cd C:\Program Files (x86)\Windows Kits\10\Debuggers\x64 
```

2. 次のコマンドを使用してデバッグするリモート ユーザーに、WinDbg を起動します。 キーとポートの値に一致したターゲットの BCDEdit を使用して設定。

```console
C:\> WinDbg –k net:port=50010,key=2steg4fzbj2sz.23418vzkd4ko3.1g34ou07z4pev.1sp3yo9yz874p
```

**-&gt;ターゲット システム**

ターゲット システムを再起動します。

**&lt;ホスト システムで**

1 分または 2 では、ホスト システムで、デバッグ出力が表示されます。

![windows は、カーネルのライブ接続からのコマンド ウィンドウ出力の表示のデバッガーします。](images/debuglab-image-winddbg-hh.png)

デバッガー コマンド ウィンドウは、WinDbg で主にデバッグ情報ウィンドウです。 デバッガー コマンドを入力し、このウィンドウで、コマンドの出力を表示できます。

デバッガー コマンド ウィンドウは、2 つのペインに分割されます。 ウィンドウの下部にある小さいウィンドウ (コマンドのエントリのウィンドウ) でのコマンドを入力し、ウィンドウの上部にある大きいウィンドウで、コマンドの出力を表示します。

コマンドのエントリ ウィンドウで上向きの矢印と下向きコマンド履歴をスクロールする方向キー。 コマンドが表示されたら、それを編集またはキーを押して**ENTER**コマンドを実行します。

## <a name="span-idkernelmodedebuggingcommandsandtechniquesspansection-2-kernel-mode-debugging-commands-and-techniques"></a><span id="kernelmodedebuggingcommandsandtechniques"></span>セクション 2: カーネル モードのデバッグ コマンドや技法


*セクション 2 では、ターゲット システムに関する情報を表示するのにデバッグ コマンドを使用します。*

**&lt;ホスト システムで**

**.Prefer とデバッガーのマークアップ言語 (DML) を有効にする\_dml**

いくつかは、すばやく情報を収集するでクリックできるデバッガー マークアップ言語を使用してコマンドの表示テキストをデバッグします。

1. WinDBg で Ctrl + Break (Scroll Lock) を使用して、ターゲット システムで実行されているコードを中断します。 少しのターゲット システムが応答する時間がかかる場合があります。
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

**注**  が省略されている出力は、"... で示されます。 "このラボで。

 

まだ読み込まれているシンボルとシンボルのパスを設定するがある、あるので限定された情報は、デバッガーで使用できます。

## <a name="span-iddownloadspansection-3-download-and-build-the-sysvad-audio-driver"></a><span id="download"></span>セクション 3:ダウンロードして Sysvad オーディオ ドライバーのビルド


*セクション 3 では、ダウンロードし、Sysvad オーディオ ドライバーをビルドします。*

通常は操作することで独自のドライバー コード WinDbg を使用する場合。 オーディオ ドライバーのデバッグについて理解しておく Sysvad 仮想オーディオ サンプル ドライバーが使用されます。 このサンプルは、ネイティブのカーネル モード コードをステップ実行の単一方法を説明するために使用されます。 この手法を非常に複雑なカーネル モード コードの問題のデバッグで役に立つことができます。

をダウンロードして Sysvad サンプル オーディオ ドライバーをビルドするには、次の手順を実行します。

1.  **ダウンロードして、GitHub から Sysvad オーディオ サンプルを抽出**

    Sysvad サンプルとここで、Readme.md ファイルを表示するのにブラウザーを使用することができます。

    [https://github.com/Microsoft/Windows-driver-samples/tree/master/audio/sysvad](https://github.com/Microsoft/Windows-driver-samples/blob/97cf5197cf5b882b2c689d8dc2b555f2edf8f418/general/echo/kmdf/ReadMe.md)

    ![github リポジトリの 全般 フォルダーとダウンロードの zip ボタン](images/sysvad-lab-github.png)

    このラボでは、ユニバーサル ドライバー サンプルは、1 つの zip ファイルをダウンロードする方法を示します。

    a. Master.zip ファイルをローカル ハード ドライブにダウンロードします。

    <https://github.com/Microsoft/Windows-driver-samples/archive/master.zip>

    b. 右クリックして*Windows ドライバーのサンプル-master.zip*、選択**すべて展開**します。 新しいフォルダーを指定するか、抽出したファイルを保存する既存のサブスクリプションへの参照します。 たとえば、指定する*c:\\WDK\_サンプル\\* として新しいファイルが抽出先フォルダーです。

    c. ファイルが抽出されると、次のサブフォルダーに移動します。

    *C:\\WDK\_サンプル\\Sysvad*

2.  **Visual Studio でのドライバー ソリューションを開く**

    Visual Studio で、次のようにクリックします**ファイル** &gt; **オープン** &gt; **プロジェクト/ソリューション.。** を抽出したファイルを含むフォルダーに移動します (たとえば、 *c:\\WDK\_サンプル\\Sysvad*)。 ダブルクリックして、 *Syvad*ソリューション ファイル。

    Visual Studio では、ソリューション エクスプ ローラーを見つけます。 (これがまだ開いていない場合は、選択**ソリューション エクスプ ローラー**から、**ビュー**メニュー)。ソリューション エクスプ ローラーでは、さまざまなプロジェクトとサンプルの変更に時間の経過に含まれるものを含む 1 つのソリューションを確認できます。 
        
    ![visual studio と sysvad プロジェクトから読み込まれた device.c ファイル](images/sysvad-lab-visual-studio-solution.png)

3.  **サンプルの構成とプラットフォームを設定します。**

    ソリューション エクスプ ローラーで右クリックして**ソリューション 'sysvad' (7 プロジェクト)** 、選択**Configuration Manager**します。 構成とプラットフォームの設定は、4 つのプロジェクトの同じことを確認します。 既定では、構成が"Win10 Debug"に設定し、プラットフォームのすべてのプロジェクトの"Win64"に設定されています。 任意の構成または 1 つのプロジェクトのプラットフォームの変更を加えた場合は、残りの 3 つのプロジェクトに対しても同じ変更を行う必要があります。

    **注**  このラボでは、64 ビット Windows が使用されている前提としています。 32 ビット Windows を使用している場合は、32 ビットのドライバーをビルドします。

     

4.  **ドライバーの署名を確認します。**

    TabletAudioSample を見つけます。 Sysvad ドライバーのプロパティ ページを開き、確認**ドライバーの署名** &gt; **記号モード**に設定されている*テスト サインオン*します。

5.  **Visual Studio を使用してサンプルをビルドします。**

    Visual Studio で、次のようにクリックします。**ビルド** &gt; **ソリューションのビルド**します。

    ビルドの windows では、6 つすべてのプロジェクトのビルドが成功したことを示すメッセージを表示する必要があります。

6.  **組み込みのドライバー ファイルを見つけます**

    ファイル エクスプ ローラーでは、サンプルの抽出されたファイルを含むフォルダーに移動します。 移動するなど、 *c:\\WDK\_サンプル\\Sysvad*前に指定したフォルダーがある場合、します。 コンパイル済みのドライバー ファイルの場所がで選択した構成とプラットフォームの設定によって異なります、そのフォルダー内、 **Configuration Manager**します。 など、既定の設定のままの場合、コンパイル済みのドライバー ファイルに保存という名前のフォルダー  *\\x64\\デバッグ*64 ビットのビルドをデバッグします。

    TabletAudioSample ドライバーのビルド済みのファイルを含むフォルダーに移動します。

    *C:\\WDK\_サンプル\\Sysvad\\TabletAudioSample\\x64\\デバッグ*します。 フォルダー、TabletAudioSample が含まれます。Sys、シンボル ファイルの pdp および inf ファイル。 SwapAPO を検索する必要がありますと KeywordDetectorContosoAdapter dll とシンボル ファイル。

    ドライバーをインストールするには、次のファイルが必要です。

    |                                   |                                                                                   |
    |-----------------------------------|-----------------------------------------------------------------------------------|
    | TabletAudioSample.sys             | ドライバー ファイルです。                                                                  |
    | TabletAudioSample.pdb             | ドライバーのシンボル ファイル。                                                           |
    | tabletaudiosample.inf             | ドライバーをインストールするために必要な情報が含まれる情報 (INF) ファイル。 |
    | KeywordDetectorContosoAdapter.dl  | サンプルのキーワード ディテクターです。                                                        |
    | KeywordDetectorContosoAdapter.pdb | キーワードの検出機能をサンプル シンボル ファイルです。                                          |
    | lSwapAPO.dll                      | パスワードを管理するための UI 用のサンプル ドライバー拡張します。                                |
    | lSwapAPO.pdb                      | APO UI シンボル ファイル。                                                           |
    | TabletAudioSample.cer             | TabletAudioSample 証明書ファイル。                                           |

     

7.  USB ドライブを検索またはホストから、ターゲット システムに組み込みのドライバー ファイルをコピーするネットワーク共有を設定します。

次のセクションはターゲット システムにコードをコピーおよびしインストール ドライバーをテストします。

## <a name="span-idinstallspansection-4-install-the-sysvad-audio-driver-sample-on-the-target-system"></a><span id="install"></span>セクション 4:ターゲット システム上の Sysvad オーディオ ドライバーのサンプルをインストールします。


*セクション 4 では、devcon を使用して、Sysvad オーディオ ドライバーをインストールします。*

**-&gt; ターゲット システム**

ドライバーをインストールするコンピューターと呼ばれる、*ターゲット コンピューター*または*テスト コンピューター*します。 通常、これを開発およびドライバー パッケージをビルド コンピューターから別のコンピューターです。 開発およびドライバーをビルドする場所のコンピューターと呼ばれる、*ホスト コンピューター*します。

ターゲット コンピューターに移行してドライバー パッケージ、ドライバーをインストールするプロセスと呼ばれます*展開*ドライバー。 Sysvad ドライバーのサンプルは、自動または手動で展開できます。

ドライバーを手動で展開する前に、テスト署名を有効にして、ターゲット コンピューターを準備する必要があります。 また、DevCon ツールを WDK のインストールで検索する必要があります。 その後、ターゲット システムでビルドされたドライバー サンプルを実行する準備ができました。

ターゲット システム上のドライバーをインストールするには、次の手順を実行します。

1.  **テストを有効にする署名されたドライバー**

    テストを実行する機能を有効にするには、署名されたドライバー。

    1. Windows の設定を開きます。

    2. **更新とセキュリティ**、 **Recovery**します。

    3. [**スタートアップを高度な**、] をクリックして**今すぐ再起動**します。

    4. PC が再起動したら、選択**トラブルシューティング**します。

    5. 選択し、**詳細オプション**、**スタートアップ設定**順にクリックします**再起動**します。

    6. キーを押してドライバー署名の強制を無効にするを選択して、 **F7**キー。

    7. PC は、場所に新しい値で開始されます。

2.  **&lt;ホスト システムで**

    WDK のインストールの Tools フォルダーに移動し、DevCon ツールを見つけます。 たとえば、次のフォルダーを探します。

    *C:\\Program Files (x86)\\Windows Kits\\10\\Tools\\x64\\devcon.exe*

3.  **-&gt; ターゲット システム**

    **ドライバーをインストールします。**

    次の手順では、インストールして、ドライバーのサンプルをテストする方法を示します。

    このドライバーのインストールに必要な INF ファイル*TabletAudioSample.inf*します。 ターゲット コンピューターで、管理者としてコマンド プロンプト ウィンドウを開きます。 ドライバー パッケージ フォルダーに移動、TabletAudioSample.inf ファイルを右クリックし **インストール**します。

    ダイアログ ボックスには、テスト ドライバーが署名されていないドライバーであることが示されます。 **[かまわず続行]** をクリックして続行します。

    ![windows セキュリティの警告 - windows は、発行元を確認できません](images/debuglab-image-install-security-warning.png)

    >[!TIP]
    > インストールで問題が発生した場合は、詳細については、次のファイルを確認します。
    `%windir%\inf\setupapi.dev.log`
    >
     
    詳細な手順についてを参照してください。[ドライバーの展開、テスト、およびデバッグ用コンピューターの構成](https://docs.microsoft.com/windows-hardware/drivers/gettingstarted/provision-a-target-computer-wdk-8-1)します。

    INF ファイルにはインストールするためのハードウェア ID が含まれています、 *tabletaudiosample.sys*します。 Syvad サンプルでは、ハードウェア ID は次のとおりです。 `root\sysvad_TabletAudioSample`

    ターゲット コンピューターで、管理者としてコマンド プロンプト ウィンドウを開きます。 ドライバー パッケージ フォルダーに移動し、次のコマンドを入力します。 `devcon status root\sysvad_TabletAudioSample`
       
    ステータス情報は、表示の中に、devcon をインストールします。


4.  **デバイス マネージャーでのドライバーを確認します。**

    コマンド プロンプト ウィンドウで、対象のコンピューターに次のように入力します。 **devmgmt**デバイス マネージャを開きます。 デバイス マネージャーで、[表示] メニュー選択**デバイスの種類によって**します。

    デバイス ツリーで探します*仮想オーディオ デバイス (WDM) - タブレット サンプル*オーディオ デバイス ノードにします。 これは通常下、**サウンド、ビデオ、およびゲーム コント ローラー**ノード。 インストールされ、アクティブであることを確認します。

    PC デバイス マネージャーでの実際のハードウェアのドライバーを強調表示します。 ドライバーを右クリックし、[ドライバーの無効化を無効にする] をクリックします。

    オーディオ ハードウェア ドライバーがデバイス マネージャーでの確認が表示されますは無効になっていることを示す下向きの矢印。

    ![デバイス マネージャーのツリーで強調表示されているオーディオ デバイスを仮想タブレットのサンプル](images/sysvad-lab-audio-device-manager.png)

    ドライバーのサンプルを正常にインストールした後で、テストする準備ができましたがようになりました。

**Sysvad オーディオ ドライバーをテストします。**

1. コマンド プロンプト ウィンドウで、対象のコンピューターに次のように入力します。 **devmgmt**デバイス マネージャを開きます。 デバイス マネージャーで、上、**ビュー**メニューの **デバイスの種類によって**します。 デバイス ツリーで探します*仮想オーディオ デバイス (WDM) - タブレット サンプル*します。

2. コントロール パネルを開きに移動します**ハードウェアとサウンド** &gt; **オーディオ デバイスを管理する**します。 [サウンド] ダイアログ ボックスには、ラベルが付いてスピーカー アイコンを選択します。*仮想オーディオ デバイス (WDM) - タブレット サンプル*、順にクリックします**Set Default**、クリックはしないで **[ok]** します。 これは、[サウンド] ダイアログ ボックスを開いたままです。
3. MP3 または対象のコンピューター上の他のオーディオ ファイルを見つけてダブルクリックを再生します。 [サウンド] ダイアログ ボックスであることを確認アクティビティに関連付けられているボリューム レベルのインジケーターで、*仮想オーディオ デバイス (WDM) - タブレット サンプル*ドライバー。

## <a name="span-idusewindbgtodisplayinformationspansection-5-use-windbg-to-display-information-about-the-driver"></a><span id="usewindbgtodisplayinformation"></span>セクション 5:WinDbg を使用して、ドライバーに関する情報を表示するには


*セクション 5 では、シンボル パスを設定し、カーネル デバッガー コマンドを使用して、Sysvad サンプル ドライバーに関する情報を表示します。*

可能性のある重要なデバッグするときに、変数名などの追加情報を表示する WinDbg の記号を許可します。 WinDbg は Microsoft Visual Studio では、ソース レベルのデバッグのシンボルの書式をデバッグします。 任意のシンボルまたは変数 PDB シンボル ファイルを持つモジュールからアクセスできます。

デバッガーを読み込むには、次の手順を実行します。

**&lt;ホスト システムで**

1.  デバッガーが閉じている場合は、もう一度、管理者コマンド プロンプト ウィンドウで、次のコマンドを使用してを開きます。 構成したものでは、キーとポートを置き換えます。

    ```console
    C:\> WinDbg –k net:port=50010,key=2steg4fzbj2sz.23418vzkd4ko3.1g34ou07z4pev.1sp3yo9yz874p
    ```

2.  Ctrl + Break (Scroll Lock) を使用して、ターゲット システムで実行されているコードを中断します。

**シンボル パスを設定します。**

1.  WinDbg の環境で Microsoft シンボル サーバーにシンボル パスを設定するには、使用、 **.symfix**コマンド。

    ```dbgcmd
    0: kd> .symfix
    ```

2.  ローカル シンボルを使用する、ローカル シンボルの場所を追加する追加のパスを使用して、 **.sympath +** し **.reload/f**します。

    ```dbgcmd
    0: kd> .sympath+ C:\WDK_Samples\Sysvad
    0: kd> .reload /f
    ```

    **注**  、 **.reload**コマンドと、 **/f** force オプションが指定したモジュールのすべてのシンボル情報を削除し、シンボルを再読み込みします。 場合によっては、このコマンドも再読み込みまたはモジュール自体がアンロードされます。

     

**注**  WinDbg を提供する高度な機能を使用する適切なシンボルを読み込む必要があります。 シンボルが正しく構成されていない場合、シンボルに依存する機能を使用しようとしたときに、シンボルが使用できないことを示すメッセージが届きます。

```dbgcmd
0:000> dv
Unable to enumerate locals, HRESULT 0x80004005
Private symbols (symbols.pri) are required for locals.
Type “.hh dbgerr005” for details.
```

 

**注**  
**シンボル サーバー**

シンボルを使用するために使用する方法を数多くあります。 多くの状況では、必要なときに、Microsoft が提供するシンボル サーバーからアクセス シンボルに PC を構成できます。 このチュートリアルでは、このアプローチを使用することを前提としています。 環境内でシンボルが別の場所にいる場合は、その場所を使用する手順を変更します。 詳細については、次を参照してください。[シンボル ストアとシンボル サーバー](symbol-stores-and-symbol-servers.md)します。

 

**注**  
**ソース コードのシンボルの要件を理解します。**

ソースのデバッグを実行するには、バイナリのチェック (デバッグ) バージョンをビルドする必要があります。 コンパイラでは、シンボル ファイル (.pdb ファイル) を作成します。 これらのシンボル ファイルは、バイナリの命令がソース行に対応させる方法をデバッガーに表示されます。 実際のソース ファイル自体も、デバッガーにアクセスできる必要があります。

シンボル ファイルでは、ソース コードのテキストは含まれません。 デバッグをお勧め、リンカーは、コードを最適化していない場合。 ソースのデバッグとローカル変数へのアクセスより難しくなると、コードが最適化されている場合もほぼ不可能です。 でローカル変数またはソース行の表示に関する問題が発生する場合は、次のビルド オプションを設定します。

COMPILE_DEBUG 設定 = 1

ENABLE_OPTIMIZER 設定 = 0

 

1.  Sysvad ドライバーに関する情報を表示するデバッガーの [コマンド] 領域で、次を入力します。

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

    詳細については、次を参照してください。 [ **lm**](lm--list-loaded-modules-.md)します。

2.  をクリックして、**グローバル シンボルのすべての参照**デバッグ、文字で始まる項目シンボルに関する情報を表示する出力のリンクをします。
3.  DML が有効になっているため、出力の一部の要素をクリックして、ホット リンクです。 をクリックして、*データ*デバッグ、文字で始まる項目シンボルに関する情報を表示する出力のリンクをします。

    ```dbgcmd
    0: kd> x /D /f tabletaudiosample!a*
     A B C D E F G H I J K L M N O P Q R S T U V W X Y Z

    fffff806`9adb1000 tabletaudiosample!AddDevice (struct _DRIVER_OBJECT *, struct _DEVICE_OBJECT *)
    ```

    詳しくは、次を参照してください。 [ **(シンボルを調べる) x**](x--examine-symbols-.md)します。

4.  **! Lmi**拡張機能には、モジュールに関する情報が表示されます。 型 **! lmi tabletaudiosample**します。 出力は、下に表示されるテキストのようになります。

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

5.  使用して、 **! dh**拡張機能を次に示すようにヘッダー情報を表示します。

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

## <a name="span-iddisplayingtheplugandplaydevicetreespansection-6-displaying-plug-and-play-device-tree-information"></a><span id="displayingtheplugandplaydevicetree"></span>セクション 6:プラグ アンド プレイ デバイス ツリーの情報を表示します。


*セクション 6 では、プラグ アンド プレイ デバイス ツリーに存在する場所と Sysvad サンプルのデバイス ドライバーに関する情報が表示されます。*

プラグ アンド プレイ デバイス ツリーで、デバイス ドライバーに関する情報は、トラブルシューティングに役立ちます。 たとえば、デバイス ドライバーが、デバイス ツリーに常駐していない場合はデバイス ドライバーのインストールの問題。

デバイス ノードのデバッグ拡張機能の詳細については、次を参照してください。 [ **! devnode**](-devnode.md)します。

**&lt;ホスト システムで**

1. プラグ アンド プレイ デバイス ツリー内のすべてのデバイス ノードを表示するには、入力、 **! devnode 0 1**コマンド。 このコマンドを実行する 2 分かかることができます。 この期間中、"\*ビジー"WinDbg の [状態] 領域に表示されます。

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

2. Ctrl キーを押しながら F キーを使用して、デバイス ドライバーの名前を探すように生成される出力で検索する*sysvad*します。

   ![検索対象の用語 sysvad を表示するダイアログ ボックスを検索します。](images/sysvad-lab-audio-find-dialog.png)

   デバイス ノード エントリの名前を持つ`sysvad_TabletAudioSample`に表示されます、! Syvad の devnode 出力します。

   ```dbgcmd
     DevNode 0xffffe00086e68190 for PDO 0xffffe00089c575a0
       InstancePath is "ROOT\sysvad_TabletAudioSample\0000"
       ServiceName is "sysvad_tabletaudiosample"
       State = DeviceNodeStarted (0x308)
   ...
   ```

   PDO のアドレスと DevNode アドレスが表示されることに注意してください。

3. 使用して、 `!devnode 0 1 sysvad_TabletAudioSample` Sysvad デバイス ドライバに関連付けられているプラグ アンド プレイの情報を表示するコマンド。

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

4. PDO ドライバーの実行中のインスタンスに関連付けられているが、前のコマンドに表示される出力に含まれています、この例では*0xffffe00089c575a0*します。 入力、 **! devobj**<em>&lt;PDO アドレス&gt;</em> Sysvad デバイス ドライバに関連付けられているプラグ アンド プレイの情報を表示するコマンド。 されるアドレスを使用して、PDO **! devnode** PC では、ここで示すように 1 つない上を表示します。

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

5. 出力が表示される、 **! devobj**コマンドに接続しているデバイスの名前が含まれています。\\ドライバー\\sysvad\_tabletaudiosample します。 使用して、 **! drvobj**コマンドを 2 に、接続しているデバイスに関連付けられている情報を表示するビット マスク。

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

6. 入力、 **! devstack**<em>&lt;PDO アドレス&gt;</em>デバイス ドライバに関連付けられているプラグ アンド プレイの情報を表示するコマンド。 出力が表示される、 **! devnode 0 1**コマンドには、ドライバーの実行中のインスタンスに関連付けられている PDO アドレスが含まれています。 この例では*0xffffe00089c575a0*します。 されるアドレスを使用して、PDO **! devnode** PC のない、次のように表示されます。

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

出力は、シンプルな farily デバイスのドライバー スタックがあることを示しています。 Sysvad\_TabletAudioSample ドライバー PnPManager ノードの子であります。 PnPManager は、ルート ノードです。

この図より複雑なデバイス ノード ツリーを示しています。

![約 20 のノードを持つデバイス ノード ツリー](images/debuglab-image-device-node-tree.png)

**注**  より複雑なドライバー スタックの詳細については、次を参照してください。[ドライバー スタック](https://docs.microsoft.com/windows-hardware/drivers/gettingstarted/driver-stacks)と[デバイス ノードとデバイス スタック](https://docs.microsoft.com/windows-hardware/drivers/gettingstarted/device-nodes-and-device-stacks)します。

 

## <a name="span-idworkingwithbreakpointsspansection-7-working-with-breakpoints"></a><span id="workingwithbreakpoints"></span>セクション 7:ブレークポイントの操作


*セクション 7 では、特定の時点でコードが実行を停止するブレークポイントで機能します。*

**コマンドを使用してブレークポイントの設定**

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

 

1.  WinDbg UI を使用していることを確認**デバッグ** &gt; **ソース モード**WinDbg の現在のセッションで有効にします。

2.  ソース パスをローカルのコードの場所を追加するには、次のコマンドを入力します。

    ```dbgcmd
    .sympath+ C:\WDK_Samples\Sysvad
    ```

3.  シンボル パスに、ローカル シンボルの場所を追加するには、次のコマンドを入力します。

    ```dbgcmd
    .sympath+ C:\WDK_Samples\Sysvad
    ```

4.  **デバッグのマスクを設定します。**

    ドライバーを使用して操作するときは、すべてが表示されるメッセージの表示に便利ですができます。 すべてのデバッグ対象システムからメッセージを既定のデバッグのビット マスクを変更するには、次に表示される、デバッガーの種類。

    ```dbgcmd
    0: kd> ed nt!Kd_DEFAULT_MASK 0xFFFFFFFF
    ```

5.  ブレークポイントを設定、 **bm**ブレークポイントを設定する関数名 (AddDevice) を続けて、ドライバーの名前を使用して、コマンドは、感嘆符で区切られました。

    ```dbgcmd
    0: kd> bm tabletaudiosample!AddDevice
    breakpoint 1 redefined
      1: fffff801`14b5f000 @!"tabletaudiosample!AddDevice"
    ```

    別の構文を使用するにはのような変数の設定と組み合わせて&lt;モジュール&gt;!&lt;シンボル&gt;、&lt;クラス&gt;::&lt;メソッド&gt;、'&lt;file.cpp&gt;:&lt;行番号&gt;'、または時間数をスキップ&lt;条件&gt; &lt; \#&gt;します。 詳細については、次を参照してください。[を使用してブレークポイント](using-breakpoints.md)します。

6.  」と入力して、ブレークポイントが設定されたことを確認する現在のブレークポイントを一覧表示、 **bl**コマンド。

    ```dbgcmd
    0: kd> bl
    1 e fffff801`14b5f000     0001 (0001) tabletaudiosample!AddDevice
    ```

7.  移動コマンドを入力して、ターゲット システムでコードが実行を再開**g**します。

8.  **-&gt;ターゲット システム**

    、Windows でアイコンを使用するか入力してにデバイス マネージャーを開く**mmc devmgmt.msc**します。 **デバイス マネージャー**展開、**サウンド、ビデオ、およびゲーム コント ローラー**ノード。 仮想のオーディオ ドライバー エントリを右クリックし、選択**を無効にする** メニューから。

9.  仮想のオーディオ ドライバー エントリを再び右クリックし、選択**を有効にする** メニューから。
10. **&lt;ホスト システムで**

    これが原因で、Windows AddDevice を呼び出すと、ドライバーを再読み込みする必要があります。 これにより、起動する AddDevice デバッグ ブレークポイントとターゲット システム上のドライバー コードの実行を停止する必要があります。

    ```dbgcmd
    Breakpoint 1 hit
    tabletaudiosample!AddDevice:
    fffff801`14baf000 4889542410      mov     qword ptr [rsp+10h],rdx
    ```

    ソース パスが正しく設定されている場合、adapter.cpp で AddDevice ルーチンで停止する必要があります。

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

11. 」と入力して、コードをステップ 1 行ずつ、 **p**コマンドまたは F10 キーを押しています。 ステップ インできますフォワード sysvad AddDevice コード外 PpvUtilCall、PnpCallAddDevice し PipCallDriverAddDevice Windows コード。 番号を指定することができます、 **p**コマンドを複数の行がたとえばステップ前進*p 5*します。

12. 完了したら、go コマンドを使用して、コードのステップ**g**ターゲット システムでの実行を再起動します。

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

 

特定の時点、4 つのデータ ブレークポイントを設定することができますのみで、データを正しく配置すること、または、ブレークポイントをトリガーしないかどうかを確認するかどうかは (単語が 2 で割り切れるアドレスで終了する必要があります、dword が 4 で割り切れる必要があります、および 0 または 8 では、(クワドワード)。)

たとえば、特定のメモリ アドレスの読み取り/書き込みのブレークポイントを設定するには、このようなコマンドを使用します。

```dbgcmd
ba r 4 fffff800`7bc9eff0
```

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

 

クリックしてブレークポイントも変更する代わりに、**編集** &gt; **ブレークポイント**します。 ブレークポイントの ダイアログ ボックスが既存のブレークポイントでのみ動作することに注意してください。 コマンドラインからは、新しいブレークポイントを設定する必要があります。

**MixerVolume にブレークポイントを設定します。**

オーディオ ドライバー コードのさまざまな部分は、デバイス ドライバーが読み込まれた後、さまざまなイベントに応答すると呼ばれます。 次のセクションでは、ユーザーが仮想ドライバーでオーディオの音量を調整するときにも発生するブレークポイントを設定します。

MixerVolume でブレークポイントを設定するには、次の手順を実行します。

1.  **&lt;ホスト システムで**

    ボリュームを変更するメソッドを検索するのにには、文字列のボリュームが含まれている CAdapterCommon、内のシンボルを一覧表示するのに x コマンドを使用します。

    ```dbgcmd
    kd> x tabletaudiosample!CAdapterCommon::*
    ...
    fffff800`7bce26a0 tabletaudiosample!CAdapterCommon::MixerVolumeWrite (unsigned long, unsigned long, long)
    …
    ```

    CTRL キーを押しながら F キーを使用して、ボリュームの出力で上へ検索を MixerVolumeWrite メソッドを検索します。

2.  ビジネス継続性を使用して前のブレークポイントをクリア\*します。
3.  次のコマンドを使用して、CAdapterCommon::MixerVolumeWrite ルーチンには、シンボル ブレークポイントを設定します。

    ```dbgcmd
    kd> bm tabletaudiosample!CAdapterCommon::MixerVolumeWrite
      1: fffff801`177b26a0 @!"tabletaudiosample!CAdapterCommon::MixerVolumeWrite"
    ```

4.  ブレークポイントが正しく設定されていることを確認するブレークポイントの一覧を表示します。

    ```dbgcmd
    kd> bl
    1 e fffff801`177b26a0 [c:\WDK_Samples\audio\sysvad\common.cpp @ 1668]    0001 (0001) tabletaudiosample!CAdapterCommon::MixerVolumeWrite
    ```

5.  移動コマンドを入力して、ターゲット システムでコードが実行を再開**g**します。

6.  コントロール パネルの選択で**ハードウェアとサウンド** &gt;**サウンド**します。 右クリックして**シンクの説明のサンプル**選択**プロパティ**します。 選択、**レベル**タブ。スライダーの音量を調整します。

7.  させる SetMixerVolume デバッグ ブレークポイントが発生する必要があり、ターゲット システム上のドライバー コードの実行を停止する必要があります。

    ```dbgcmd
    kd> g
    Breakpoint 1 hit
    tabletaudiosample!CAdapterCommon::MixerVolumeWrite:
    fffff801`177b26a0 44894c2420      mov     dword ptr [rsp+20h],r9d
    ```

    Common.cpp でこの行で停止する必要があります。

    ```dbgcmd
    {
        if (m_pHW)
        {
            m_pHW->SetMixerVolume(Index, Channel, Value);
        }
    } // MixerVolumeWrite
    ```

8.  現在の変数とその値を表示するのにには、dv コマンドを使用します。 変数の詳細については、このラボの次のセクションで提供されます。

    ```dbgcmd
    2: kd> dv
               this = 0x00000000`00000010
             ulNode = 0x344
          ulChannel = 0x210a45f8
            lVolume = 0n24
    ```

9.  キーを押して**F10**コードを 1 つのステップ実行します。

10. キーを押して**F5** MixerVolumeWrite コードの実行を完了します。

**概要 - デバッガー コマンド ウィンドウからコードをステップ実行**

次に使用できるコマンドを (かっこ内に表示する関連付けられたキーボード短いカット) 使用してコードをステップ実行します。

-   (Ctrl + Break) で中断 - このコマンドは、システムが実行されていて、WinDbg (カーネル デバッガーで、シーケンスは Ctrl + C) との通信に限り、システムが中断します。

-   ステップ オーバー (F10): このコマンドは 1 つのステートメントや、一度に 1 つの命令を進めるコードが実行を実行します。 呼び出しが発生した場合はコードが実行は呼び出し経由で呼び出されたルーチンを入力しなくても渡します。 (場合、プログラミング言語は C または C++ と、WinDbg は元のモードでは、ソース モード有効にできますオンまたはオフを使用して**デバッグ**&gt;**ソース モード**)。

-   ステップ イン (F11) – する点を除いて、呼び出しの実行が呼び出されたルーチンに移動し、ステップ オーバーのようにこのコマンドは、します。

-   ステップ アウト (shift + f11): このコマンドの実行を実行して、現在の終了を実行するルーチン (呼び出し履歴内の現在の場所)。 これは、十分なルーチンを見た場合に便利です。

-   (F7 キーまたは Ctrl + F10)、カーソル位置まで実行 – を解除し、; f7 キーを押して実行する変換元または [逆アセンブル] ウィンドウにカーソルを置きますコードの実行は、そのポイントまで実行されます。 コードの実行フローが、カーソルによって示されるポイントに到達しない場合 (たとえば、IF ステートメントを実行されない場合は)、コードの実行が、指定されたポイントに届いていませんので、WinDbg は中断されませんが。

-   ブレークポイントが発生したか、バグ チェックのようなイベントが発生するまで実行 (F5) – を実行します。

**詳細オプション**

-   命令を設定するコードの実行がその時点から開始されます (たとえば、f5 キーまたは f10 キーを使用して) 続行できるようになりますし、ソース ウィンドウで現在の行 (Ctrl + Shift + I) –、行にカーソルを置いて、このショートカット キーを入力します。 これは、機能は、シーケンスを再実行したい、注意が必要ですが便利です。 たとえば、レジスタと変数に設定されていないものになるコードが実行がその行を自然連絡いたしましたかどうか。

-   直接設定--eip レジスタのすることができます値を格納する、eip レジスタにし、f5 キーを押すとすぐに (または F10、f11 キーなど)、そのアドレスから実行を開始します。 これは、機能は、アセンブリ命令のアドレスを指定することを除いてカーソル指定されている現在の行に命令を設定に似ています。

簡単に、コマンドラインからではなく、ui の手順にのでこの方法はお勧めです。 かどうか、必要に応じて、次のコマンドを使用できます、コマンドラインでソース ファイルをステップ実行します。

-   .lines - ソース行情報の有効化します。

-   bp メイン - は、モジュールの先頭に最初のブレークポイントを設定します。

-   l + t - ステップ実行、ソース行によって行われます。

-   選択**デバッグ**&gt;**ソース モード**; ソースのモードに切り替わる、`L+t`コマンドでは不十分です。

-   l + s - ソースのプロンプトで行が表示されます。

-   g -"main"が入力されるまでプログラムを実行します。

-   p-1 つのソース行を実行します。

詳細については、次を参照してください。 [WinDbg でソース コードをデバッグ](source-window.md)デバッグ リファレンス ドキュメント。

**コードにブレークポイントを設定**

コードでブレークポイントを設定するには追加することで、`DebugBreak()`ステートメントは、プロジェクトを再構築とドライバーを再インストールします。 実稼働コードではなく、初期開発段階で使用するための手法をこのブレークポイントは、ドライバーを有効にすると、毎回を起動します。 この手法は動的に、ブレークポイントのコマンドを使用してブレークポイントを設定するほどの柔軟性はありません。

ヒント:ブレークポイントをさらにラボ作業の追加を Sysvad ドライバーのコピーを保持したい場合があります。

1.  AddDevice メソッドを追加することで実行するたびに発生するブレークポイントを設定、`DebugBreak()`をサンプル コードのステートメント。

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

2.  すべての Microsoft Visual Studio でのドライバーを再構築し、再ターゲット マシンにインストールする前に説明した手順に従います。 更新されたドライバをインストールする前に、既存のドライバーをアンインストールしてください。
3.  前のブレークポイントをクリアし、デバッガーが対象の PC に接続されているかどうかを確認します。

4.  コードが実行されに達すると、`DebugBreak`ステートメントでは、実行が停止し、メッセージが表示されます。

    ```dbgcmd
    KERNELBASE!DebugBreak:
    77b3b770 defe     __debugbreak
    ```

## <a name="span-idlookingatvariablesspanspan-idlookingatvariablesspanspan-idlookingatvariablesspansection-8-display-variables"></a><span id="LookingAtVariables"></span><span id="lookingatvariables"></span><span id="LOOKINGATVARIABLES"></span>セクション 8:変数を表示します。


*セクション 8 では、変数を表示するのにデバッガー コマンドを使用します。*

コードが期待どおりに動作していることを確認するコードの実行時に変数を確認すると便利ですができます。 このラボは、オーディオ ドライバーのサウンドを生成する変数を調べます。

1.  使用して、 **dv**コマンドを tabletaudiosample に関連付けられているロケールの変数を調べます。CMiniportWaveRT::New\*します。

    ```dbgcmd
    kd> dv tabletaudiosample!CMiniportWaveRT::New*
    ```

2.  前のブレークポイントをクリアします。

    ```dbgcmd
    bc *
    ```

3.  次のコマンドを使用して CMiniportWaveCyclicStreamMSVAD ルーチンにシンボル ブレークポイントを設定します。

    ```dbgcmd
    0: kd> bm tabletaudiosample!CMiniportWaveRT::NewStream
      1: fffff801`177dffc0 @!"tabletaudiosample!CMiniportWaveRT::NewStream"
    ```

4.  移動コマンドを入力して、ターゲット システムでコードが実行を再開**g**します。

5.  **-&gt; ターゲット システム**

    .Wav ファイルの拡張子で使用する Windows の通知のサウンド ファイル) などの小型メディア ファイルを見つけて、それを再生するファイルをクリックします。 たとえば、Windows にある Ring05.wav を使用することができます\\メディアのディレクトリ。

6.  **&lt;ホスト システムで**

    メディア ファイルを再生すると、ブレークポイントが発生する必要があり、ターゲット システム上のドライバー コードの実行を停止する必要があります。

    ```dbgcmd
    Breakpoint 1 hit
    tabletaudiosample!CMiniportWaveRT::NewStream:
    fffff801`177dffc0 44894c2420      mov     dword ptr [rsp+20h],r9d
    ```

    ソース コード ウィンドウには、NewStream 関数の入り口で中かっこが強調表示する必要があります。

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

    名前と特定のフレームのすべてのローカル変数の値を表示するには」と入力して、 **dv**コマンド。

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

8.  **DML を使用して、変数を表示するには**

    DML を使用して、変数の調査、下線付きの要素をクリックします。 クリック アクションのビルド、 [ **dx (表示 NatVis 式)** ](dx--display-visualizer-variables-.md)にドリル ダウンできるようにするコマンドは、データ構造を入れ子になった。

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

    グローバル変数のメモリの場所を入力して検索できます**でしょうか。&lt;変数名&gt;** します。

    ```dbgcmd
    0: kd> ? signalProcessingMode
    Evaluate expression: -52768896396472 = ffffd001`c8acd348
    ```

10. この場合、変数のメモリ位置が返されます*ffffd001\`c8acd348*します。 メモリ位置の内容を表示するにはその場所の入力の値をダンプすることによって、 **dd**コマンドの前のコマンドによって返されるメモリ位置を使用します。

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

11. 変数名を使用することも、 **dd**コマンド。

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

12. **変数を表示します。**

    使用して、**ビュー** &gt; **ローカル**ローカル変数を表示するメニュー項目。 このインターフェイスより複雑なデータ構造をドリル ダウンするには、この機能も提供します。

    ![サンプル コードのローカル変数とコマンド ウィンドウを表示する windbg](images/sysvad-lab-display-variables.png)

13. P または f10 キーを ntStatus を強調するまでは、前方の約 10 個のコード行をステップ = IsFormatSupported (暗証番号 (pin)、キャプチャ、DataFormat)。コード行。

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

14. 使用して、 **dv**コマンドの名前と特定のフレームのすべてのローカル変数の値を表示します。 想定どおり、値が異なる、このコマンドを実行する最後の時刻からローカル変数といくつかの変数は変更ではなく、現在のフレームやその値が変更されたこと追加コードが実行されているように注意してください。

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

## <a name="span-idviewingcallstacksspansection-9-view-call-stacks"></a><span id="viewingcallstacks"></span>セクション 9:呼び出し履歴の表示


*セクション 9 では、呼び出し元/呼び出されるコードを確認する呼び出し履歴を表示します。*

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

 

使用可能な呼び出し履歴を保持する場合は、クリックして**ビュー** &gt; **コール スタック**を表示します。 追加情報の表示を切り替える、ウィンドウの上部にある列をクリックします。

![windbg の呼び出し履歴 ウィンドウ](images/sysvad-lab-call-stack.png)

この出力には、ブレーク状態にサンプルのアダプター コードのデバッグ中に呼び出し履歴が表示されます。

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

さらにコードを調べるには、DML を使用できます。 00 最初のエントリをクリックすると、 [ **.frame (ローカル コンテキストの設定)** ](-frame--set-local-context-.md)コンテキストを設定するコマンドを使用し、 [ **dv (ローカル変数の表示)** ](dv--display-local-variables-.md)コマンドには、ローカル変数が表示されます。

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

## <a name="span-iddisplayingprocessesandthreadsspansection-10-display-processes-and-threads"></a><span id="displayingprocessesandthreads"></span>セクションの 10:表示のプロセスとスレッド


*セクションの 10 では、デバッガー コマンドを使用して、プロセスとスレッドを表示します。*

**プロセス**

プロセスの現在のコンテキストを変更するには、使用、.process&lt;プロセス&gt;コマンド。 次の例では、プロセスを識別し、コンテキストを切り替える方法を示します。

-   使用して、`!process`サウンドの再生に関連する現在のプロセスを表示するコマンド。

    詳細については、次を参照してください[ **! プロセス。** ](-process.md)

プロセスが audiodg.exe に関連付けられている出力を示しています。 このトピックの前のセクションで説明されているブレークポイントでまだの場合は、現在のプロセスが audiodg.exe イメージに関連付けられて場合があります。

**&lt;ホスト システムで**

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

実行されている状態でのこのプロセスに関連付けられているスレッドの 1 つであるに注意してください。 このスレッド ブレークポイントにヒットしたときに、メディア クリップの再生をサポートしていました。

使用して、 **! process 0 0**すべてのプロセスの概要情報を表示するコマンド。 コマンドの出力は、CTRL + F を使用して、audiodg.exe 画像に関連付けられたプロセスのプロセス ID を探します。 次に示す例ではプロセス ID は*ffffe001d147c840*します。

プロセス ID のレコードは、このラボに後で使用する PC で audiodg.exe に関連付けられています。 \_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_

```dbgcmd
...

PROCESS ffffe001d147c840
    SessionId: 0  Cid: 10f0    Peb: ee6cf8a000  ParentCid: 0434
    DirBase: d2122000  ObjectTable: ffffc0001f191ac0  HandleCount: <Data Not Accessible>
    Image: audiodg.exe
...
```

メディア クリップが完了するまで転送は、コードを実行するデバッガーを g を入力します。 再生します。 その後、中断、デバッガーにキーを押して Ctrl + ScrLk (Ctrl + Break) の使用、! 別のプロセスが現在実行されていることを確認するコマンドを処理します。

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

上記の出力は別のシステム プロセスの*ffffe001cd0ad040*が実行されています。 イメージの名前は、システム、いない audiodg.exe を示しています。

使用して、! audiodg.exe に関連付けられているプロセスに切り替えるにコマンドを処理します。 プロセス ID は、例では、 *ffffe001d147c840*します。 プロセス id で、先ほど記録した例では、プロセス ID に置き換えてください。

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

このコードがアクティブでないため、すべてのスレッドは待機状態、想定どおりです。

**スレッド**

表示し、スレッドを設定するコマンドは、プロセスの非常に似ています。 使用して、 [ **! スレッド**](-thread.md)スレッドを表示するコマンド。 使用[ **.thread** ](-thread--set-register-context-.md)を現在のスレッドを設定します。

詳細については、media player に関連付けられたスレッドをもう一度メディア クリップを再生します。 前のセクションで説明されているブレークポイントは、引き続き有効では、audiodg.exe のコンテキストで停止します。

使用します。 スレッドの現在のスレッドの簡単な情報を表示するには-1 0。 スレッドがアドレスでは、スレッドおよびプロセス Id、スレッド環境ブロックの終了アドレス、表示 (ある場合) の Win32 関数のアドレス スレッドは作成を実行し、スレッドのスケジューリングの状態。

```dbgcmd
0: kd> !thread -1 0
THREAD ffffe001d3a27040  Cid 10f0.17f4  Teb: 000000ee6cf9d000 Win32Thread: 0000000000000000 RUNNING on processor 0
```

実行しているスレッドに関する情報を表示するには、次のように入力します。 [ **! スレッド**](-thread.md)します。 次のような情報が表示されます。

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

K コマンドを使用すると、スレッドに関連付けられている呼び出し履歴を表示できます。

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

メディア クリップが完了するまで転送は、コードを実行するデバッガーを g を入力します。 再生します。 その後、中断、デバッガーに ctrl - ScrLk (Ctrl + break) を使用して、! スレッドのコマンドを別のスレッドが現在実行されていることを確認します。

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

イメージの名前は rundll32.exe、実際にないメディア クリップの再生に関連付けられているイメージ名です。

**注**   、現在のスレッドを設定するには、入力 .thread&lt;スレッド番号&gt;します。

スレッドとプロセスの詳細については、次を参照してください。

[スレッドとプロセス](threads-and-processes.md)

[コンテキストを変更します。](changing-contexts.md)

 

## <a name="span-idirqlregistersmemoryspansection-11-irql-registers-and-disassembly"></a><span id="irqlregistersmemory"></span>第 11 条:IRQL、レジスタ、および逆アセンブル


### <a name="span-idviewthesavedirqlspanview-the-saved-irql"></a><span id="view_the_saved_irql"></span>保存した IRQL を表示します。

*セクションの 11 では、IRQL と、regsisters の内容が表示されます。*

**&lt;ホスト システムで**

割り込み要求レベル (IRQL) を使用して、割り込み処理の優先度を管理できます。 各プロセッサには、スレッドを上げたり下げたりする IRQL 設定があります。 プロセッサの IRQL 設定以下で発生する割り込みは、マスクされ、現在の操作には影響しません。 プロセッサの IRQL 設定の上で発生した割り込みは、現在の操作よりも優先されます。 [ **! Irql** ](-irql.md)デバッガー中断が発生する前に拡張機能に、ターゲット コンピューターの現在のプロセッサの割り込み要求レベル (IRQL) が表示されます。 ときに、デバッガーでは、IRQL の変更対象のコンピューターに分割が、IRQL を効果的なデバッガー中断が保存され、によって表示される直前に! irql します。

```dbgcmd
0: kd> !irql
Debugger saved IRQL for processor 0x0 -- 2 (DISPATCH_LEVEL)
```

### <a name="span-idviewingtheregistersspanview-the-registers-and-disassembly"></a><<span id="viewingtheregisters"></span>レジスタとの逆アセンブルを表示します。

**レジスタを表示します。**

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

また、クリックして、レジスタの内容を表示できる**ビュー** &gt; **登録**します。

![windbg は約 12 レジスタが表示されたウィンドウを登録します。](images/sysvad-lab-audio-display-registers.png)

レジスタの内容の表示は、アセンブリ言語でコードが実行およびその他のシナリオでのステップするときに役立ちます。 詳細については、次を参照してください。 [ **r (レジスタ)** ](r--registers-.md)します。

レジスタの内容については、次を参照してください。 [x86 アーキテクチャ](x86-architecture.md)と[x64 アーキテクチャ](x64-architecture.md)します。

**逆アセンブリ**

[実行] をクリックして実行されているアセンブリ言語のコードを表示するのには、コードを分解する**ビュー** &gt; **逆アセンブル**します。

![windbg の逆アセンブル ウィンドウ](images/sysvad-lab-audio-disassembly-window.png)

アセンブリ言語の逆アセンブリの詳細については、次を参照してください。 [x86 注釈付き逆アセンブリ](annotated-x86-disassembly.md)と[x64 注釈付き逆アセンブリ](annotated-x64-disassembly.md)します。

## <a name="span-idworkingwithmemoryspansection-12-work-with-memory"></a><span id="workingwithmemory"></span>セクション 12:メモリを使用します。


*セクションの 12 では、デバッガー コマンドを使用して、メモリの内容を表示します。*

**表示メモリ**

問題を識別するために、または変数や、ポインターを検査するメモリを確認する必要があります。 メモリを表示するには、次のいずれかを入力して**d\* &lt;アドレス&gt;** コマンド。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>db</p></td>
<td align="left"><p>バイト値および ASCII 文字のデータを表示します。</p></td>
</tr>
<tr class="even">
<td align="left"><p>dd</p></td>
<td align="left"><p>二重ワイド単語 (4 バイト) としてデータを表示します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>du</p></td>
<td align="left"><p>Unicode 文字データを表示します。</p></td>
</tr>
<tr class="even">
<td align="left"><p>dw</p></td>
<td align="left"><p>ワード値 (2 バイト) および ASCII の文字としてデータを表示します。</p></td>
</tr>
</tbody>
</table>

 

**注**  疑問符 (?) でその内容を示す、無効なアドレスを表示しようとした場合。

 

クリックして、メモリを表示する代わりに、**ビュー** &gt; **メモリ**します。 使用して、**表示形式**メモリを表示する方法を変更するプル ダウンします。

![windbg ビューの [メモリ] ウィンドウ](images/sysvad-lab-audio-memory-display.png)

1.  ボリューム コントロールに関連付けられたデータを表示するには、bm コマンドを使用して、PropertyHandlerAudioEngineVolumeLevel ルーチンを発生させるブレークポイントを設定します。 新しいブレークポイントを設定すると、前にすべてのビジネス継続性を使用して前のブレークポイントをクリアが\*します。

    ```dbgcmd
    kd> bc *
    ```

2.  Bm コマンドを使用して、PropertyHandlerAudioEngineVolumeLevel ルーチンを発生させるブレークポイントを設定します。

    ```dbgcmd
    kd> bm tabletaudiosample!CMiniportWaveRT::SetDeviceChannelVolume
      1: fffff80f`02c3a4b0 @!"tabletaudiosample!CMiniportWaveRT::SetDeviceChannelVolume"
    ```

3.  ブレークポイントが正しく設定されていることを確認するブレークポイントの一覧を表示します。

    ```dbgcmd
    kd> bl
      1: fffff80f`02c3a4b0 @!"tabletaudiosample!CMiniportWaveRT::SetDeviceChannelVolume"
    ```

4.  使用して、 **g**でコードが実行を再起動するコマンド。

    ターゲット システムには、システム トレイのボリュームを調整します。 これにより、ブレークポイントが起動します。

    ```dbgcmd
    Breakpoint 1 hit
    tabletaudiosample!CMiniportWaveRT::SetDeviceChannelVolume:
    fffff80f`02c3a4b0 44894c2420      mov     dword ptr [rsp+20h],r9d
    ```

5.  使用して、**ビュー** &gt; **ローカル**ローカル変数を表示するメニュー項目。 IVolume 変数の現在の値に注意してください。

6.  表示データ型と IVolume 変数の現在の値のサンプル コード」と入力して、 **dt**コマンドと変数の名前。

    ```dbgcmd
    kd> dt lVolume
    Local var @ 0xa011ea50 Type long
    0n-6291456
    ```

7.  SetDeviceChannelVolume を入力することで、ブレークポイントにヒットします。

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

8.  使用して IVolume のメモリ位置に値を表示しようとしています、 [ **dt (型の表示)** ](dt--display-type-.md)コマンド。

    ```dbgcmd
    kd> dt dt lVolume
    Local var @ 0xffffb780b7eee664 Type long
    0n0
    ```

    変数が定義するのにはまだ、ため、情報は含まれません。

9.  実行する転送最後の行のコード SetDeviceChannelVolume F10 キーを押します。

    ```dbgcmd
        return ntStatus;
    ```

10. 使用して IVolume のメモリ位置に値を表示、 [ **dt (表示の種類)** ](dt--display-type-.md)コマンド。

    ```dbgcmd
    kd> dt lVolume
    Local var @ 0xffffb780b7eee664 Type long
    0n-6291456
    ```

    これで、変数がアクティブでは、この例では 6291456 の値が表示されます。

11. 使用して、IVolume のメモリ位置を表示することも、 [**でしょうか。(式の評価)** ](---evaluate-expression-.md)コマンド。

    ```dbgcmd
    kd> ? lVolume
    Evaluate expression: -79711507126684 = ffffb780`b7eee664
    ```

12. 表示された場合、アドレス*ffffb780\`b7eee664* lVolume 変数のアドレスです。 Dd コマンドを使用すると、その場所でメモリの内容を表示できます。

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

13. L4 範囲パラメーターを指定することで、最初の 4 バイトのアドレスを表示できます。

    ```dbgcmd
    kd> dd ffffb780`b7eee664 l4
    ffffb780`b7eee664  ffa00000 00000018 00000000 c52d7008
    ```

14. さまざまな種類メモリの出力が表示されるを参照する入力、 **du**、 **da**と**db**コマンド。

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

    単精度浮動小数点数 (4 バイト) としてデータを表示するのにには、df 浮動小数点数のオプションを使用します。

    ```dbgcmd
    df ffffb780`b7eee664 
    ffffb780`b7eee664          -1.#QNAN   3.3631163e-044                0        -2775.002
    ffffb780`b7eee674          -1.#QNAN  -5.8032637e+019         -1.#QNAN        -2775.002
    ffffb780`b7eee684          -1.#QNAN                0         -1.#QNAN                0
    ffffb780`b7eee694          -1.#QNAN         -1.#QNAN         -1.#QNAN  -2.8479408e-005
    ```

**メモリへの書き込み**

メモリの読み取りに使用されるコマンドと同様に、使用できます、e\*メモリの内容を変更するコマンド。

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
<td align="left"><p>ASCII 文字列 (NULL で終了していません)</p></td>
</tr>
<tr class="even">
<td align="left"><p>eu</p></td>
<td align="left"><p>Unicode 文字列 (NULL で終了していません</p></td>
</tr>
<tr class="odd">
<td align="left"><p>新しい</p></td>
<td align="left"><p>ワード値 (2 バイト)</p></td>
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
<td align="left"><p>eb</p></td>
<td align="left"><p>バイト値</p></td>
</tr>
<tr class="odd">
<td align="left"><p>ed</p></td>
<td align="left"><p>ダブル ワード値 (4 バイト)</p></td>
</tr>
</tbody>
</table>

 

次の例では、メモリを上書きする方法を示します。

1.  最初に、サンプル コードで使用される lVolume のアドレスを見つけます。

    ```dbgcmd
    kd> ? lVolume
    Evaluate expression: -79711507126684 = ffffb780`b7eee664
    ```

2.  使用して、新しい文字でそのメモリ アドレスを上書き、 **eb**コマンド。

    ```dbgcmd
    kd> eb 0xffffb780`b7eee664 11 11 11 11 11
    ```

3.  」と入力して、文字を上書きされていることを確認するメモリ位置の表示、 **db**コマンド。

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

また、ウォッチやローカル変数ウィンドウのメモリの内容を変更できます。 [ウォッチ] ウィンドウで、現在のフレームのコンテキスト外にある変数を参照してください可能性があります。 それらの変更では、コンテキストにない場合は関係ありません。

## <a name="span-idendingthesessionspansection-13-end-the-windbg-session"></a><span id="endingthesession"></span>セクション 13:WinDbg のセッションを終了します。


**&lt;ホスト システムで**

ユーザー モードのデバッグ セッションを終了、デバッガーを休止モードに戻る、もう一度実行するターゲット アプリケーションの設定を入力、 **qd** (Quit およびデタッチ) コマンド。

使用してください、 **g**コマンド、コードの実行対象のコンピュータを使用できるようにします。 これを使用して、ブレークポイントをクリアするといった方法も * * bc \\* * * いるため、ターゲット コンピューターが中断してホスト コンピューターのデバッガーに接続しようとしています。 しません。

```dbgcmd
0: kd> qd
```

詳細については、次を参照してください。 [WinDbg でデバッグ セッションを終了する](ending-a-debugging-session-in-windbg.md)デバッグ リファレンス ドキュメント。

## <a name="span-idwindowsdebuggingresourcesspansection-14-windows-debugging-resources"></a><span id="windowsdebuggingresources"></span>セクション 14:Windows デバッグ用のリソース


追加情報は、Windows のデバッグで使用できます。 これらの例では、Windows Vista などの Windows の以前のバージョンを使用して、これらの書籍の一部が説明する概念は Windows のほとんどのバージョンに適用可能なことに注意してください。

**ブックの「**

-   *高度な Windows デバッグ*Mario Hewardt して Daniel Pravat

-   *内部の Windows デバッグ:A Practical Guide to デバッグ出力およびトレース戦略 Windows® で*Tarik Soulami によって

-   *Windows Internals* E. のある Mark Russinovich、David A. Solomon Alex Ionescu して

**ビデオ**

デフラグ ツール WinDbg エピソード 13 ~ 29 の表示します。 <https://channel9.msdn.com/Shows/Defrag-Tools>

**トレーニング ベンダー:**

OSR  - <https://www.osr.com/>


## <a name="see-also"></a>関連項目

[Windows のデバッグの概要](getting-started-with-windows-debugging.md) 

 






---
title: ネットワークが KDNET で仮想マシンのデバッグの設定
description: このトピックでは、カーネル デバッグを HYPER-V 仮想マシンへの接続を構成する方法について説明します。
ms.assetid: E4C4D2A1-2FB0-4028-8A52-30B8F4F738D0
ms.date: 07/02/2018
ms.localizationpriority: medium
ms.openlocfilehash: 5c42087cdf0cd516cb14cb57025a2697bbc8fe86
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63364728"
---
# <a name="setting-up-network-debugging-of-a-virtual-machine---kdnet"></a>ネットワークが仮想マシン - KDNET のデバッグの設定

このトピックでは、HYPER-V 仮想マシン (VM) へのカーネル デバッグ接続を構成する方法について説明します。


## <a name="hyper-v-virtual-machine-setup"></a>HYPER-V 仮想マシンのセットアップ

デバッグするには、Gen 2 HYPER-V 仮想マシン (VM) は、次の手順を完了します。

**1.Windows がインストールされた VM を作成します。**

VM を作成する方法については、次を参照してください。 [、Hyper-v と仮想マシンを作成](https://docs.microsoft.com/virtualization/hyper-v-on-windows/quick-start/quick-create-virtual-machine)です。

**2.外部仮想スイッチを定義します。** 

VM と仮想外部ネットワーク スイッチの通信に使用できます。 外部ネットワーク スイッチを作成する方法については、次を参照してください。[仮想ネットワークの作成](https://docs.microsoft.com/virtualization/hyper-v-on-windows/quick-start/connect-to-network)です。

外部ネットワーク スイッチが構成されている場合、次のオプションを設定する必要があります。

|オプション| [値]|
|----------|----------|
| 接続の種類 | 外部ネットワーク|
| 管理オペレーティング システムにこのネットワーク アダプターの共有を許可する | 有効 |
| VLAN ID | Disabled |


**3.セキュア ブートを無効にします。**

BCDEdit ブート設定を更新する kdnet ユーティリティは、一時的に、次の手順に従って、仮想マシンでセキュア ブートを無効にします。

1. HYPER-V マネージャーを読み込むし、VM のプロパティを選択します。

2. をクリックして、**セキュリティ**設定します。

3. チェック ボックスをオフ、**セキュア ブートを有効にする**チェック ボックスをオンします。

4. クリックして**OK**設定を保存します。

セキュア ブートは、再度有効に完了したらとデバッグは無効になりましたターゲット VM でのカーネル デバッグします。  


**4.Windows 用デバッグ ツールをインストールします。**

デバッグ ツールでは、デバッガーと kdnet ユーティリティが使用され、インストールする必要があります。 ダウンロードして、デバッグ ツールをインストールする方法については、次を参照してください。[デバッグ ツールの Windows にダウンロード](debugger-download-tools.md)します。 


## <a name="setting-up-network-debugging-of-a-virtual-machine---kdnet"></a>ネットワークが仮想マシン - KDNET のデバッグの設定

### <a name="record-the-host-ip-address"></a>ホストの IP アドレスを記録します。 

ホストのデバッガーをターゲットの仮想マシンとして同じ PC で実行するには、次の手順に従います。 

1. OS のホスト コンピューターでコマンド プロンプト ウィンドウを開き、入力*IPConfig* IP 構成を表示します。 

2. コマンドの出力では、外部仮想スイッチとして構成されているイーサネット アダプターを探します。

    ```console
    ...

    Ethernet adapter vEthernet (External Virtual Switch):

    ...

    IPv4 Address. . . . . . . . . . . : <YourHostIPAddress>

    ...

    ```

3. デバッグ ホスト アドレスとして使用される外部仮想スイッチの IPv4 アドレスを記録します。

4. ターゲットと、ホスト コンピューター間の接続を確認する対象のコンピューターで管理者特権でコマンド プロンプト ウィンドウを開くし、次のコマンドを入力、 *YourHostIPAddress*はホスト コンピューターの IP アドレスです。 

    ```console
    ping -4 <YourHostIPAddress>
    ```


## <a name="span-idsettingupthetargetcomputerspanspan-idsettingupthetargetcomputerspanspan-idsettingupthetargetcomputerspansetting-up-the-vm-target-computer"></a><span id="Setting_Up_the_Target_Computer"></span><span id="setting_up_the_target_computer"></span><span id="SETTING_UP_THE_TARGET_COMPUTER"></span>VM のターゲット コンピューターをセットアップします。

Kdnet.exe ユーティリティを使用すると、次の手順では対象のコンピューターのデバッガーの設定を自動的に構成します。

1. WDK の検索*kdnet.exe*と*VerifiedNICList.xml*ファイル。 既定ではそれらが表示されます。

```console
C:\Program Files (x86)\Windows Kits\10\Debuggers\x64
```

> [!NOTE]
> 次の手順では、両方の Pc に、ターゲットとホストの両方で Windows の 64 ビット バージョンが実行されていることを前提としています。 場合はそうでない、最適な方法では、ターゲットを実行しているホストでツールの同じ「ビット数」を実行します。 たとえば、ターゲットは、32 ビット Windows を実行している、ホスト上の 32 のバージョンのデバッガーを実行します。 詳細については、次を参照してください。 [32 ビットまたは 64 ビット デバッグ ツールを選択する](choosing-a-32-bit-or-64-bit-debugger-package.md)します。
> 

4. 切り取りし、貼り付けをするに使用される長いキーを許可するのには、拡張セッションのサポートを有効にします。 [VM] ウィンドウから、**ビュー**のプルダウン メニューを有効にする*拡張セッション*。 

5. 対象の VM のコンピューターに C:\KDNET ディレクトリおよびコピーを作成、 *kdnet.exe*と*VerifiedNICList.xml*ファイルをそのディレクトリにします。

6. ターゲット コンピューターで、管理者としてコマンド プロンプト ウィンドウを開きます。 ターゲット コンピューターに、サポートされているネットワーク アダプターがあることを確認するには、このコマンドを入力します。

    ```console
    C:\KDNET>kdnet

    Network debugging is supported on the following NICs:
    busparams=0.25.0, Intel(R) 82579LM Gigabit Network Connection, KDNET is running on this NIC.kdnet.exe
    ```

7. このコマンドをホスト システムの IP アドレスを設定して生成された一意の接続キー型です。 以前に記録したホスト システムの IP アドレスを使用します。  各ターゲット/ホスト ペアリングの一意のポート アドレスを選択と連携 50000 50039 範囲内です。 この例では、50005 を選択します。

    ```console
    C:\>kdnet <YourIPAddress> <YourDebugPort> 

    Enabling network debugging on Microsoft Hypervisor Virtual Machine.
    Key=3u8smyv477z20.2owh9gl90gbxx.3sfsihzgq7di4.nh8ugnmzb4l7

    To debug this vm, run the following command on your debugger host machine.
    windbg -k net:port=50005,key=3u8smyv477z20.2owh9gl90gbxx.3sfsihzgq7di4.nh8ugnmzb4l7

    Then restart this VM by running shutdown -r -t 0 from this command prompt.
    ```

8. CRTL + C を使用して、windbg の指定された出力をコマンド バッファーにコピーします。 これにより、返される長さのキー値を書き留めますしようとしています。

9. 再度有効にする BitLocker およびセキュリティで保護された boot 完了すると、デバッガーの設定を構成します。

10. 拡張セッションのサポートを使用して VM には、ブレークポイントでそのままにした場合のタイムアウトことができます、ために無効にする*拡張セッション*サポートを使用して、**ビュー**プル ダウン VM でのメニュー。 

11. デバッガーが読み込まれ、実行後、VM が再起動されます。 このプロセスは次に説明します。 


## <a name="span-idstartingthedebuggingsessionspanspan-idstartingthedebuggingsessionspanspan-idstartingthedebuggingsessionspanstarting-the-debugging-session"></a><span id="Starting_the_Debugging_Session"></span><span id="starting_the_debugging_session"></span><span id="STARTING_THE_DEBUGGING_SESSION"></span>デバッグ セッションの開始


2. 対象の PC に接続する場合に、CTRL + V を使用して、メインの OS コマンド ウィンドウで先ほどコピーした kdnet によって返された windbg 文字列を貼り付けます。

    ```console
    C:\Debuggers\windbg -k net:port=<YourDebugPort>,key=<YourKey> 
    ```

最初のネットワーク デバッグ接続を確立しようとは、デバッグ アプリケーション (WinDbg または KD) に、ファイアウォール経由のアクセスを許可するように求め可能性があります。 チェック ボックスをオンにして、プロンプトに応答する必要があります**3 つすべて**ネットワークの種類: ドメイン、プライベート、および公開します。 



## <a name="span-idrestartingtargetspanspan-idrestartingtargetspanspan-idrestartingtargetspan-restarting-the-target-pc"></a><span id="Restarting_Target"></span><span id="restarting_target"></span><span id="RESTARTING_TARGET"></span> 対象の PC を再起動します。

デバッガーを接続すると、対象のコンピュータを再起動します。 完全に再起動する VM を強制するには、管理者のコマンド プロンプトから、このコマンドを使用します。

   ```console
   shutdown -r -t 0 
   ```

ターゲットの仮想マシンが再起動されると、ホスト OS でデバッガーが接続する必要があります。 

VM に接続すると、ヒットの中断すると、デバッガーはデバッグを開始できます。 


## <a name="troubleshooting-kdnet-virtual-machine-network-debugging"></a>KDNET 仮想マシンのネットワークのトラブルシューティングのデバッグ 

デバッガーが接続できない場合は、接続を確認する対象の VM から ping コマンドを使用します。 

```console
C:\>Ping <HostComputerIPAddress> 
```

*何かが正しく動作していないし、かもしれないとしています.* 

- ように、ファイアウォールを介した WinDbg をできるようにしました。 
- BCDEdit または kdnet によって生成された一意のキーを使用していることを確認します。


*Vm はネットワーク接続がないです。*  

- HYPER-V マネージャーから仮想スイッチ マネージャーを開き、既存の仮想スイッチを選択して Microsoft カーネル デバッグ ネットワーク アダプターに、ドロップ ダウン ボックスから選択し、ok をクリックしてから、仮想スイッチ マネージャー ダイアログで、外部ネットワークの NIC を変更ボックス。  仮想スイッチ NIC を更新した後、シャット ダウンすることを確認しますし、Vm を再起動します。 



## <a name="sequence-to-add-hyper-v-role-to-a-windows-pc"></a>Windows PC に HYPER-V ロールを追加するシーケンス

対象のコンピューターが仮想マシン ホストの場合は、ネットワーク デバッグを設定し、まだ仮想マシンのネットワークのアクセス権を持ちます。

次のような状況でのデバッグを設定するとします。

-   対象のコンピュータでは、単一のネットワーク インターフェイス カードが。
-   ターゲット コンピューターに HYPER-V ロールをインストールする予定があります。
-   ターゲット コンピューターに 1 つまたは複数の仮想マシンを作成する予定があります。

最良のアプローチでは、ネットワーク、Hyper-v の役割をインストールする前に、ターゲット コンピューターでのデバッグを設定します。 仮想マシンはネットワークへのアクセスがあります。

デバッグ対象のコンピューター上で HYPER-V ロールがインストールされた後のネットワークをセットアップする場合は、カーネル ネットワーク デバッグ アダプターにこれらをブリッジする、仮想マシンのネットワーク設定を変更する必要があります。 それ以外の場合、仮想マシンには、ネットワークへのアクセスはありません。


## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>関連トピック

[カーネル モード デバッグのセットアップ、仮想マシン手動で仮想 COM ポートを使用しての](attaching-to-a-virtual-machine--kernel-mode-.md)

[ネットワーク接続を手動で設定](setting-up-a-network-debugging-connection.md)

 

 







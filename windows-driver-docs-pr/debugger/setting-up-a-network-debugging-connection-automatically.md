---
title: KDNET ネットワーク カーネル デバッグの自動設定
description: KDNET を使用すると、ネットワークのカーネル デバッグが自動的に、Windows 用デバッグ ツールを構成できます。
ms.assetid: B4A79B2E-D4B1-42CA-9121-DEC923C76927
keywords:
- ネットワークのデバッグ
- イーサネットのデバッグ
- WinDbg
- KDNET
ms.date: 09/25/2018
ms.localizationpriority: medium
ms.openlocfilehash: d33e84652f94172fa4df340ae488450cee94615f
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56573659"
---
# <a name="setting-up-kdnet-network-kernel-debugging-automatically"></a>KDNET ネットワーク カーネル デバッグの自動設定

デバッグ ツールの Windows カーネルがネットワーク経由でデバッグをサポートします。 このトピックでは、デバッグ、kdnet.exe セットアップ ツールを使用して自動的にネットワークをセットアップする方法を説明します。

デバッガーを実行しているコンピューターが呼び出されます、*ホスト コンピューター*、デバッグ中のコンピューターを呼び出すと、*対象のコンピュータ*します。 7 以降、ホスト コンピューターで Windows が実行する必要があり、8 またはそれ以降、ターゲット コンピューターで Windows が実行する必要があります。



## <a name="span-iddeterminingtheipaddressofthehostcomputerspanspan-iddeterminingtheipaddressofthehostcomputerspanspan-iddeterminingtheipaddressofthehostcomputerspandetermining-the-ip-address-of-the-host-computer"></a><span id="Determining_the_IP_Address_of_the_Host_Computer"></span><span id="determining_the_ip_address_of_the_host_computer"></span><span id="DETERMINING_THE_IP_ADDRESS_OF_THE_HOST_COMPUTER"></span>ホスト コンピューターの IP アドレスを決定します。

1. ターゲットとホスト Pc がネットワーク ハブに接続しているまたは、適切なネットワーク ケーブルを使用して切り替えることを確認します。 

2. ホスト コンピューターでは、コマンド プロンプト ウィンドウを開き、入力*IPConfig* IP 構成を表示します。 

3. コマンドの出力では、イーサネット アダプターの IPv4 アドレスを見つけます。

    ```console
    ...

    Ethernet adapter Ethernet:
    ...

    IPv4 Address. . . . . . . . . . . : <YourHostIPAddress>
    ...

    ```
4. デバッグに使用するネットワーク アダプターの IPv4 アドレスをメモしておきます。

 

## <a name="span-idsettingupthetargetcomputerspanspan-idsettingupthetargetcomputerspanspan-idsettingupthetargetcomputerspansetting-up-the-host-and-target-computers"></a><span id="Setting_Up_the_Target_Computer"></span><span id="setting_up_the_target_computer"></span><span id="SETTING_UP_THE_TARGET_COMPUTER"></span>ホストとターゲット コンピューターを設定します。

Kdnet.exe ユーティリティを使用すると、次の手順では対象のコンピューターのデバッガーの設定を自動的に構成します。

1. Windows デバッグ ツールがホスト システム上にインストールされていることを確認します。 ダウンロードして、デバッガー ツールのインストールについては、[デバッグ ツールの Windows にダウンロード](debugger-download-tools.md)を参照してください。 

2. 検索、 *kdnet.exe*と*VerifiedNICList.xml*ファイル。 既定では、これらはここにします。

   ```console
   C:\Program Files (x86)\Windows Kits\10\Debuggers\x64
   ```

   > [!NOTE]
   > 次の手順では、両方の Pc に、ターゲットとホストの両方で Windows の 64 ビット バージョンが実行されていることを前提としています。 場合はそうでない、最適な方法では、ターゲットを実行しているホストでツールの同じ「ビット数」を実行します。 たとえば、ターゲットは、32 ビット Windows を実行している、ホスト上の 32 のバージョンのデバッガーを実行します。 詳細については、[32 ビットまたは 64 ビット デバッグ ツールを選択する](choosing-a-32-bit-or-64-bit-debugger-package.md)を参照してください。
   > 

3. ホスト コンピューターでは、2 つのファイルをネットワーク共有にコピーまたはつまみのドライブでは、ターゲット コンピューター上で使用できるようにします。

4. 対象のコンピューターに C:\KDNET ディレクトリおよびコピーを作成、 *kdnet.exe*と*VerifiedNICList.xml*ファイルをそのディレクトリにします。

   > [!IMPORTANT]
   > ブート情報を変更する kdnet を使用する前に、テスト用のコンピューターの BitLocker とセキュア ブートなどの Windows セキュリティ機能を一時的に中断する必要があります。
   > テストが完了すると、これらのセキュリティ機能を再度有効にし、適切なセキュリティ機能を無効にするテスト PC を管理します。


5. ターゲット コンピューターで、管理者としてコマンド プロンプト ウィンドウを開きます。 ターゲット コンピューターに、サポートされているネットワーク アダプターがあることを確認するには、このコマンドを入力します。

   ```console
   C:\KDNET>kdnet
   Network debugging is supported on the following NICs:
   busparams=1.0.0, Broadcom NetXtreme Gigabit Ethernet, Plugged in.  
   This Microsoft hypervisor supports using KDNET in guest VMs.
   ```

6. Kdnet からの出力にそのネットワーク アダプターに示すよう、ターゲットがサポートされている、進むことができます。

7. このコマンドをホスト システムの IP アドレスを設定して生成された一意の接続キー型です。 IP アドレスまたはホスト システムの名前を使用します。 各ターゲット/ホスト ペアリングの一意のポート アドレスを選択と連携 50000 50039 の推奨される範囲内です。

   ```console
   C:\>kdnet <HostComputerIPAddress> <YourDebugPort> 
   
   Enabling network debugging on Intel(R) 82577LM Gigabit Network Connection.
   Key=2steg4fzbj2sz.23418vzkd4ko3.1g34ou07z4pev.1sp3yo9yz874p
   ```

8. 返されたキーをメモ帳の .txt ファイルにコピーします。


## <a name="span-idusingwindbgspanspan-idusingwindbgspanspan-idusingwindbgspan-using-windbg"></a><span id="Using_WinDbg"></span><span id="using_windbg"></span><span id="USING_WINDBG"></span> Using WinDbg

ホスト コンピューターでは、WinDbg を開きます。 **ファイル**] メニューの [選択**カーネル デバッグ**します。 カーネル デバッグ ダイアログ ボックスで、開く、 **Net**タブ。実際のポート番号と以前に保存したをメモ帳の .txt ファイルでキーを貼り付けます。 **[OK]** をクリックします。

コマンド プロンプト ウィンドウを開き、次のコマンドを入力して、WinDbg セッションを開始することもできます、 <YourPort> 、上で選択したポートと<YourKey>kdnet 上記によって返されたキーします。 以前に保存したをメモ帳の .txt ファイルでそのキーを貼り付けます。

   ```console
  windbg -k net:port=<YourDebugPort>,key=<YourKey> 
   ```

WinDbg のポートにアクセスを許可するポートをファイアウォール経由でアクセスするための WinDbg に関する求められたら、 **3 つすべて**の異なるネットワークの種類。

![windows セキュリティの警告 - windows ファイアウォールがこのアプリの一部の機能をブロックします。 ](images/debuglab-image-firewall-dialog-box.png)


## <a name="span-idrestartingtargetspanspan-idrestartingtargetspanspan-idrestartingtargetspan-restarting-the-target-pc"></a><span id="Restarting_Target"></span><span id="restarting_target"></span><span id="RESTARTING_TARGET"></span> 対象の PC を再起動します。

デバッガーを接続すると、対象のコンピュータを再起動します。 管理者のコマンド プロンプトから次のコマンドを使用することは、PC を再起動する方法の 1 つです。

   ```console
   shutdown -r -t 0 
   ```

## <a name="span-idtroubleshootingtipsspanspan-idtroubleshootingtipsspantroubleshooting-tips"></a><span id="troubleshooting_tips"></span><span id="TROUBLESHOOTING_TIPS"></span>トラブルシューティングのヒント

**アプリケーションのデバッグを許可するファイアウォールを通過する必要があります。**

デバッガー、ファイアウォール経由のアクセスが必要です。 コントロール パネルを使用すると、ファイアウォール経由のアクセスを許可します。 

1. 開いている**コントロール パネルの [&gt;システムとセキュリティ**] をクリック**アプリを Windows ファイアウォールを通過できます**します。 

2. アプリケーションの一覧で探します*Windows GUI のシンボリック デバッガー*と*Windows カーネル デバッガー*します。 

3. これら 2 つのアプリケーションを許可するチェック ボックスを使用して**3 つすべて**の種類の異なるネットワーク ファイアウォールを経由します。 

4. 下へスクロールし、をクリックして**OK**は、ファイアウォールの変更を保存します。 デバッガーを再起動します。

    ![windows のコントロール パネルのファイアウォールの構成が Windows GUI のシンボリック デバッガーと Windows カーネル デバッガーを有効になっている次の 3 つネットワークの種類のすべての表示](images/firewall-control-pannel-windbg-gui-config.png)

**Ping を使用して、接続をテストするには**

場合は、デバッガーは、タイムアウトになると、接続していないのターゲット PC に、ping コマンドを使用して、接続を確認します。 

   ```console
   C:\>Ping <HostComputerIPAddress> 
   ```

**ネットワーク デバッグ用にポートを選択します。**

デバッガーでは、タイムアウトになると、接続していないの場合は、50000 の既定のポート番号は既に使用またはブロックされているため、その可能性があります。 

任意のポート番号は 49152 ~ 65535 から選択できます。 推奨される範囲では、50000 ~ 50039 です。 選択したポートを排他アクセスのホスト コンピューターで実行されているデバッガーでは開けません。 

**注**  ネットワーク デバッグに使用できるポート番号の範囲は、会社のネットワーク ポリシーによって制限される可能性があります。 会社のポリシーがネットワークのデバッグに使用できるポートの範囲を制限するかどうかを判断するには、ネットワーク管理者に確認します。

**サポートされているネットワーク アダプター**

Kdnet.exe を実行すると、そのネットワーク アダプターがサポートされていないことと、「このマシンの Nic のいずれかのネットワークのデバッグはサポートされていません」の場合は表示されます。 

ホスト コンピューターは、任意のネットワーク アダプターを使用できますが、ターゲット コンピューターが Windows のツールをデバッグでサポートされているネットワーク アダプターを使用する必要があります。 サポートされているネットワーク アダプターの一覧は、[イーサネット Nic を Windows 10 でのネットワーク カーネル デバッグのサポートされている](supported-ethernet-nics-for-network-kernel-debugging-in-windows-10.md)と[イーサネット Nic を Windows 8.1 でのネットワーク カーネル デバッグのサポートされている](supported-ethernet-nics-for-network-kernel-debugging-in-windows-8-1.md)を参照してください。



## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>関連トピック

[Windows 10 でのデバッグ ネットワーク カーネルのイーサネット Nic をサポート](supported-ethernet-nics-for-network-kernel-debugging-in-windows-10.md)
 

[Windows 8.1 でのデバッグ ネットワーク カーネルのイーサネット Nic をサポート](supported-ethernet-nics-for-network-kernel-debugging-in-windows-8-1.md)


[KDNET のネットワーク カーネル デバッグを手動での設定](setting-up-a-network-debugging-connection.md)


 







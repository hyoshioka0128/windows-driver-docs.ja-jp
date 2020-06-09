---
title: Visual Studio での仮想マシンのカーネルモード デバッグの設定
description: Microsoft Visual Studio を使用して、仮想マシンのカーネルモードデバッグをセットアップし、実行することができます。
ms.assetid: E7A289CA-29CE-4C6F-AD08-529E58379715
ms.date: 10/08/2018
ms.localizationpriority: medium
ms.openlocfilehash: e965d57fdd8bd4a6d8403c2fff68564c6f2b2a2d
ms.sourcegitcommit: dadc9ced1670d667e31eb0cb58d6a622f0f09c46
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/09/2020
ms.locfileid: "84534767"
---
# <a name="setting-up-kernel-mode-debugging-of-a-virtual-machine-in-visual-studio"></a>Visual Studio での仮想マシンのカーネルモード デバッグの設定

> [!IMPORTANT]
> この機能は、Windows 10 バージョン1507以降のバージョンの WDK では使用できません。
>

Microsoft Visual Studio を使用して、仮想マシンのカーネルモードデバッグをセットアップし、実行することができます。 仮想マシンは、デバッガーと同じ物理コンピューターに配置することも、同じネットワークに接続されている別のコンピューターに配置することもできます。 Visual Studio を使用してカーネルモードのデバッグを行うには、Visual Studio に Windows Driver Kit (WDK) が統合されている必要があります。 統合環境をインストールする方法の詳細については、「 [Visual Studio を使用したデバッグ](debugging-using-visual-studio.md)」を参照してください。

デバッガーを実行するコンピューターは*ホストコンピューター*と呼ばれ、デバッグ対象の仮想マシンは*ターゲット仮想マシン*と呼ばれます。

## <a name="span-idconfiguring_the_target_virtual_machinespanspan-idconfiguring_the_target_virtual_machinespanspan-idconfiguring_the_target_virtual_machinespanconfiguring-the-target-virtual-machine"></a><span id="Configuring_the_Target_Virtual_Machine"></span><span id="configuring_the_target_virtual_machine"></span><span id="CONFIGURING_THE_TARGET_VIRTUAL_MACHINE"></span>ターゲット仮想マシンを構成しています


1. 仮想マシンで、管理者特権でのコマンドプロンプトウィンドウに次のコマンドを入力します。

   **bcdedit/debug on**

   **bcdedit/dbgsettings serial debugport:**<em>n</em> **ボーレート: 115200**

   ここで、 *n*は仮想マシンの COM ポートの番号です。

2. 仮想マシンを再起動します。
3. 仮想マシンで、COM ポートを名前付きパイプにマップするように構成します。 デバッガーはこのパイプを介して接続します。 このパイプの作成方法の詳細については、仮想マシンのドキュメントを参照してください。

## <a name="span-idconfiguring_the_host_computerspanspan-idconfiguring_the_host_computerspanspan-idconfiguring_the_host_computerspanconfiguring-the-host-computer"></a><span id="Configuring_the_Host_Computer"></span><span id="configuring_the_host_computer"></span><span id="CONFIGURING_THE_HOST_COMPUTER"></span>ホストコンピューターの構成


ホストコンピューターは、仮想マシンを実行しているのと同じ物理コンピューターにすることも、別のコンピューターにすることもできます。

1. ホストコンピューターの Visual Studio の [**ドライバー** ] メニューで、[テスト] **[ &gt; コンピューターの構成**] の順に選択します。
2. [**新しいコンピューターの追加**] をクリックします。
3. [**コンピューター名**] に、ターゲット仮想マシンを実行している物理コンピューターの名前を入力します。
4. [**デバッガーを手動で構成してプロビジョニング**しない] を選択し、[**次へ**] をクリックします。
5. [**接続の種類**] で [**シリアル**] を選択します。
6. **パイプ**を確認し、[**再接続**] を確認します。
7. デバッガーが仮想マシンと同じコンピューター上で実行されている場合は、**パイプ名**に次のように入力します。

   **\\\\.\\パイプ \\ **<em>pipename</em>。

   デバッガーが仮想マシンとは別のコンピューターで実行されている場合は、**パイプ名**に次のように入力します。

   **\\\\**<em>VMHost</em>** \\ パイプ \\ **<em>pipename</em>

   ここで、 *VMHost*はターゲット仮想マシンを実行している物理コンピューターの名前、 *pipename*はターゲット仮想マシンの COM ポートに関連付けられているパイプの名前です。

8. **[次へ]** をクリックします。 **[完了]** をクリックします。

## <a name="span-idstarting_the_debugging_sessionspanspan-idstarting_the_debugging_sessionspanspan-idstarting_the_debugging_sessionspanstarting-the-debugging-session"></a><span id="Starting_the_Debugging_Session"></span><span id="starting_the_debugging_session"></span><span id="STARTING_THE_DEBUGGING_SESSION"></span>デバッグセッションを開始しています


1.  ホストコンピューターの Visual Studio で、[**デバッグ**] メニューの [**プロセスにアタッチ**] をクリックします。
2.  [**トランスポート**] で、[ **Windows カーネルモードデバッガー**] を選択します。
3.  [**修飾子**] で、ターゲット仮想マシンを実行している物理コンピューターの名前を選択します。
4.  **[アタッチ]** をクリックします。

>[!TIP] 
> "デバッグセッションを開始できませんでした。エラー 8007005: アクセスが拒否されました" というメッセージが表示された場合は、ホストコンピューターで Visual Studio を管理者として実行します。 

## <a name="span-idgeneration_2_virtual_machinesspanspan-idgeneration_2_virtual_machinesspangeneration-2-virtual-machines"></a><span id="generation_2_virtual_machines"></span><span id="GENERATION_2_VIRTUAL_MACHINES"></span>第2世代 Virtual Machines


既定では、第2世代仮想マシンに COM ポートは表示されません。 COM ポートは、PowerShell または WMI を使用して追加できます。 Hyper-v マネージャーコンソールに COM ポートを表示するには、そのポートをパスで作成する必要があります。

第2世代仮想マシンの COM ポートを使用してカーネルデバッグを有効にするには、次の手順を実行します。

1. 次の PowerShell コマンドを入力して、セキュアブートを無効にします。

   **Set-vmfirmware – Vmname** *Vmname* **– EnableSecureBoot Off**

   ここで、 *VmName*は仮想マシンの名前です。

2. 次の PowerShell コマンドを入力して、仮想マシンに COM ポートを追加します。

   **Set VMComPort – VMName** *VMName* **1 \\ \\ \\パイプ \\ **<em>pipename</em>

   たとえば、次のコマンドは、ローカルコンピューター上の名前付きパイプ Testvm に接続するために、仮想マシン TestVM の最初の COM ポートを構成します。

   **Set VMComPort – VMName TestVM 1 \\ \\ \\パイプ \\ testpipe**

3. VM を再起動して、新しい設定が有効になるようにします。

詳細については、「[ジェネレーション 2 仮想マシンの概要](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/dn282285(v=ws.11))」を参照してください。


## <a name="span-idfirewallsspantroubleshooting-firewalls-and-network-access-issues"></a><span id="Firewalls"></span>ファイアウォールとネットワークアクセスの問題のトラブルシューティング

デバッガー (WinDbg または KD) は、ファイアウォール経由でアクセスできる必要があります。 これは、ネットワークアダプターでサポートされている仮想シリアルポートにも当てはまります。

デバッガーの読み込み時に Windows からファイアウォールをオフにするように求めるメッセージが表示された場合は、 **3 つすべて**のボックスをオンにします。

使用中の VM の詳細に応じて、仮想マシンのネットワーク設定を変更して、Microsoft カーネルネットワークデバッグアダプターにブリッジすることが必要になる場合があります。 そうしないと、仮想マシンはネットワークにアクセスできなくなります。

**Windows ファイアウォール**

コントロールパネルを使用して、Windows ファイアウォールを経由したアクセスを許可できます。 

1. コントロールパネルを開き > システムとセキュリティ] をクリックし、[Windows ファイアウォールを介したアプリの許可] を選択します。 
2. アプリケーションの一覧で、 *WINDOWS GUI のシンボリックデバッガー*と*windows カーネルデバッガー*を見つけます。 
3. この2つのアプリケーションをファイアウォールで許可するには、このチェックボックスを使用します。 ［OK］をクリックして設定を保存します。
4. デバッグアプリケーション (WinDbg または KD) を再起動します。


## <a name="span-idrelated_topicsspanrelated-topics"></a><span id="related_topics"></span>関連トピック


[バーチャルマシンホストのネットワークデバッグの設定](setting-up-network-debugging-of-a-virtual-machine-host.md)
 

 







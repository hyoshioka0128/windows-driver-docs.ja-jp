---
title: Visual Studio での仮想マシンのカーネルモード デバッグの設定
description: Microsoft Visual Studio を使用して、設定し、仮想マシンのカーネル モードのデバッグを実行することができます。
ms.assetid: E7A289CA-29CE-4C6F-AD08-529E58379715
ms.date: 10/08/2018
ms.localizationpriority: medium
ms.openlocfilehash: fa784a5cdb58fdcdb0830978688503f6b6e6e01f
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56573638"
---
# <a name="setting-up-kernel-mode-debugging-of-a-virtual-machine-in-visual-studio"></a>Visual Studio での仮想マシンのカーネルモード デバッグの設定

> [!IMPORTANT]
> この機能は、Windows 10 バージョン 1507、以降のバージョンの WDK でご利用いただけません。
>

Microsoft Visual Studio を使用して、設定し、仮想マシンのカーネル モードのデバッグを実行することができます。 仮想マシンは、デバッガーと同じ物理コンピューターまたは同じネットワークに接続されている別のコンピューターに配置できます。 カーネル モードのデバッグを Visual Studio を使用するには、Windows Driver Kit (WDK) の Visual Studio と統合が必要です。 統合環境をインストールする方法については、次を参照してください。 [Windows ドライバー開発](https://go.microsoft.com/fwlink/p?linkid=301383)します。

デバッガーを実行しているコンピューターと呼ばれる、*ホスト コンピューター*、され、デバッグ中に仮想マシンが呼び出されます、*ターゲット仮想マシン*します。

## <a name="span-idconfiguringthetargetvirtualmachinespanspan-idconfiguringthetargetvirtualmachinespanspan-idconfiguringthetargetvirtualmachinespanconfiguring-the-target-virtual-machine"></a><span id="Configuring_the_Target_Virtual_Machine"></span><span id="configuring_the_target_virtual_machine"></span><span id="CONFIGURING_THE_TARGET_VIRTUAL_MACHINE"></span>ターゲット仮想マシンの構成


1. 管理者特権のコマンド プロンプト ウィンドウで、仮想マシンでは、次のコマンドを入力します。

   **bcdedit /debug on**

   **bcdedit/dbgsettings シリアル debugport:**<em>n</em> **baudrate:115200**

   場所*n*は仮想マシン上の COM ポートの数です。

2. 仮想マシンを再起動します。
3. 仮想マシンでは、名前付きパイプにマップする COM ポートを構成します。 デバッガーは、このパイプを使用して接続されます。 このパイプを作成する方法の詳細については、仮想マシンのドキュメントを参照してください。

## <a name="span-idconfiguringthehostcomputerspanspan-idconfiguringthehostcomputerspanspan-idconfiguringthehostcomputerspanconfiguring-the-host-computer"></a><span id="Configuring_the_Host_Computer"></span><span id="configuring_the_host_computer"></span><span id="CONFIGURING_THE_HOST_COMPUTER"></span>ホスト コンピューターを構成します。


ホスト コンピューターは、仮想マシンを実行している同じ物理コンピューターを指定できますか別のコンピューターであることができます。

1. Visual Studio で、ホスト コンピューター上で、**ドライバー** ] メニューの [選択**テスト&gt;コンピューターの構成**します。
2. クリックして**新しいコンピューターを追加**します。
3. **コンピューター名**ターゲットの仮想マシンを実行している物理コンピューターの名前を入力します。
4. 選択**を手動でデバッガーを構成し、プロビジョニングを行わないでください**、 をクリック**次**します。
5. **接続の種類**、**シリアル**します。
6. 確認**パイプ**、確認と**再接続**します。
7. デバッガーが、仮想マシンと同じコンピューターで実行している場合、次の入力**パイプ名**:

   **\\\\.\\パイプ\\**<em>PipeName</em>します。

   デバッガーが、仮想マシンから別のコンピューターで実行している場合、次の入力**パイプ名**:

   **\\\\**<em>VMHost</em>**\\pipe\\**<em>PipeName</em>

   ここで、 *VMHost* 、ターゲット仮想マシンを実行している物理コンピューターの名前を指定し、 *PipeName*ターゲット仮想マシン上の COM ポートに関連付けられているパイプの名前を指定します。

8. **[次へ]** をクリックします。 **[完了]** をクリックします。

## <a name="span-idstartingthedebuggingsessionspanspan-idstartingthedebuggingsessionspanspan-idstartingthedebuggingsessionspanstarting-the-debugging-session"></a><span id="Starting_the_Debugging_Session"></span><span id="starting_the_debugging_session"></span><span id="STARTING_THE_DEBUGGING_SESSION"></span>デバッグ セッションの開始


1.  Visual Studio で、ホスト コンピューター上で、**デバッグ**] メニューの [選択**プロセスにアタッチ**します。
2.  **トランスポート**、選択**Windows カーネル モードのデバッガー**します。
3.  **修飾子**ターゲットの仮想マシンを実行している物理コンピューターの名前を選択します。
4.  クリックして**アタッチ**します。

>[!TIP] 
> メッセージが表示される場合は、"エラー 8007005、デバッグ セッションを開始できませんでした。アクセスが拒否されました"、ホスト コンピューターで管理者として Visual Studio を実行します。 

## <a name="span-idgeneration2virtualmachinesspanspan-idgeneration2virtualmachinesspangeneration-2-virtual-machines"></a><span id="generation_2_virtual_machines"></span><span id="GENERATION_2_VIRTUAL_MACHINES"></span>第 2 世代仮想マシン


既定では、COM ポートは、第 2 世代仮想マシンには表示されません。 PowerShell または WMI を介して COM ポートを追加することができます。 HYPER-V Manager コンソールに表示する COM ポートについて、パスを使用してそれらに作成する必要があります。

COM ポートを使用して、第 2 世代仮想マシンでのカーネル デバッグを有効にするのには、次の手順を実行します。

1. この PowerShell コマンドを入力して、セキュア ブートを無効にします。

   **Set-vmfirmware – Vmname** *VmName* **– EnableSecureBoot オフ**

   場所*VmName*仮想マシンの名前を指定します。

2. この PowerShell コマンドを入力して、仮想マシンに COM ポートを追加します。

   **Set-VMComPort –VMName** *VmName* **1 \\\\.\\pipe\\**<em>PipeName</em>

   たとえば、次のコマンドは、仮想マシンの名前付きパイプ TestPipe、ローカル コンピューターに接続するための TestVM で最初の COM ポートを構成します。

   **Set-vmcomport – VMName TestVM 1 \\ \\.\\パイプ\\TestPipe**

3. VM を再起動して、新しい設定が有効にします。

詳細については、「 [Generation 2 Virtual Machine Overview](https://go.microsoft.com/fwlink/p/?Linkid=331326)」を参照してください。


## <a name="span-idfirewallsspantroubleshooting-firewalls-and-network-access-issues"></a><span id="Firewalls"></span>ファイアウォールとネットワーク アクセスの問題のトラブルシューティング

デバッガー (WinDbg または KD) ファイアウォール経由のアクセスが必要です。 ネットワーク アダプターでサポートされている仮想シリアル ポートの場合、このこともできます。

デバッガーが読み込まれたになっているときに、ファイアウォールを無効にする Windows によって求められた場合**3 つすべて**ボックス。

使用中の VM の詳細、によっては、それらをカーネル ネットワーク デバッグ アダプターをブリッジする、仮想マシンのネットワーク設定を変更する必要があります。 それ以外の場合、仮想マシンには、ネットワークへのアクセスはありません。

**Windows ファイアウォール**

コントロール パネルを使用して、Windows ファイアウォール経由のアクセスを許可することができます。 

1. コントロール パネルを開き > Windows ファイアウォールを介してアプリを許可するシステムとセキュリティ、および選択します。 
2. アプリケーションの一覧で探します*Windows GUI のシンボリック デバッガー*と*Windows カーネル デバッガー*します。 
3. これら 2 つのアプリケーション、ファイアウォールを通過を許可するのにチェック ボックスを使用します。 ［OK］をクリックして設定を保存します。
4. デバッグ (WinDbg または KD) アプリケーションを再起動します。


## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>関連トピック


[バーチャル マシン ホストのネットワークのデバッグの設定](setting-up-network-debugging-of-a-virtual-machine-host.md)
 

 







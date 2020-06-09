---
title: 仮想 COM ポートを使用して、仮想マシンのカーネルモードデバッグを手動で設定する
description: Windows 用デバッグツールでは、仮想 COM ポートを使用した仮想マシンのカーネルデバッグがサポートされています。
ms.assetid: e863e664-8338-4bbe-953b-e000a6843db9
keywords:
- 仮想マシンのデバッグ
- Virtual PC のデバッグ
- VMware のデバッグ
ms.date: 04/23/2019
ms.localizationpriority: medium
ms.openlocfilehash: 49ec551a5bedc59e0ca45d8fc81b9f75a3f4e4f7
ms.sourcegitcommit: dadc9ced1670d667e31eb0cb58d6a622f0f09c46
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/09/2020
ms.locfileid: "84533909"
---
# <a name="setting-up-kernel-mode-debugging-of-a-virtual-machine-manually-using-a-virtual-com-port"></a>仮想 COM ポートを使用して、仮想マシンのカーネルモードデバッグを手動で設定する

Windows 用デバッグツールでは、仮想マシンのカーネルデバッグがサポートされています。 仮想マシンは、デバッガーと同じ物理コンピューターに配置することも、同じネットワークに接続されている別のコンピューターに配置することもできます。 このトピックでは、KDCOM 経由で仮想 COM ポートを使用して、仮想マシンのデバッグを手動で設定する方法について説明します。

KDNET 仮想ネットワークの使用はより高速なオプションであるため、お勧めします。 詳細については、「 [KDNET を使用した仮想マシンのネットワークデバッグの設定](setting-up-network-debugging-of-a-virtual-machine-host.md)」を参照してください。


## <a name="span-idsetting_up_the_target_virtual_machinespanspan-idsetting_up_the_target_virtual_machinespanspan-idsetting_up_the_target_virtual_machinespansetting-up-the-target-virtual-machine"></a><span id="Setting_Up_the_Target_Virtual_Machine"></span><span id="setting_up_the_target_virtual_machine"></span><span id="SETTING_UP_THE_TARGET_VIRTUAL_MACHINE"></span>ターゲット仮想マシンを設定しています

デバッガーを実行するコンピューターは*ホストコンピューター*と呼ばれ、デバッグ対象の仮想マシンは*ターゲット仮想マシン*と呼ばれます。

> [!IMPORTANT]
> BCDEdit を使用してブート情報を変更する前に、テスト PC で BitLocker やセキュアブートなどの Windows のセキュリティ機能を一時的に停止することが必要になる場合があります。
> セキュリティ機能が無効になっている場合は、テストが完了し、テスト PC を適切に管理するときに、これらのセキュリティ機能を再び有効にします。

1. 仮想マシンで、管理者特権でのコマンドプロンプトウィンドウに次のコマンドを入力します。

   **bcdedit/debug on**

   **bcdedit/dbgsettings serial debugport:**<em>n</em> **ボーレート: 115200**

   ここで、 *n*は仮想マシンの COM ポートの番号です。 

2. 仮想マシンで、COM ポートを名前付きパイプにマップするように構成します。 デバッガーはこのパイプを介して接続します。 このパイプの作成方法の詳細については、仮想マシンのドキュメントを参照してください。

3. 管理者特権モードでデバッガーを起動します (たとえば、管理者のコマンドプロンプトから)。 シリアルパイプ経由で VM をデバッグする場合は、デバッガーが管理者特権モードで実行されている必要があります。  デバッガーがアタッチされて実行されたら、ターゲット VM を再起動します。


## <a name="span-idstarting_the_debuggerspanspan-idstarting_the_debuggerspanstarting-the-debugging-session-using-windbg"></a><span id="starting_the_debugger"></span><span id="STARTING_THE_DEBUGGER"></span>WinDbg を使用してデバッグセッションを開始する

ホストコンピューターで、管理者として [WinDbg] を開きます。 シリアルパイプ経由で VM をデバッグする場合は、デバッガーが管理者特権モードで実行されている必要があります。 [**ファイル**] メニューの [**カーネルデバッグ**] をクリックします。 [カーネルデバッグ] ダイアログボックスで、[ **COM** ] タブを開きます。 [**パイプ**] ボックスをオンにして、[**再接続**] ボックスをオンにします。 [**ボーレート**] に「115200」と入力します。 [**リセット**] に「0」と入力します。

デバッガーが仮想マシンと同じコンピューター上で実行されている場合は、[**ポート**] に次のように入力します。

**\\\\.\\パイプ \\ **<em>pipename</em>。

デバッガーが仮想マシンとは別のコンピューターで実行されている場合は、[**ポート**] に次のように入力します。

**\\\\**<em>VMHost</em>** \\ パイプ \\ **<em>pipename</em>

**[OK]** をクリックします。

また、コマンドラインで WinDbg を開始することもできます。 デバッガーが仮想マシンと同じ物理コンピューター上で実行されている場合は、コマンドプロンプトウィンドウで次のコマンドを入力します。

**windbg-k com: パイプ、ポート = \\ \\ 。 \\パイプ \\ **<em>pipename</em>**、リセット = 0、再接続**

デバッガーが仮想マシンとは別の物理コンピューター上で実行されている場合は、コマンドプロンプトウィンドウで次のコマンドを入力します。

**windbg-k com: パイプ、ポート = \\ \\ **<em>VMHost</em>** \\ パイプ \\ **<em>pipename</em>**、リセット = 0、再接続**

## <a name="span-idstarting_the_debugging_session_using_kdspanspan-idstarting_the_debugging_session_using_kdspanspan-idstarting_the_debugging_session_using_kdspanstarting-the-debugging-session-using-kd"></a><span id="Starting_the_Debugging_Session_Using_KD"></span><span id="starting_the_debugging_session_using_kd"></span><span id="STARTING_THE_DEBUGGING_SESSION_USING_KD"></span>KD を使用したデバッグセッションの開始


デバッガーと同じ物理コンピューター上で実行されている仮想マシンをデバッグするには、*管理者特権*のコマンドプロンプトウィンドウで次のコマンドを入力します。

**kd-k com: パイプ、ポート = \\ \\ 。 \\パイプ \\ **<em>pipename</em>**、リセット = 0、再接続**

デバッガーから別の物理コンピューター上で実行されている仮想マシンをデバッグするには、コマンドプロンプトウィンドウで次のコマンドを入力します。

**kd-k com: パイプ、ポート = \\ \\ **<em>VMHost</em>** \\ パイプ \\ **<em>pipename</em>**、リセット = 0、再接続**

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>パラメータ


<span id="________VMHost"></span><span id="________vmhost"></span><span id="________VMHOST"></span>*VMHost*  
仮想マシンが実行されているコンピューターの名前を指定します。

<span id="PipeName_______"></span><span id="pipename_______"></span><span id="PIPENAME_______"></span>*PipeName*   
仮想マシンで作成したパイプの名前を指定します。

<span id="resets_0"></span><span id="RESETS_0"></span>**リセット = 0**  
ホストとターゲットが同期しているときに、無制限の数のリセットパケットをターゲットに送信できることを指定します。 Microsoft Virtual PC の場合は "**リセット = 0** " パラメーターを使用し、パイプを使用して余分なバイト数を削除する場合はその他の仮想マシンを使用します。 このパラメーターは、余分なバイトをすべて削除しないようにする、VMware またはその他の仮想マシンに対して使用しないでください。

<span id="________reconnect"></span><span id="________RECONNECT"></span>*再接続*  
読み取り/書き込みエラーが発生した場合に、デバッガーによって自動的に切断され、パイプが再接続されます。 また、デバッガーの起動時にデバッガーが名前付きパイプを見つけられない場合は、 *reconnect*パラメーターを指定すると、 *pipename*という名前のパイプが表示されるまでデバッガーが待機します。 コンピューターの再起動中にパイプを破棄して再作成する、Virtual PC およびその他の仮想マシンに*再接続*を使用します。 このパラメーターは、コンピューターの再起動時に、そのパイプを保持する VMware または他の仮想マシンには使用しないでください。

その他のコマンドラインオプションの詳細については、「 [**KD のコマンド**](kd-command-line-options.md)ラインオプション」または「 [**WinDbg コマンドラインオプション**](windbg-command-line-options.md)」を参照してください。

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


3. デバッガーがアタッチされて実行されたら、vm を停止してコールドスタートし、VM の COM ポートをアクティブ化します。エミュレートされた UART は、少なくとも1つのがパイプ名を使用して構成されていて、ホット追加できない場合を除き、デバッグには使用できません。

4. 構成の変更の更新が完了したら、セキュアブートを再度有効にします。

第2世代の Vm の詳細については、「[第2世代仮想マシンの概要](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/dn282285(v=ws.11))」を参照してください。


## <a name="span-idremarksspanspan-idremarksspanspan-idremarksspanremarks"></a><span id="Remarks"></span><span id="remarks"></span><span id="REMARKS"></span>注釈


対象のコンピュータが応答を停止した場合でも、以前のカーネルデバッグ操作のために対象のコンピュータが停止した場合、または **-b** [コマンドラインオプション](command-line-options.md)を使用した場合、デバッガーは直ちに対象のコンピュータに中断します。

それ以外の場合、対象のコンピューターは、デバッガーがブレークする順序になるまで実行を続けます。


## <a name="span-idfirewallsspantroubleshooting-firewalls-and-network-access-issues"></a><span id="Firewalls"></span>ファイアウォールとネットワークアクセスの問題のトラブルシューティング

デバッガー (WinDbg または KD) は、ファイアウォール経由でアクセスできる必要があります。 これは、ネットワークアダプターでサポートされている仮想シリアルポートにも当てはまります。

デバッガーの読み込み時に Windows からファイアウォールをオフにするように求めるメッセージが表示された場合は、3つすべてのボックスをオンにします。

使用中の VM の詳細に応じて、仮想マシンのネットワーク設定を変更して、Microsoft カーネルネットワークデバッグアダプターにブリッジすることが必要になる場合があります。 そうしないと、仮想マシンはネットワークにアクセスできなくなります。

**Windows ファイアウォール**

コントロールパネルを使用して、Windows ファイアウォールを経由したアクセスを許可できます。 コントロールパネルを開き > システムとセキュリティ] をクリックし、[Windows ファイアウォールを介したアプリの許可] を選択します。 アプリケーションの一覧で、 *WINDOWS GUI のシンボリックデバッガー*と*windows カーネルデバッガー*を見つけます。 この2つのアプリケーションをファイアウォールで許可するには、このチェックボックスを使用します。 デバッグアプリケーション (WinDbg または KD) を再起動します。


## <a name="span-idthird_party_vmsspanthird-party-vms"></a><span id="Third_Party_VMs"></span>サードパーティの Vm

**VMWare**   VMWare 機能 (リセットボタンなど) を使用して仮想マシンを再起動した場合は、WinDbg を終了し、WinDbg を再起動してデバッグを続行します。 バーチャルマシンのデバッグ中、VMWare は多くの場合、CPU の100% を消費します。

 

## <a name="span-idrelated_topicsspanrelated-topics"></a><span id="related_topics"></span>関連トピック

[KDNET を使用した仮想マシンのネットワークデバッグの設定](setting-up-network-debugging-of-a-virtual-machine-host.md)

[カーネル モードのデバッグを手動でセットアップする](setting-up-kernel-mode-debugging-in-windbg--cdb--or-ntsd.md)

[バーチャルマシンホストのネットワークデバッグの設定](setting-up-network-debugging-of-a-virtual-machine-host.md)
 







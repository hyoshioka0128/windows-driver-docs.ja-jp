---
title: カーネル モード デバッグのセットアップ、仮想マシン手動で仮想 COM ポートを使用しての
description: デバッグ ツールの Windows の仮想 COM ポートを使用して仮想マシンのカーネル デバッグをサポートします。
ms.assetid: e863e664-8338-4bbe-953b-e000a6843db9
keywords:
- 仮想マシンのデバッグ
- 仮想 PC のデバッグ
- VMware のデバッグ
ms.date: 05/30/2018
ms.localizationpriority: medium
ms.openlocfilehash: f29242c1042805498cca354902c415ff8485796f
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56531302"
---
# <a name="setting-up-kernel-mode-debugging-of-a-virtual-machine-manually-using-a-virtual-com-port"></a>カーネル モード デバッグのセットアップ、仮想マシン手動で仮想 COM ポートを使用しての

デバッグ ツールの Windows 仮想マシンのカーネルのデバッグをサポートします。 仮想マシンは、デバッガーと同じ物理コンピューターまたは同じネットワークに接続されている別のコンピューターに配置できます。 このトピックでは、KDCOM を介して仮想 COM ポートを使用して手動で仮想マシンのデバッグを設定する方法について説明します。

KDNET を使用して仮想ネットワークを高速なオプションはお勧めします。 詳細については、次を参照してください。[ネットワーク デバッグのセットアップ KDNET で仮想マシンの](setting-up-network-debugging-of-a-virtual-machine-host.md)します。


## <a name="span-idsettingupthetargetvirtualmachinespanspan-idsettingupthetargetvirtualmachinespanspan-idsettingupthetargetvirtualmachinespansetting-up-the-target-virtual-machine"></a><span id="Setting_Up_the_Target_Virtual_Machine"></span><span id="setting_up_the_target_virtual_machine"></span><span id="SETTING_UP_THE_TARGET_VIRTUAL_MACHINE"></span>ターゲットの仮想マシンの設定

デバッガーを実行しているコンピューターが呼び出されます、*ホスト コンピューター*、デバッグ中の仮想マシンを呼び出すと、*ターゲット仮想マシン*します。

> [!IMPORTANT]
> BCDEdit を使用してブート情報を変更する前に、テスト用のコンピューターの BitLocker とセキュア ブートなどの Windows セキュリティ機能を一時的に中断する必要があります。
> テストが完了すると、これらのセキュリティ機能を再度有効にし、適切なセキュリティ機能を無効にするテスト PC を管理します。

1. 管理者特権のコマンド プロンプト ウィンドウで、仮想マシンでは、次のコマンドを入力します。

   **bcdedit /debug on**

   **bcdedit/dbgsettings シリアル debugport:**<em>n</em> **baudrate:115200**

   場所*n*は仮想マシン上の COM ポートの数です。

2. 仮想マシンでは、名前付きパイプにマップする COM ポートを構成します。 デバッガーは、このパイプを使用して接続されます。 このパイプを作成する方法の詳細については、仮想マシンのドキュメントを参照してください。

3. デバッガーがアタッチされ実行されていると、対象のコンピューターを再起動します。


## <a name="span-idstartingthedebuggerspanspan-idstartingthedebuggerspanstarting-the-debugging-session-using-windbg"></a><span id="starting_the_debugger"></span><span id="STARTING_THE_DEBUGGER"></span>WinDbg を使用してデバッグ セッションの開始

ホスト コンピューターでは、WinDbg を開きます。 **ファイル**] メニューの [選択**カーネル デバッグ**します。 カーネル デバッグ ダイアログ ボックスで、開く、 **COM**タブ。チェック、**パイプ**ボックスし、チェック、**再接続**ボックス。 **ボー レート**115200 を入力します。 **リセット**0 を入力します。

デバッガーが、仮想マシンと同じコンピューターで実行している場合、次の入力**ポート**します。

**\\\\.\\パイプ\\**<em>PipeName</em>します。

デバッガーが、仮想マシンから別のコンピューターで実行している場合、次の入力**ポート**します。

**\\\\**<em>VMHost</em>**\\pipe\\**<em>PipeName</em>

**[OK]** をクリックします。

コマンドラインで、WinDbg を開始することもできます。 デバッガーが、仮想マシンと同じ物理コンピューターで実行している場合は、コマンド プロンプト ウィンドウで、次のコマンドを入力します。

**windbg -k com:pipe,port=\\\\.\\pipe\\**<em>PipeName</em>**,resets=0,reconnect**

デバッガーが、仮想マシンから別の物理コンピューターで実行している場合は、コマンド プロンプト ウィンドウで、次のコマンドを入力します。

**windbg -k com:pipe,port=\\\\**<em>VMHost</em>**\\pipe\\**<em>PipeName</em>**,resets=0,reconnect**

## <a name="span-idstartingthedebuggingsessionusingkdspanspan-idstartingthedebuggingsessionusingkdspanspan-idstartingthedebuggingsessionusingkdspanstarting-the-debugging-session-using-kd"></a><span id="Starting_the_Debugging_Session_Using_KD"></span><span id="starting_the_debugging_session_using_kd"></span><span id="STARTING_THE_DEBUGGING_SESSION_USING_KD"></span>KD を使用してデバッグ セッションの開始


デバッガーと同じ物理コンピューターで実行されている仮想マシンをデバッグするには、コマンド プロンプト ウィンドウで、次のコマンドを入力します。

**kd-k com:pipe、ポート =\\\\.\\パイプ\\**<em>PipeName</em>**、リセット = 0、再接続**

デバッガーから別の物理コンピューターで実行されている仮想マシンをデバッグするには、コマンド プロンプト ウィンドウで、次のコマンドを入力します。

**kd-k com:pipe、ポート =\\\\**<em>VMHost</em>**\\パイプ\\**<em>PipeName</em> **、リセット = 0、再接続**

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>パラメーター


<span id="________VMHost"></span><span id="________vmhost"></span><span id="________VMHOST"></span> *VMHost*  
仮想マシンが実行されているコンピューターの名前を指定します。

<span id="PipeName_______"></span><span id="pipename_______"></span><span id="PIPENAME_______"></span>*PipeName*   
仮想マシンで作成した、パイプの名前を指定します。

<span id="resets_0"></span><span id="RESETS_0"></span>**resets=0**  
ホストとターゲットを同期するときに、リセット パケットの数に制限はありませんをターゲットに送信できることを指定します。 使用して、**リセット = 0** Microsoft Virtual PC と他の仮想マシンがパイプ余分のバイトを削除するパラメーター。 このパラメーターは、VMware、または他の仮想マシンのすべての余分なバイトを削除しないをパイプを使わないでください。

<span id="________reconnect"></span><span id="________RECONNECT"></span> *reconnect*  
原因のデバッガーが自動的に切断し、読み取り/書き込みエラーが発生した場合は、パイプを再接続します。 さらに、デバッガーが開始されると、デバッガーが名前付きパイプを見つけられない場合、*再接続*パラメーターによって、デバッガーは、名前付きパイプを待機する*PipeName*を表示します。 使用*再接続*Virtual PC とを破棄し、コンピューターの中に、パイプを再作成する他の仮想マシンを再起動します。 このパラメーターは、VMware、またはコンピューターの再起動中に、パイプを保持している他の仮想マシンを使わないでください。

追加のコマンド ライン オプションの詳細については、次を参照してください[ **KD コマンド ライン オプション**](kd-command-line-options.md)または[ **WinDbg コマンド ライン オプション**](windbg-command-line-options.md) .

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


3. デバッガーがアタッチされ実行されていると、停止およびコールドは、VM 内の COM ポートをアクティブ化する VM を起動します。　エミュレートされた UART をしない限り、少なくとも 1 つは実際に設定されたパイプ名を使用して、ホット追加することはできませんをデバッグするため使用できません。

4. 再度有効にするセキュリティで保護された boot が完了したら、構成の変更を更新します。

第 2 世代 Vm の詳細については、次を参照してください。[第 2 世代仮想マシン概要](https://go.microsoft.com/fwlink/p/?Linkid=331326)します。


## <a name="span-idremarksspanspan-idremarksspanspan-idremarksspanremarks"></a><span id="Remarks"></span><span id="remarks"></span><span id="REMARKS"></span>「解説」


ターゲット コンピューターが応答しなくなった、デバッグ アクションでは、以前のカーネルのため、ターゲット コンピューターが停止しても、または使用した場合、 **-b** [コマンド ライン オプション](command-line-options.md)、デバッガーは中断しますターゲット コンピューターですぐにします。

それ以外の場合、ターゲット コンピューターでは、デバッガーの注文を解除するまで実行が続行されます。


## <a name="span-idfirewallsspantroubleshooting-firewalls-and-network-access-issues"></a><span id="Firewalls"></span>ファイアウォールとネットワーク アクセスの問題のトラブルシューティング

デバッガー (WinDbg または KD) ファイアウォール経由のアクセスが必要です。 ネットワーク アダプターでサポートされている仮想シリアル ポートの場合、このこともできます。

デバッガーが読み込まれるときに、ファイアウォールを無効にする Windows によって求められたら、次の 3 つのすべてのボックスを選択します。

使用中の VM の詳細、によっては、それらをカーネル ネットワーク デバッグ アダプターをブリッジする、仮想マシンのネットワーク設定を変更する必要があります。 それ以外の場合、仮想マシンには、ネットワークへのアクセスはありません。

**Windows ファイアウォール**

コントロール パネルを使用して、Windows ファイアウォール経由のアクセスを許可することができます。 コントロール パネルを開き > Windows ファイアウォールを介してアプリを許可するシステムとセキュリティ、および選択します。 アプリケーションの一覧で探します*Windows GUI のシンボリック デバッガー*と*Windows カーネル デバッガー*します。 これら 2 つのアプリケーション、ファイアウォールを通過を許可するのにチェック ボックスを使用します。 デバッグ (WinDbg または KD) アプリケーションを再起動します。


## <a name="span-idthirdpartyvmsspanthird-party-vms"></a><span id="Third_Party_VMs"></span>サード パーティ製の Vm

**VMWare**    VMWare の機能 (たとえば、リセット ボタン) を使用して、仮想マシンを再起動する場合は、WinDbg を終了し、デバッグを継続する WinDbg を再起動します。 仮想マシンは、デバッグ時に VMWare は多くの場合、CPU を 100% を消費します。

 

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>関連トピック

[ネットワークが KDNET で仮想マシンのデバッグの設定](setting-up-network-debugging-of-a-virtual-machine-host.md)

[カーネル モードのデバッグを手動での設定](setting-up-kernel-mode-debugging-in-windbg--cdb--or-ntsd.md)

[バーチャル マシン ホストのネットワークのデバッグの設定](setting-up-network-debugging-of-a-virtual-machine-host.md)
 







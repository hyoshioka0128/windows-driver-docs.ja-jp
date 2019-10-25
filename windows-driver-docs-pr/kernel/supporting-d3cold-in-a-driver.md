---
title: ドライバーでの D3cold のサポート
description: Windows 8 以降では、D3 (オフ) デバイスの電源状態は、D3hot と D3cold という2つの異なる下位互換性に分割されています。
ms.assetid: D085820E-EDAC-4353-8500-207F77D9CC1F
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: e671878716ef77dd37903ef53e7f41ed57c20d2d
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72836225"
---
# <a name="supporting-d3cold-in-a-driver"></a>ドライバーでの D3cold のサポート


Windows 8 以降では、D3 (オフ) デバイスの電源状態は、D3hot と D3cold という2つの異なる下位互換性に分割されています。 D3 は、電力が最も低いデバイスの電源状態であり、D3cold は D3 の低電力の下位レベルです。 アイドル状態のデバイスを D3cold 下位下に移動すると、電力消費が減少し、モバイルハードウェアプラットフォームをバッテリ料金で実行できる時間が長くなります。

D3hot では、ほとんどの場合、デバイスはオフになっています。 ただし、デバイスはメインの電源から切断されていないため、親バスコントローラーはバス上のデバイスの存在を検出できます。 D3cold では、メインの電源がデバイスから削除され、バスコントローラーはデバイスの存在を検出できません。 詳細については、「[デバイスの低電力状態](device-sleeping-states.md)の D3hot と D3cold」の説明を参照してください。

以前のバージョンの Windows では、D3 デバイスの電源状態は暗黙的に D3hot と D3cold の下位の部分に分割されていますが、コンピューターが S0 システムの電源状態を終了する準備をしているときに、S1 ~ S4 のスリープ状態のいずれかを入力しない限り、デバイスは D3cold に入ることができません。 コンピューターが S0 にとどまるときにデバイスが入力できる低電力の Dx 状態は、D1 から D3hot までに制限されます。

Windows 8 は、コンピューターが S0 で、スリープ状態に入る準備ができていない場合に、デバイスの電源状態の D3cold の下位状態への移行をサポートするための Windows の最初のバージョンです。 このように D3cold をサポートするデバイスは、次の方法で電力を節約するのに役立ちます。

-   デバイスは、他の低電力の Dx 状態よりも D3cold の電力消費量が少なくなります。
-   このデバイスが他のデバイスとバスを共有し、これらのすべてのデバイスが D3cold をサポートしている場合、バス上のすべてのデバイスが D3cold を入力すると、バスコントローラーは低電力の Dx 状態になる可能性があります。
-   このデバイスが他のデバイスと電源を共有し、これらのすべてのデバイスが D3cold をサポートしている場合、これらのデバイスの最後に D3hot が入力されると、電源を取り外すことができます。このとき、これらのデバイスはすべて D3cold になります。

逆に、D3cold でアイドル状態にならないデバイスは、他のデバイスが D3cold やその他の低電力の Dx 状態を入力するのを防ぐことができます。

次のトピックには、デバイスドライバーでの D3cold のサポートに関する詳細情報が含まれています。

## <a name="in-this-section"></a>このセクションの内容


<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>トピック</th>
<th>説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><a href="enabling-transitions-to-d3cold.md" data-raw-source="[Enabling Transitions to D3cold](enabling-transitions-to-d3cold.md)">D3cold への移行を有効にする</a></p></td>
<td><p>すべてのバージョンの Windows では、コンピューターのスリープ中にデバイスを D3cold にすることができます (システムの低電力状態 S1 ~ S4)。 コンピューターが S0 を終了する前に、関数ドライバー、バスドライバー、およびフィルタードライバーが連携して、デバイスを D3hot に移動します。 コンピューターが低電力の Sx 状態になると、この移行は、デバイスを D3hot から D3cold に移動する副作用になります。</p></td>
</tr>
<tr class="even">
<td><p><a href="d3cold-capabilities-of-a-device.md" data-raw-source="[D3cold Capabilities of a Device](d3cold-capabilities-of-a-device.md)">デバイスの D3cold 機能</a></p></td>
<td><p>デバイスの電源ポリシー所有者 (PPO) であるドライバーがデバイスを D3cold に入力できるようにするには (コンピューターが S0 のままになっている場合)、ドライバーはデバイスの応答性が高く、デバイスが D3cold に入った後も正常に動作し続けることを確認する必要があります。</p></td>
</tr>
<tr class="odd">
<td><p><a href="using-guid-d3cold-support-interface.md" data-raw-source="[Using the GUID_D3COLD_SUPPORT_INTERFACE Driver Interface](using-guid-d3cold-support-interface.md)">GUID_D3COLD_SUPPORT_INTERFACE Driver インターフェイスの使用</a></p></td>
<td><p>Windows 8 以降では、ドライバーは<a href="https://msdn.microsoft.com/library/windows/hardware/hh967714" data-raw-source="[GUID_D3COLD_SUPPORT_INTERFACE](https://msdn.microsoft.com/library/windows/hardware/hh967714)">GUID_D3COLD_SUPPORT_INTERFACE</a>インターフェイスのルーチンを呼び出して、デバイスの D3COLD 機能を判別し、これらのデバイスで D3COLD を使用できるようにします。 このインターフェイスの2つの主なルーチンは、 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-set_d3cold_support" data-raw-source="[&lt;em&gt;SetD3ColdSupport&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-set_d3cold_support)"><em>SetD3ColdSupport</em></a>と<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-get_idle_wake_info" data-raw-source="[&lt;em&gt;GetIdleWakeInfo&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-get_idle_wake_info)"><em>GetIdleWakeInfo</em></a>です。</p></td>
</tr>
<tr class="even">
<td><p><a href="surprise-wake-up.md" data-raw-source="[Surprise Wake-Up](surprise-wake-up.md)">突然のウェイクアップ</a></p></td>
<td><p>突然のウェイクアップは、D0 への予期しない移行です。 デバイスが D3cold になると、同じ電源レール上の別のデバイスのドライバーが D3cold から D0 への移行を要求したときの副作用として、突然ウェイクアップが発生する可能性があります。 最初のデバイスのドライバーは、デバイスが初期化されていない D0 状態のままにならないように、突然ウェイクアップの通知を受け取る必要があります。</p></td>
</tr>
</tbody>
</table>

 

 

 





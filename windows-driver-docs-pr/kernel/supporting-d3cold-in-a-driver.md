---
title: ドライバーで D3cold のサポート
description: Windows 8 以降、(オフ) デバイスの電源状態 D3 は D3hot と D3cold 2 つの異なる下位に分割されます。
ms.assetid: D085820E-EDAC-4353-8500-207F77D9CC1F
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 71bc176204f94c2be25ba71c0e2b7ecaf8a4e65c
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56536468"
---
# <a name="supporting-d3cold-in-a-driver"></a>ドライバーで D3cold のサポート


Windows 8 以降、(オフ) デバイスの電源状態 D3 は D3hot と D3cold 2 つの異なる下位に分割されます。 D3 が最も低い搭載デバイスの電源の状態と D3cold は、最も低いを利用した下位状態の D3 します。 下位 D3cold 状態にアイドル状態のデバイスの移動、電力消費量を削減し、モバイル ハードウェア プラットフォームは、バッテリの充電で実行できる時間を拡張できます。

D3hot、デバイスはオフにほとんどの場合。 ただし、デバイスは、メイン電源から切断されません、親バス コント ローラーは、バス上のデバイスの存在を検出できます。 D3cold では、主電源は、デバイスから削除され、バス コント ローラーは、デバイスの存在を検出できません。 詳細については、D3hot および D3cold での説明を参照してください。[デバイス低電力状態](device-sleeping-states.md)します。

以前のバージョンの Windows では、下位に、D3 デバイスの電源の状態は暗黙的に D3hot と D3cold に分割しますが、コンピューターの準備を S0 システム電源の状態を終了し、S1 S4 からのスリープ状態のいずれかを入力しない限り、デバイスは D3cold を入力ことはできません。 デバイスがコンピューターの S0 内に存続するときに入力できる低電力 Dx 状態は、D1 ~ D3hot に制限されます。

Windows 8 は、コンピューターは、S0 があり、スリープ状態を入力する準備をしてはいない D3cold 下位状態にデバイスの電源状態の遷移をサポートするために Windows の最初のバージョンです。 この方法で D3cold をサポートするデバイスは、次の方法で電力の節約に役立ちます。

-   デバイスは、その他の低電力 Dx 状態よりも D3cold で電力を消費します。
-   このデバイスを共有する場合、バスの他のデバイスでは、およびこれらすべてのデバイス サポート D3cold、し、結局、バス上のデバイス D3cold をバス コント ローラーは低電力 Dx の状態を入力します。
-   このデバイスが他のデバイスに電源を共有し、これらすべてのデバイスをサポートして D3cold 場合、し、これらのデバイスの最後に入る D3hot、電源を削除できます、時点で、これらすべてのデバイスは連動 D3cold を入力します。

逆に、D3cold でアイドル状態のことはできませんが、デバイスには、D3cold または他の低電力 Dx 状態に入るを他のデバイスができないようにすることができます。

次のトピックには、D3cold をデバイス ドライバーのサポートに関する詳細が含まれます。

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
<td><p><a href="enabling-transitions-to-d3cold.md" data-raw-source="[Enabling Transitions to D3cold](enabling-transitions-to-d3cold.md)">D3cold への切り替えを有効にします。</a></p></td>
<td><p>Windows のすべてのバージョンでは、D3cold にする (S1 S4 から、システム低電力状態のいずれか) で、コンピューターがスリープ状態中にデバイスを有効にします。 コンピューターでは、S0 が終了する前に関数ドライバー、バス ドライバー、およびフィルター ドライバー連携 D3hot にデバイスを移動します。 コンピューターが省電力 Sx 状態になったときこの遷移副作用 D3cold D3hot からデバイスに移動します。</p></td>
</tr>
<tr class="even">
<td><p><a href="d3cold-capabilities-of-a-device.md" data-raw-source="[D3cold Capabilities of a Device](d3cold-capabilities-of-a-device.md)">デバイスの D3cold 機能</a></p></td>
<td><p>D3cold (コンピューターの S0 内に存続するとき) を入力するデバイスは、デバイスの電源ポリシー所有者 (PPO) である、ドライバーは可能前に、ドライバーは、デバイスが応答および D3cold を入力すると、デバイスが正しく動作しているに確認する必要があります。</p></td>
</tr>
<tr class="odd">
<td><p><a href="using-guid-d3cold-support-interface.md" data-raw-source="[Using the GUID_D3COLD_SUPPORT_INTERFACE Driver Interface](using-guid-d3cold-support-interface.md)">GUID_D3COLD_SUPPORT_INTERFACE ドライバー インターフェイスを使用します。</a></p></td>
<td><p>Windows 8 以降、ドライバーで呼び出すことが、ルーチン、 <a href="https://msdn.microsoft.com/library/windows/hardware/hh967714" data-raw-source="[GUID_D3COLD_SUPPORT_INTERFACE](https://msdn.microsoft.com/library/windows/hardware/hh967714)">GUID_D3COLD_SUPPORT_INTERFACE</a>インターフェイス D3cold を使用して、これらのデバイスを有効にしてデバイスの D3cold 機能を判断します。 このインターフェイスで 2 つの主なルーチンは<a href="https://msdn.microsoft.com/library/windows/hardware/hh967716" data-raw-source="[&lt;em&gt;SetD3ColdSupport&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/hh967716)"> <em>SetD3ColdSupport</em> </a>と<a href="https://msdn.microsoft.com/library/windows/hardware/hh967712" data-raw-source="[&lt;em&gt;GetIdleWakeInfo&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/hh967712)"> <em>GetIdleWakeInfo</em></a>します。</p></td>
</tr>
<tr class="even">
<td><p><a href="surprise-wake-up.md" data-raw-source="[Surprise Wake-Up](surprise-wake-up.md)">驚きのウェイク アップ</a></p></td>
<td><p>驚きのウェイク アップでは、D0 に予期しない移行です。 デバイス D3cold を入力すると、同じ power レール上の別のデバイスのドライバー D3cold から D0 への遷移を要求するときに副作用として突然のウェイク アップが発生があります。 最初のデバイス ドライバーは、デバイスが初期化されていない d0 に残っていることを防ぐために、突然のウェイク アップの通知を受け取る必要があります。</p></td>
</tr>
</tbody>
</table>

 

 

 





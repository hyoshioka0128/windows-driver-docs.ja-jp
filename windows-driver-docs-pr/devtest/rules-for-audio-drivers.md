---
title: オーディオ ドライバーの規則
description: オーディオ (PortCls) ミニポート ドライバーの DDI 準拠規則は、PortCls.sys とそのミニポート ドライバー間 DDI インターフェイスを確認します。
ms.assetid: 65078F78-B7F2-41A7-BD3B-A90A4A77750F
ms.date: 05/21/2018
ms.localizationpriority: medium
ms.openlocfilehash: fa0774238702c8f0a42047e07392dc865104179f
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67353882"
---
# <a name="rules-for-audio-drivers"></a>オーディオ ドライバーの規則


オーディオ (PortCls) ミニポート ドライバーの DDI 準拠規則は、PortCls.sys とそのミニポート ドライバー間 DDI インターフェイスを確認します。

## <a name="in-this-section"></a>このセクションの内容


<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">トピック</th>
<th align="left">説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><a href="audio-pcaddadapterdevice.md" data-raw-source="[&lt;strong&gt;PcAddAdapterDevice&lt;/strong&gt;](audio-pcaddadapterdevice.md)"><strong>PcAddAdapterDevice</strong></a></p></td>
<td align="left"><p>PcAddAdapterDevice ルールでは、PortCls ミニポート ドライバーが正しく使用を指定します、 <a href="audio-pcaddadapterdevice.md" data-raw-source="[&lt;strong&gt;PcAddAdapterDevice&lt;/strong&gt;](audio-pcaddadapterdevice.md)"> <strong>PcAddAdapterDevice</strong> </a>を具体的には、関数、 <em>DeviceExtensionSize</em>ゼロ (0) か、ありません PORT_CLASS_DEVICE_EXTENSION_SIZE 未満にする必要があります。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="audio-pcallocateandmappages.md" data-raw-source="[&lt;strong&gt;PcAllocateAndMapPages&lt;/strong&gt;](audio-pcallocateandmappages.md)"><strong>PcAllocateAndMapPages</strong></a></p></td>
<td align="left"><p>PortCls ミニポート ドライバーが、正しいパラメーターを使用して、次のインターフェイスを呼び出す PcAllocateAndMapPages ルールを指定します。</p>
<ul>
<li>IPortWaveRTStream::AllocatePagesForMdl</li>
<li>IPortWaveRTStream::AllocateContiguousPagesForMdl</li>
<li>IPortWaveRTStream::MapAllocatedPages</li>
</ul></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="audio-pcallocatedpages.md" data-raw-source="[&lt;strong&gt;PcAllocatedPages&lt;/strong&gt;](audio-pcallocatedpages.md)"><strong>PcAllocatedPages</strong></a></p></td>
<td align="left"><p>PcAllocatedPages ルールでは、PortCls ミニポート ドライバーが AllocatePagesForMdl または AllocateContiguousPagesForMdl メソッドを呼び出して、以前割り当てられたページを解放することを指定します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="audio-pcirqlddis.md" data-raw-source="[&lt;strong&gt;PcIrqlDDIs&lt;/strong&gt;](audio-pcirqlddis.md)"><strong>PcIrqlDDIs</strong></a></p></td>
<td align="left"><p>PcIrqlDDIs ルールでは、ある PortCls ミニポート ドライバー呼び出す必要があります PortCls Ddi 適切な IRQL でレベルを指定します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="audio-pcirqliport.md" data-raw-source="[&lt;strong&gt;PcIrqlIport&lt;/strong&gt;](audio-pcirqliport.md)"><strong>PcIrqlIport</strong></a></p></td>
<td align="left"><p>PcIrqlIport ルールでは、こと PortCls ミニポート ドライバー呼び出す必要があります PortCls IPort インターフェイスで適切な IRQL レベルを指定します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="pcporequestpowerirp.md" data-raw-source="[&lt;strong&gt;PcPoRequestPowerIrp&lt;/strong&gt;](pcporequestpowerirp.md)"><strong>PcPoRequestPowerIrp</strong></a></p></td>
<td align="left"><p>このルールは、PortCls ミニポート ドライバーを呼び出さないことを確認します。 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-porequestpowerirp" data-raw-source="[&lt;strong&gt;PoRequestPowerIrp&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-porequestpowerirp)"> <strong>PoRequestPowerIrp</strong> </a>で<a href="https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-set-power" data-raw-source="[&lt;strong&gt;IRP_MN_SET_POWER&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-set-power)"> <strong>IRP_MN_SET_POWER</strong></a>します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="audio-pcpropertyrequest.md" data-raw-source="[&lt;strong&gt;PcPropertyRequest&lt;/strong&gt;](audio-pcpropertyrequest.md)"><strong>PcPropertyRequest</strong></a></p></td>
<td align="left"><p>PcPropertyRequest ルールでは、PortCls ミニポート ドライバーが呼び出す必要がありますしないことを指定します、 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nf-portcls-pccompletependingpropertyrequest" data-raw-source="[&lt;strong&gt;PcCompletePendingPropertyRequest&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nf-portcls-pccompletependingpropertyrequest)"> <strong>PcCompletePendingPropertyRequest</strong> </a>で、 <em>NtStatus</em> status _ の値保留中です。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="audio-pcregisteradapterpower.md" data-raw-source="[&lt;strong&gt;PcRegisterAdapterPower&lt;/strong&gt;](audio-pcregisteradapterpower.md)"><strong>PcRegisterAdapterPower</strong></a></p></td>
<td align="left"><p>PortCls ミニポート ドライバーがしないで PcRegisterAdapterPower ルールを指定します。</p>
<ul>
<li>呼び出す<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nf-portcls-pcregisteradapterpowermanagement" data-raw-source="[&lt;strong&gt;PcRegisterAdapterPowerManagement&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nf-portcls-pcregisteradapterpowermanagement)"> <strong>PcRegisterAdapterPowerManagement</strong> </a>を呼び出さなくても 2 回<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nf-portcls-pcunregisteradapterpowermanagement" data-raw-source="[&lt;strong&gt;PcUnregisterAdapterPowerManagement&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nf-portcls-pcunregisteradapterpowermanagement)"> <strong>PcUnregisterAdapterPowerManagement</strong></a>します。</li>
<li>呼び出す<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nf-portcls-pcunregisteradapterpowermanagement" data-raw-source="[&lt;strong&gt;PcUnregisterAdapterPowerManagement&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nf-portcls-pcunregisteradapterpowermanagement)"> <strong>PcUnregisterAdapterPowerManagement</strong> </a>呼び出さず<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nf-portcls-pcregisteradapterpowermanagement" data-raw-source="[&lt;strong&gt;PcRegisterAdapterPowerManagement&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nf-portcls-pcregisteradapterpowermanagement)"> <strong>PcRegisterAdapterPowerManagement</strong> </a>最初。</li>
</ul></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="audio-pctimedwavertstreamsetstate.md" data-raw-source="[&lt;strong&gt;PcTimedWaveRtStreamSetState&lt;/strong&gt;](audio-pctimedwavertstreamsetstate.md)"><strong>PcTimedWaveRtStreamSetState</strong></a></p></td>
<td align="left"><p>PcTimedWaveRtStreamSetState ルールでは、ProtCls ミニポート ドライバーを使用して状態遷移は、ことを指定します<a href="https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff536756(v=vs.85)" data-raw-source="[&lt;strong&gt;IMiniportWaveRTStream::SetState&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff536756(v=vs.85))"> <strong>IMiniportWaveRTStream::SetState</strong> </a>必要な時間内で。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="audio-pcunmapallocatedpages.md" data-raw-source="[&lt;strong&gt;PcUnmapAllocatedPages&lt;/strong&gt;](audio-pcunmapallocatedpages.md)"><strong>PcUnmapAllocatedPages</strong></a></p></td>
<td align="left"><p>PcUnmapAllocatedPages ルールを使用することを指定します。</p>
<ul>
<li>PortCls ミニポート ドライバーは、最初解除せずに現在割り当てられて、MDL にマップされません。</li>
<li>PortCls ミニポート ドライバーを使用して解放する前にメモリの割り当てを解除、 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nn-portcls-iminiportwavertstream" data-raw-source="[IMiniportWaveRTStream](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nn-portcls-iminiportwavertstream)">IMiniportWaveRTStream</a>インターフェイス。</li>
</ul></td>
</tr>
</tbody>
</table>

 

 

 






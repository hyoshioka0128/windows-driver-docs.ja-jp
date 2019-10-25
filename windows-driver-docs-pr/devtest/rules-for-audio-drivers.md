---
title: オーディオドライバーの規則
description: オーディオ (PortCls) ミニポートドライバーの DDI コンプライアンス規則により、PortCls とそのミニポートドライバーの間の DDI インターフェイスが検証されます。
ms.assetid: 65078F78-B7F2-41A7-BD3B-A90A4A77750F
ms.date: 05/21/2018
ms.localizationpriority: medium
ms.openlocfilehash: 2180ee42e4469baabd03864495a1c905dd78284b
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72839327"
---
# <a name="rules-for-audio-drivers"></a>オーディオドライバーの規則


オーディオ (PortCls) ミニポートドライバーの DDI コンプライアンス規則により、PortCls とそのミニポートドライバーの間の DDI インターフェイスが検証されます。

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
<td align="left"><p>PcAddAdapterDevice ルールは、PortCls ミニポートドライバーが<a href="audio-pcaddadapterdevice.md" data-raw-source="[&lt;strong&gt;PcAddAdapterDevice&lt;/strong&gt;](audio-pcaddadapterdevice.md)"><strong>pcaddadapterdevice</strong></a>関数を正しく使用することを指定します。具体的には、 <em>deviceextensionsize</em>はゼロ (0) または PORT_CLASS_DEVICE_EXTENSION_SIZE 未満にする必要があります。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="audio-pcallocateandmappages.md" data-raw-source="[&lt;strong&gt;PcAllocateAndMapPages&lt;/strong&gt;](audio-pcallocateandmappages.md)"><strong>PcAllocateAndMapPages</strong></a></p></td>
<td align="left"><p>PcAllocateAndMapPages 規則は、正しいパラメーターを使用して、PortCls ミニポートドライバーが次のインターフェイスを呼び出すことを指定します。</p>
<ul>
<li>IPortWaveRTStream:: AllocatePagesForMdl</li>
<li>IPortWaveRTStream:: AllocateContiguousPagesForMdl</li>
<li>IPortWaveRTStream:: MapAllocatedPages</li>
</ul></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="audio-pcallocatedpages.md" data-raw-source="[&lt;strong&gt;PcAllocatedPages&lt;/strong&gt;](audio-pcallocatedpages.md)"><strong>PcAllocatedPages</strong></a></p></td>
<td align="left"><p>PcAllocatedPages 規則は、PortCls ミニポートドライバーが、Allocatepg Formdl または AllocateContiguousPagesForMdl メソッドを呼び出すことによって、以前に割り当てられたページを解放することを指定します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="audio-pcirqlddis.md" data-raw-source="[&lt;strong&gt;PcIrqlDDIs&lt;/strong&gt;](audio-pcirqlddis.md)"><strong>PcIrqlDDIs</strong></a></p></td>
<td align="left"><p>PcIrqlDDIs 規則は、PortCls ミニポートドライバーが正しい IRQL レベルで PortCls DDIs を呼び出す必要があることを指定します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="audio-pcirqliport.md" data-raw-source="[&lt;strong&gt;PcIrqlIport&lt;/strong&gt;](audio-pcirqliport.md)"><strong>PcIrqlIport</strong></a></p></td>
<td align="left"><p>PcIrqlIport 規則は、PortCls ミニポートドライバーが正しい IRQL レベルで PortCls IPort インターフェイスを呼び出す必要があることを指定します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="pcporequestpowerirp.md" data-raw-source="[&lt;strong&gt;PcPoRequestPowerIrp&lt;/strong&gt;](pcporequestpowerirp.md)"><strong>PcPoRequestPowerIrp</strong></a></p></td>
<td align="left"><p>このルールは、PortCls ミニポートドライバーが<a href="https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-set-power" data-raw-source="[&lt;strong&gt;IRP_MN_SET_POWER&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-set-power)"><strong>IRP_MN_SET_POWER</strong></a>を使用して<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-porequestpowerirp" data-raw-source="[&lt;strong&gt;PoRequestPowerIrp&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-porequestpowerirp)"><strong>PoRequestPowerIrp</strong></a>を呼び出すことができないことを確認します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="audio-pcpropertyrequest.md" data-raw-source="[&lt;strong&gt;PcPropertyRequest&lt;/strong&gt;](audio-pcpropertyrequest.md)"><strong>PcPropertyRequest</strong></a></p></td>
<td align="left"><p>PcPropertyRequest 規則は、PortCls ミニポートドライバーがありますの<em>NtStatus</em>値を持つ<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-pccompletependingpropertyrequest" data-raw-source="[&lt;strong&gt;PcCompletePendingPropertyRequest&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-pccompletependingpropertyrequest)"><strong>Pccompletependingpropertyrequest</strong></a>を呼び出さないことを指定します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="audio-pcregisteradapterpower.md" data-raw-source="[&lt;strong&gt;PcRegisterAdapterPower&lt;/strong&gt;](audio-pcregisteradapterpower.md)"><strong>アダプターパワー</strong></a></p></td>
<td align="left"><p>PcregiPortCls Adapterpower rule は、次のようにして、ミニミニポートドライバーが以下を実行しないように指定します。</p>
<ul>
<li><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-pcunregisteradapterpowermanagement" data-raw-source="[&lt;strong&gt;PcUnregisterAdapterPowerManagement&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-pcunregisteradapterpowermanagement)"><strong>Pcunregisteradapterpowermanagement</strong></a>の呼び出しを介在させずに、 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-pcregisteradapterpowermanagement" data-raw-source="[&lt;strong&gt;PcRegisterAdapterPowerManagement&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-pcregisteradapterpowermanagement)"><strong>pcregisteradapterpowermanagement</strong></a>を2回呼び出します。</li>
<li>最初に<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-pcregisteradapterpowermanagement" data-raw-source="[&lt;strong&gt;PcRegisterAdapterPowerManagement&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-pcregisteradapterpowermanagement)"><strong>Pcregisteradapterpowermanagement</strong></a>を呼び出さずに<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-pcunregisteradapterpowermanagement" data-raw-source="[&lt;strong&gt;PcUnregisterAdapterPowerManagement&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-pcunregisteradapterpowermanagement)"><strong>pcunregisteradapterpowermanagement</strong></a>を呼び出します。</li>
</ul></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="audio-pctimedwavertstreamsetstate.md" data-raw-source="[&lt;strong&gt;PcTimedWaveRtStreamSetState&lt;/strong&gt;](audio-pctimedwavertstreamsetstate.md)"><strong>PcTimedWaveRtStreamSetState</strong></a></p></td>
<td align="left"><p>PcTimedWaveRtStreamSetState 規則は、ProtCls ミニポートドライバーが、必要な時間内に<a href="https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff536756(v=vs.85)" data-raw-source="[&lt;strong&gt;IMiniportWaveRTStream::SetState&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff536756(v=vs.85))"><strong>IMiniportWaveRTStream:: SetState</strong></a>を介して状態遷移を行うことを指定します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="audio-pcunmapallocatedpages.md" data-raw-source="[&lt;strong&gt;PcUnmapAllocatedPages&lt;/strong&gt;](audio-pcunmapallocatedpages.md)"><strong>PcUnmapAllocatedPages</strong></a></p></td>
<td align="left"><p>PcUnmapAllocatedPages ルールでは、次のことを指定します。</p>
<ul>
<li>PortCls ミニポートドライバーは、最初にマップを解除せずに現在マップされている MDL をマップしません。</li>
<li>PortCls ミニポートドライバーは、 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nn-portcls-iminiportwavertstream" data-raw-source="[IMiniportWaveRTStream](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nn-portcls-iminiportwavertstream)">IMiniportWaveRTStream</a>インターフェイスを使用して解放する前に、メモリを解除します。</li>
</ul></td>
</tr>
</tbody>
</table>

 

 

 






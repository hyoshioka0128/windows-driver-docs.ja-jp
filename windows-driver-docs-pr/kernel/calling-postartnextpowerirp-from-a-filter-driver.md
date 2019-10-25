---
title: フィルター ドライバーからの PoStartNextPowerIrp の呼び出し
description: フィルター ドライバーからの PoStartNextPowerIrp の呼び出し
ms.assetid: 6005f107-8f90-4530-91c2-9f0947cacb0a
keywords:
- 電源 Irp WDK カーネル、PoStartNextPowerIrp
- PoStartNextPowerIrp
- フィルタードライバーの WDK 電源管理
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 59e86feb41a2a1dc34ef9cfdcfb15772b41341cf
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72837137"
---
# <a name="calling-postartnextpowerirp-from-a-filter-driver"></a>フィルター ドライバーからの PoStartNextPowerIrp の呼び出し


Windows Vista 以降では、 [**Postartnextpowerirp**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-postartnextpowerirp)を呼び出す必要はなく、このルーチンの呼び出しによって電源管理操作は実行されません。 ただし、Windows Server 2003、Windows XP、および Windows 2000 では、フィルタードライバーは、すべての[**IRP\_\_クエリ\_power**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-query-power)または\_irp に対して、電源要求[ **\_設定\_** ](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-set-power)されている場合に、 **postartnextpowerirp**を呼び出す必要があります。ドライバーが受け取る。 呼び出しが発生するタイミングは、次の表に示すように、要求の種類と、ドライバーが失敗するか要求を成功させるかによって異なります。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th>要求の種類</th>
<th>ドライバーが要求を成功させると、次の呼び出しが行われます。</th>
<th>ドライバーが要求に失敗した場合、次の呼び出しが行われます。</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>IRP_MN_QUERY_POWER</strong> (デバイスの電源状態)</p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-io_completion_routine" data-raw-source="[&lt;em&gt;IoCompletion&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-io_completion_routine)"><em>Iocompletion</em></a>ルーチンで、を返す直前。</p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch" data-raw-source="[&lt;em&gt;DispatchPower&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch)"><em>DispatchPower</em></a>ルーチンで、 <strong>IoCompleteRequest</strong>を呼び出す前。</p></td>
</tr>
<tr class="even">
<td><p><strong>IRP_MN_QUERY_POWER</strong> (システム電源の状態)</p></td>
<td><p><em>DispatchPower</em>ルーチンで、削除ロックを取得し、IRP スタックの場所を設定する前。</p></td>
<td><p><em>DispatchPower</em>ルーチンで、 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocompleterequest" data-raw-source="[&lt;strong&gt;IoCompleteRequest&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocompleterequest)"><strong>IoCompleteRequest</strong></a>を呼び出す前。</p></td>
</tr>
<tr class="odd">
<td><p><strong>IRP_MN_SET_POWER</strong> (デバイスの電源状態)</p></td>
<td><p><em>Iocompletion</em>ルーチンで、を返す直前。</p></td>
<td><p>許可しない。</p></td>
</tr>
<tr class="even">
<td><p><strong>IRP_MN_SET_POWER</strong> (システム電源の状態)</p></td>
<td><p><em>DispatchPower</em>ルーチンで、削除ロックを取得し、IRP スタックの場所を設定する前。</p></td>
<td><p>許可しない。</p></td>
</tr>
</tbody>
</table>

 

 

 





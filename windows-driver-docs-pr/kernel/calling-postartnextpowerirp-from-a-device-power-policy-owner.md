---
title: デバイス電源ポリシー オーナーからの PoStartNextPowerIrp の呼び出し
description: デバイス電源ポリシー オーナーからの PoStartNextPowerIrp の呼び出し
ms.assetid: 58576ff8-638e-4928-9a2d-337ac3f4d2d8
keywords:
- Irp WDK カーネル、PoStartNextPowerIrp を電源します。
- PoStartNextPowerIrp
- デバイスの電源ポリシー WDK カーネル
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3ae50f955a22e1a06951b2008fdc9307289abb17
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67385265"
---
# <a name="calling-postartnextpowerirp-from-a-device-power-policy-owner"></a>デバイス電源ポリシー オーナーからの PoStartNextPowerIrp の呼び出し





Windows Vista 以降、通話[ **PoStartNextPowerIrp** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-postartnextpowerirp)は必要ありませんし、このルーチンの呼び出しには電源管理操作は実行されません。 ただしで Windows Server 2003、Windows XP、および Windows 2000 では、電源ポリシーがデバイスを所有している関数ドライバー呼び出す必要があります**PoStartNextPowerIrp**に対して 1 回ごと[ **IRP\_MN\_クエリ\_POWER** ](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-query-power)または[ **IRP\_MN\_設定\_POWER** ](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-set-power)ドライバーが受信した要求。 呼び出しが発生したときは、要求とは、ドライバーの失敗または、要求が次の表は成功を収めるかどうかの種類によって異なります。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th>要求の種類</th>
<th>ドライバーには、要求が成功すると、呼び出しが発生します。</th>
<th>ドライバーには、要求が失敗した場合、呼び出しが発生します。</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>IRP_MN_QUERY_POWER</strong> (デバイスの電源の状態)</p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-io_completion_routine" data-raw-source="[&lt;em&gt;IoCompletion&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-io_completion_routine)"> <em>IoCompletion</em> </a>ルーチンを返す前に、すぐにします。</p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_dispatch" data-raw-source="[&lt;em&gt;DispatchPower&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_dispatch)"> <em>DispatchPower</em> </a>ルーチンを呼び出す前に<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iocompleterequest" data-raw-source="[&lt;strong&gt;IoCompleteRequest&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iocompleterequest)"> <strong>IoCompleteRequest</strong></a>します。</p></td>
</tr>
<tr class="even">
<td><p><strong>IRP_MN_QUERY_POWER</strong> (システム電源の状態)</p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-porequestpowerirp" data-raw-source="[&lt;strong&gt;PoRequestPowerIrp&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-porequestpowerirp)"> <strong>PoRequestPowerIrp</strong> </a>システム IRP を完了する前に、すぐに関連するデバイス、IRP のコールバック ルーチン。</p></td>
<td><p><em>DispatchPower</em>ルーチンを呼び出す前に<strong>IoCompleteRequest</strong>します。</p></td>
</tr>
<tr class="odd">
<td><p><strong>IRP_MN_SET_POWER</strong> (デバイスの電源の状態)</p></td>
<td><p><em>IoCompletion</em>ルーチンを返す前に、すぐにします。</p></td>
<td><p>許可されていません。</p></td>
</tr>
<tr class="even">
<td><p><strong>IRP_MN_SET_POWER</strong> (システム電源の状態)</p></td>
<td><p><strong>PoRequestPowerIrp</strong>システム IRP を完了する前に、すぐに関連するデバイス、IRP のコールバック ルーチン。</p></td>
<td><p>許可されていません。</p></td>
</tr>
</tbody>
</table>

 

 

 





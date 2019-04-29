---
title: フィルター ドライバーからの PoStartNextPowerIrp の呼び出し
description: フィルター ドライバーからの PoStartNextPowerIrp の呼び出し
ms.assetid: 6005f107-8f90-4530-91c2-9f0947cacb0a
keywords:
- Irp WDK カーネル、PoStartNextPowerIrp を電源します。
- PoStartNextPowerIrp
- フィルター ドライバー WDK の電源管理
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3db70e6b8800be6242c9b65ccb7a732ca290b594
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63338603"
---
# <a name="calling-postartnextpowerirp-from-a-filter-driver"></a>フィルター ドライバーからの PoStartNextPowerIrp の呼び出し


Windows Vista 以降、通話[ **PoStartNextPowerIrp** ](https://msdn.microsoft.com/library/windows/hardware/ff559776)は必要ありませんし、このルーチンの呼び出しには電源管理操作は実行されません。 ただしで Windows Server 2003、Windows XP、および Windows 2000 では、フィルター ドライバーを呼び出す必要があります**PoStartNextPowerIrp**に対して 1 回ごと[ **IRP\_MN\_クエリ\_電源** ](https://msdn.microsoft.com/library/windows/hardware/ff551699)または[ **IRP\_MN\_設定\_POWER** ](https://msdn.microsoft.com/library/windows/hardware/ff551744)ドライバーが受信した要求。 呼び出しが発生したときは、要求とは、ドライバーの失敗または、要求が次の表は成功を収めるかどうかの種類によって異なります。

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
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff548354" data-raw-source="[&lt;em&gt;IoCompletion&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff548354)"> <em>IoCompletion</em> </a>ルーチンを返す前に、すぐにします。</p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_dispatch" data-raw-source="[&lt;em&gt;DispatchPower&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_dispatch)"> <em>DispatchPower</em> </a>ルーチンを呼び出す前に<strong>IoCompleteRequest</strong>します。</p></td>
</tr>
<tr class="even">
<td><p><strong>IRP_MN_QUERY_POWER</strong> (システム電源の状態)</p></td>
<td><p><em>DispatchPower</em>ルーチンと IRP スタックの場所を設定する前に削除ロックの取得後にします。</p></td>
<td><p><em>DispatchPower</em>ルーチンを呼び出す前に<a href="https://msdn.microsoft.com/library/windows/hardware/ff548343" data-raw-source="[&lt;strong&gt;IoCompleteRequest&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff548343)"> <strong>IoCompleteRequest</strong></a>します。</p></td>
</tr>
<tr class="odd">
<td><p><strong>IRP_MN_SET_POWER</strong> (デバイスの電源の状態)</p></td>
<td><p><em>IoCompletion</em>ルーチンを返す前に、すぐにします。</p></td>
<td><p>許可しない。</p></td>
</tr>
<tr class="even">
<td><p><strong>IRP_MN_SET_POWER</strong> (システム電源の状態)</p></td>
<td><p><em>DispatchPower</em>ルーチンと IRP スタックの場所を設定する前に削除ロックの取得後にします。</p></td>
<td><p>許可しない。</p></td>
</tr>
</tbody>
</table>

 

 

 





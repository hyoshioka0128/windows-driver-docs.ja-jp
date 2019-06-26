---
title: NDIS_STATUS_PM_WAKE_REASON
description: NDIS_STATUS_PM_WAKE_REASON 状態の表示は、ネットワーク アダプターによって生成されたウェイク アップ イベントに関する情報を提供します。
ms.assetid: 0CF29C9B-4AAA-473D-A3E8-C1E9530B595E
ms.date: 07/18/2017
keywords:
- NDIS_STATUS_PM_WAKE_REASON ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: 703c2246cea170e800cd487439e92605570bc6d5
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67368524"
---
# <a name="ndisstatuspmwakereason"></a>NDIS\_状態\_PM\_WAKE\_理由


**NDIS\_状態\_PM\_WAKE\_理由**状態を示す値が、ネットワーク アダプターによって生成されたウェイク アップ イベントに関する情報を提供します。

<a name="remarks"></a>注釈
-------

NDIS 6.30 以降、ミニポート ドライバーの問題の NDIS 状態を示す値**NDIS\_状態\_PM\_WAKE\_理由**します。 この状態表示には、NDIS およびネットワーク アダプターによって生成されたウェイク アップ イベントの理由についての上にあるドライバーに通知します。

ミニポート ドライバーでは、この種類の状態を示す値をサポートする場合、ミニポート ドライバーを発行する必要があります、 **NDIS\_状態\_PM\_WAKE\_理由**状態表示場合は、ネットワークアダプターでは、ウェイク アップの信号が生成されます。 それがの OID のセット要求を処理中にこのドライバーは[OID\_PNP\_設定\_POWER](https://docs.microsoft.com/windows-hardware/drivers/network/oid-pnp-set-power)電力状態にアダプターを移行します。

ミニポート ドライバーはこの状態表示を行うときに、設定、 **StatusBuffer**のメンバー、 [ **NDIS\_状態\_INDICATION** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_status_indication)構造体へのポインターを[ **NDIS\_PM\_WAKE\_理由**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_pm_wake_reason)構造体。

発行する方法について、 **NDIS\_状態\_PM\_WAKE\_理由**を示す値を参照してください[発行 NDIS Wake 理由状態インジケーター](https://docs.microsoft.com/windows-hardware/drivers/network/issuing-ndis-wake-reason-indications).

<a name="requirements"></a>必要条件
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>バージョン</p></td>
<td><p>NDIS 6.30 以降をサポートします。</p></td>
</tr>
<tr class="even">
<td><p>Header</p></td>
<td>Ndis.h (Ndis.h を含む)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


****
[**NDIS\_PM\_WAKE\_理由**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_pm_wake_reason)

[**NDIS\_状態\_を示す値**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_status_indication)

 

 





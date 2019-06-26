---
title: NDIS_STATUS_WAN_CO_MTULINKPARAMS
description: NDIS_STATUS_WAN_CO_MTULINKPARAMS 状態では、リンクを高速化することを示し、ウィンドウ パラメーターが変更されている CoNDIS ミニポート アダプターでアクティブになっている特定の VC を送信します。
ms.assetid: 1ba67087-08aa-4359-9884-e47bf634fda5
ms.date: 07/18/2017
keywords:
- NDIS_STATUS_WAN_CO_MTULINKPARAMS ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: acd894952e035cf4352d15c6a3276047dbf6b809
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67372550"
---
# <a name="ndisstatuswancomtulinkparams"></a>NDIS\_状態\_WAN\_CO\_MTULINKPARAMS


NDIS\_状態\_WAN\_CO\_MTULINKPARAMS 状態では、リンクを高速化することを示し、ウィンドウ パラメーターが変更されている CoNDIS ミニポート アダプターでアクティブになっている特定の VC を送信します。

<a name="remarks"></a>注釈
-------

**StatusBuffer**のメンバー、 [ **NDIS\_状態\_INDICATION** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_status_indication)構造体にはへのポインターが含まれています、 [ **WAN\_CO\_MTULINKPARAMS** ](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff565821(v=vs.85))構造体。 WAN\_CO\_MTULINKPARAMS 構造は、VC の新しいパラメーターをについて説明します。

NDIS の詳細については\_状態\_WAN\_CO\_MTULINKPARAMS を参照してください[を示している CoNDIS WAN ミニポート ドライバー ステータス](https://docs.microsoft.com/windows-hardware/drivers/network/indicating-condis-wan-miniport-driver-status)します。 いる CoNDIS WAN インターフェイスの詳細については、次を参照してください。[いる CoNDIS の WAN ミニポート ドライバーを実装する](https://docs.microsoft.com/windows-hardware/drivers/network/implementing-condis-wan-miniport-drivers)します。

<a name="requirements"></a>要件
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>バージョン</p></td>
<td><p>以降では、NDIS 6.20 が動作をサポートします。</p></td>
</tr>
<tr class="even">
<td><p>Header</p></td>
<td>Ndis.h (Ndis.h を含む)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[**NDIS\_状態\_を示す値**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_status_indication)

[**WAN\_CO\_MTULINKPARAMS**](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff565821(v=vs.85))

 

 





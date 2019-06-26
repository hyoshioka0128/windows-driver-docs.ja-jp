---
title: NDIS_STATUS_WAN_CO_FRAGMENT
description: NDIS_STATUS_WAN_CO_FRAGMENT 状態では、いる CoNDIS WAN ミニポート ドライバーが VC のエンドポイントから部分的なパケットを受信したことを示します。
ms.assetid: 5a534364-d528-45f8-a2e0-3c745b3b5ad0
ms.date: 07/18/2017
keywords:
- NDIS_STATUS_WAN_CO_FRAGMENT ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: 0ae329c9cf2a2737949585cd6617e3f6d3124de4
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67372574"
---
# <a name="ndisstatuswancofragment"></a>NDIS\_状態\_WAN\_CO\_フラグメント


NDIS\_状態\_WAN\_CO\_-FRAGMENT status はいる CoNDIS WAN ミニポート ドライバーが VC のエンドポイントから部分的なパケットを受信したことを示します。

<a name="remarks"></a>注釈
-------

**StatusBuffer**のメンバー、 [ **NDIS\_状態\_INDICATION** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_status_indication)構造体にはへのポインターが含まれています、 [ **NDIS\_WAN\_CO\_フラグメント**](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff559030(v=vs.85))構造体。 NDIS\_WAN\_CO\_フラグメントの構造が理由を部分的なパケットが受信されたことを説明します。

NDIS の詳細については\_状態\_WAN\_CO\_フラグメントを参照してください[を示している CoNDIS WAN ミニポート ドライバー ステータス](https://docs.microsoft.com/windows-hardware/drivers/network/indicating-condis-wan-miniport-driver-status)します。 いる CoNDIS WAN インターフェイスの詳細については、次を参照してください。[いる CoNDIS の WAN ミニポート ドライバーを実装する](https://docs.microsoft.com/windows-hardware/drivers/network/implementing-condis-wan-miniport-drivers)します。

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
<td><p>NDIS 6.0 および NDIS 5.1 のドライバーを Windows Vista でサポートされています。 Windows XP で 5.1 の NDIS ドライバーのサポートされています。</p></td>
</tr>
<tr class="even">
<td><p>Header</p></td>
<td>Ndis.h (Ndis.h を含む)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[**NDIS\_状態\_を示す値**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_status_indication)

[**NDIS\_WAN\_CO\_フラグメント**](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff559030(v=vs.85))

 

 





---
title: NDIS_STATUS_WAN_CO_FRAGMENT
description: NDIS_STATUS_WAN_CO_FRAGMENT 状態は、CoNDIS WAN ミニポートドライバーが VC のエンドポイントから部分的なパケットを受信したことを示します。
ms.assetid: 5a534364-d528-45f8-a2e0-3c745b3b5ad0
ms.date: 07/18/2017
keywords:
- NDIS_STATUS_WAN_CO_FRAGMENT ネットワークドライバー (Windows Vista 以降)
ms.localizationpriority: medium
ms.openlocfilehash: 8e09b31a63c3675baf3e2f66498180567f3eb9b8
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843503"
---
# <a name="ndis_status_wan_co_fragment"></a>NDIS\_ステータス\_WAN\_CO\_フラグメント


NDIS\_ステータス\_WAN\_CO\_フラグメントの状態は、CoNDIS WAN ミニポートドライバーが VC のエンドポイントから部分的なパケットを受信したことを示します。

<a name="remarks"></a>注釈
-------

[**Ndis\_ステータス\_示す**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_status_indication)構造体の**statusbuffer**メンバーには、 [**ndis\_WAN\_CO\_FRAGMENT**](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff559030(v=vs.85))構造体へのポインターが含まれています。 NDIS\_WAN\_CO\_フラグメント構造は、部分的なパケットを受信した理由を示します。

NDIS\_ステータス\_WAN\_CO\_フラグメントの詳細については、「 [wan のミニポートドライバーの状態を](https://docs.microsoft.com/windows-hardware/drivers/network/indicating-condis-wan-miniport-driver-status)確認する」を参照してください。 CoNDIS WAN インターフェイスの詳細については、「 [CONDIS Wan ミニポートドライバーの実装](https://docs.microsoft.com/windows-hardware/drivers/network/implementing-condis-wan-miniport-drivers)」を参照してください。

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
<td><p>Windows Vista では、NDIS 6.0 および NDIS 5.1 ドライバーでサポートされています。 Windows XP の NDIS 5.1 ドライバーでサポートされています。</p></td>
</tr>
<tr class="even">
<td><p>Header</p></td>
<td>Ndis .h (Ndis .h を含む)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[**NDIS\_状態\_表示**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_status_indication)

[**NDIS\_WAN\_CO\_FRAGMENT**](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff559030(v=vs.85))

 

 





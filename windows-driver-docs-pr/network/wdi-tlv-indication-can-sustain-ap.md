---
title: WDI_TLV_INDICATION_CAN_SUSTAIN_AP
description: WDI_TLV_INDICATION_CAN_SUSTAIN_AP では、理由を維持 AP のことを示す値を含む TLV です。
ms.assetid: 9C7B8E8D-BAF4-4DC7-A020-5B0DEC7CC2FB
ms.date: 07/18/2017
keywords:
- WDI_TLV_INDICATION_CAN_SUSTAIN_AP ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: da7936ed19c50cd27ede5d5ace9878f123d0ec0d
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67380787"
---
# <a name="wditlvindicationcansustainap"></a>WDI\_TLV\_INDICATION\_できます\_サステイン\_アジア太平洋


WDI\_TLV\_INDICATION\_できます\_サステイン\_AP はため、維持 AP のことを示す値を含む TLV します。

## <a name="tlv-type"></a>TLV 型


0xE7

## <a name="length"></a>長さ


Uint32 型のサイズをバイト単位で。

## <a name="values"></a>値


| 型   | 説明                                                                                                                        |
|--------|------------------------------------------------------------------------------------------------------------------------------------|
| UINT32 | 維持 AP のことが理由です。 参照してください[ **WDI\_できます\_サステイン\_AP\_理由**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wditypes/ne-wditypes-_wdi_can_sustain_ap_reason)の考えられる理由の値。 |

 

<a name="requirements"></a>必要条件
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>サポートされている最小のクライアント</p></td>
<td><p>Windows 10</p></td>
</tr>
<tr class="even">
<td><p>サポートされている最小のサーバー</p></td>
<td><p>Windows Server 2016</p></td>
</tr>
<tr class="odd">
<td><p>Header</p></td>
<td>Wditypes.hpp</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[NDIS\_STATUS\_WDI\_INDICATION\_CAN\_SUSTAIN\_AP](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wdi-indication-can-sustain-ap)

 

 





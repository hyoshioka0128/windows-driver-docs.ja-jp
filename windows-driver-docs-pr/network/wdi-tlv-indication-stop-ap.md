---
title: WDI_TLV_INDICATION_STOP_AP
description: WDI_TLV_INDICATION_STOP_AP では、ため、アジア太平洋の停止を示す値を含む TLV です。
ms.assetid: 49FA6AF6-68BE-437B-9715-5090F52F0109
ms.date: 07/18/2017
keywords:
- WDI_TLV_INDICATION_STOP_AP ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: 7087e406b044010d4ebf48c3838c7720140d347f
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67380775"
---
# <a name="wditlvindicationstopap"></a>WDI\_TLV\_INDICATION\_停止\_アジア太平洋


WDI\_TLV\_INDICATION\_停止\_AP はため、アジア太平洋の停止を示す値を含む TLV します。

## <a name="tlv-type"></a>TLV 型


0xE6

## <a name="length"></a>長さ


Uint32 型のサイズをバイト単位で。

## <a name="values"></a>値


| 型   | 説明                                                                                                  |
|--------|--------------------------------------------------------------------------------------------------------------|
| UINT32 | アジア太平洋の停止の理由です。 参照してください[ **WDI\_停止\_AP\_理由**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wditypes/ne-wditypes-_wdi_stop_ap_reason)の考えられる理由の値。 |

 

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


[NDIS\_STATUS\_WDI\_INDICATION\_STOP\_AP](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wdi-indication-stop-ap)

 

 





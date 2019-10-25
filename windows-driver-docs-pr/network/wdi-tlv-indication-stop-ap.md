---
title: WDI_TLV_INDICATION_STOP_AP
description: WDI_TLV_INDICATION_STOP_AP は、停止している AP を示す理由を含む TLV です。
ms.assetid: 49FA6AF6-68BE-437B-9715-5090F52F0109
ms.date: 07/18/2017
keywords:
- WDI_TLV_INDICATION_STOP_AP ネットワークドライバー (Windows Vista 以降)
ms.localizationpriority: medium
ms.openlocfilehash: fc19dfffedc925b07fd8cf53dbdfcb7bdc308935
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841744"
---
# <a name="wdi_tlv_indication_stop_ap"></a>WDI\_TLV\_\_\_AP の停止


WDI\_TLV\_\_停止\_AP は、AP の停止を示す理由を含む TLV です。

## <a name="tlv-type"></a>TLV 型


0xE6

## <a name="length"></a>長さ


UINT32 のサイズ (バイト単位)。

## <a name="values"></a>値


| タスクバーの検索ボックスに   | 説明                                                                                                  |
|--------|--------------------------------------------------------------------------------------------------------------|
| UINT32 | AP の停止理由。 考えられる理由値については、「 [**WDI\_STOP\_AP\_reason**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wditypes/ne-wditypes-_wdi_stop_ap_reason) 」を参照してください。 |

 

<a name="requirements"></a>要件
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
<td>Wditypes</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[NDIS\_STATUS\_WDI\_示さ\_STOP\_AP](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wdi-indication-stop-ap)

 

 





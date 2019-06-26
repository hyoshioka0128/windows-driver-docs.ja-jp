---
title: WDI_TLV_ETHERTYPE_ENCAP_TABLE
description: WDI_TLV_ETHERTYPE_ENCAP_TABLE では、関連付け、Ethertype をカプセル化を含む TLV です。
ms.assetid: BAAC7E5B-F13F-4AC8-A3F9-76197F92C7E3
ms.date: 07/18/2017
keywords:
- WDI_TLV_ETHERTYPE_ENCAP_TABLE ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: 10a5c91693127604ab26407550b6ffdc03110564
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67358551"
---
# <a name="wditlvethertypeencaptable"></a>WDI\_TLV\_ETHERTYPE\_全て\_テーブル


WDI\_TLV\_ETHERTYPE\_全て\_テーブルは、アソシエーションの Ethertype カプセル化を含む TLV します。

## <a name="tlv-type"></a>TLV 型


0x31

## <a name="length"></a>長さ


含まれるすべての要素のサイズの合計をバイト単位で。

## <a name="values"></a>値


| 型                                                                                       | 説明                                                                                                                                                                  |
|--------------------------------------------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| [**WDI\_ETHERTYPE\_カプセル化\_エントリ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wditypes/ns-wditypes-_wdi_ethertype_encapsulation_entry)\[\] | 配列の[ **WDI\_ETHERTYPE\_カプセル化\_エントリ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wditypes/ns-wditypes-_wdi_ethertype_encapsulation_entry)関連付け Ethertype カプセル化を指定する要素。 |

 

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

 

 





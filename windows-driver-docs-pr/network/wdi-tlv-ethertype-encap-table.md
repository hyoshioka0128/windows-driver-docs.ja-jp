---
title: WDI_TLV_ETHERTYPE_ENCAP_TABLE
description: WDI_TLV_ETHERTYPE_ENCAP_TABLE は、アソシエーションの Ethertype カプセル化を含む TLV です。
ms.assetid: BAAC7E5B-F13F-4AC8-A3F9-76197F92C7E3
ms.date: 07/18/2017
keywords:
- WDI_TLV_ETHERTYPE_ENCAP_TABLE ネットワークドライバー (Windows Vista 以降)
ms.localizationpriority: medium
ms.openlocfilehash: a41a61477b4aea91e1270444d3fcdfe078aa55cc
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72834089"
---
# <a name="wdi_tlv_ethertype_encap_table"></a>WDI\_TLV\_ETHERTYPE\_ENCAP\_テーブル


WDI\_TLV\_ETHERTYPE\_ENCAP\_TABLE は、アソシエーションの TLV ETHERTYPE を含むカプセル化です。

## <a name="tlv-type"></a>TLV 型


0x31

## <a name="length"></a>長さ


含まれているすべての要素のサイズの合計 (バイト単位)。

## <a name="values"></a>値


| タスクバーの検索ボックスに                                                                                       | 説明                                                                                                                                                                  |
|--------------------------------------------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| [**WDI\_ETHERTYPE\_カプセル化\_エントリ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wditypes/ns-wditypes-_wdi_ethertype_encapsulation_entry)\[\] | アソシエーションの Ethertype カプセル化を指定する[**WDI\_ETHERTYPE\_カプセル化\_エントリ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wditypes/ns-wditypes-_wdi_ethertype_encapsulation_entry)要素の配列。 |

 

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

 

 





---
title: WDI_TLV_HESSID
description: WDI_TLV_HESSID は、HESSIDs の一覧を含む TLV です。
ms.assetid: 630A1824-7722-4B03-8073-EFC44E142400
ms.date: 07/18/2017
keywords:
- WDI_TLV_HESSID ネットワークドライバー (Windows Vista 以降)
ms.localizationpriority: medium
ms.openlocfilehash: 671f8209f35441afe7c09192b66457bd233f680e
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844203"
---
# <a name="wdi_tlv_hessid"></a>WDI\_TLV\_HESSID


WDI\_TLV\_HESSID は、HESSIDs の一覧を含む TLV です。

## <a name="tlv-type"></a>TLV 型


0xC8

## <a name="length"></a>長さ


[**WDI\_MAC\_アドレス**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dot11wdi/ns-dot11wdi-_wdi_mac_address)構造体の配列のサイズ (バイト単位)。 配列には1つ以上の構造体が含まれている必要があります。

## <a name="values"></a>値


| タスクバーの検索ボックスに                                                  | 説明        |
|-------------------------------------------------------|--------------------|
| [**WDI\_MAC\_アドレス**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dot11wdi/ns-dot11wdi-_wdi_mac_address)\[\] | HESSIDs のリスト。 |

 

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

 

 





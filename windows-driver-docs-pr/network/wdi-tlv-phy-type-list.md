---
title: WDI_TLV_PHY_TYPE_LIST
description: WDI_TLV_PHY_TYPE_LIST は、PHY 型の配列を含む TLV です。
ms.assetid: 4066E4CE-D63E-4499-AE27-11F6BD57795D
ms.date: 07/18/2017
keywords:
- WDI_TLV_PHY_TYPE_LIST ネットワークドライバー (Windows Vista 以降)
ms.localizationpriority: medium
ms.openlocfilehash: 74aa73aeb6b962d8e7c4c14e658b09988736176a
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841664"
---
# <a name="wdi_tlv_phy_type_list"></a>WDI\_TLV\_PHY\_種類\_リスト


WDI\_TLV\_PHY\_型\_リストは、PHY 型の配列を含む TLV です。

## <a name="tlv-type"></a>TLV 型


0x19

## <a name="length"></a>長さ


[**WDI\_PHY\_型**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wditypes/ne-wditypes-_wdi_phy_type)の値の配列のサイズ (バイト単位)。 配列には1つ以上の値が含まれている必要があります。

## <a name="values"></a>値


| タスクバーの検索ボックスに                                            | 説明                  |
|-------------------------------------------------|------------------------------|
| [**WDI\_PHY\_種類**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wditypes/ne-wditypes-_wdi_phy_type)\[\] | PHY 型の値の配列。 |

 

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

 

 





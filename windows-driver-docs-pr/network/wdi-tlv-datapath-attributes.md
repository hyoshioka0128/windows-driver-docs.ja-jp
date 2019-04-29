---
title: WDI_TLV_DATAPATH_ATTRIBUTES
description: WDI_TLV_DATAPATH_ATTRIBUTES は、データパス属性を含む TLV です。
ms.assetid: 3477054B-01CE-4D08-8A58-49FD8840B237
ms.date: 07/18/2017
keywords:
- WDI_TLV_DATAPATH_ATTRIBUTES ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: d4befa0556667dc4f28dd36f338243483680ee74
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63331817"
---
# <a name="wditlvdatapathattributes"></a>WDI\_TLV\_データパス\_属性


WDI\_TLV\_データパス\_属性はデータパス属性を含む TLV します。

## <a name="tlv-type"></a>TLV 型


0xb8 と

## <a name="length"></a>長さ


すべてのサイズ (バイト) を合計には、TLVs が含まれています。

## <a name="values"></a>値


| 種類                                                                      | 許可されている複数の TLV インスタンス | 省略可能 | 説明                |
|---------------------------------------------------------------------------|--------------------------------|----------|----------------------------|
| [**WDI\_TLV\_データパス\_機能**](wdi-tlv-datapath-capabilities.md) |                                | x        | データパス機能。 |

 

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

 

 





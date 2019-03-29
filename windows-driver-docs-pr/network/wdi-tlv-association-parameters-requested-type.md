---
title: WDI_TLV_ASSOCIATION_PARAMETERS_REQUESTED_TYPE
description: WDI_TLV_ASSOCIATION_PARAMETERS_REQUESTED_TYPE では、要求された関連付けパラメーター TLV 型を含む TLV です。
ms.assetid: BF4FE327-56A6-4EEE-B6C2-9B93D5C1DD47
ms.date: 07/18/2017
keywords:
- WDI_TLV_ASSOCIATION_PARAMETERS_REQUESTED_TYPE ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: 6fab91a66e56360eb20c880dfd2482528498bdd8
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56579639"
---
# <a name="wditlvassociationparametersrequestedtype"></a>WDI\_TLV\_アソシエーション\_パラメーター\_要求された\_型


WDI\_TLV\_アソシエーション\_パラメーター\_要求された\_型が要求された関連付けパラメーター TLV 型を含む TLV します。

## <a name="tlv-type"></a>TLV 型


0 xbb です。

## <a name="length"></a>長さ


Uint16 型の要素の配列のサイズをバイト単位で。 配列には、1 つ以上の要素を含める必要があります。

## <a name="values"></a>値


| 型       | 説明                                                                                                                                                                                                                                  |
|------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| UINT16\[\] | 要求された関連付けパラメーター TLV 型の一覧。 有効な TLV 種類は[ **WDI\_TLV\_PMKID** ](wdi-tlv-pmkid.md) (0x9F) と[ **WDI\_TLV\_余分な\_アソシエーション\_要求\_IES** ](wdi-tlv-extra-association-request-ies.md) (0x40)。 |

 

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

 

 





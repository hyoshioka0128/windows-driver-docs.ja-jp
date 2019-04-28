---
title: WDI_TLV_ASSOCIATION_REQUEST_FRAME
description: WDI_TLV_ASSOCIATION_REQUEST_FRAME では、関連付けに使用された関連要求を含む TLV です。
ms.assetid: C2323DFE-2B13-4E35-BF9B-4A0B5F3B2076
ms.date: 07/18/2017
keywords:
- WDI_TLV_ASSOCIATION_REQUEST_FRAME ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: 3ed020c91b3dafcd8490f1a86f850a4d7f21b207
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63363038"
---
# <a name="wditlvassociationrequestframe"></a>WDI\_TLV\_アソシエーション\_要求\_フレーム


WDI\_TLV\_アソシエーション\_要求\_フレームは、関連付けに使用された関連要求を含む TLV します。

## <a name="tlv-type"></a>TLV 型


0x2E

## <a name="length"></a>長さ


UINT8 の要素の配列のサイズをバイト単位で。 配列には、1 つ以上の要素を含める必要があります。

## <a name="values"></a>値


| 型      | 説明                                                                                                                                       |
|-----------|---------------------------------------------------------------------------------------------------------------------------------------------------|
| UINT8\[\] | 関連付けに使用された関連要求を指定する UINT8 要素の配列。 これは、802.11 MAC ヘッダーには含まれません。 |

 

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

 

 





---
title: WDI_TLV_EXTRA_ASSOCIATION_REQUEST_IES
description: WDI_TLV_EXTRA_ASSOCIATION_REQUEST_IES は、ポートによって送信されたアソシエーションの要求に含める必要がある情報要素 (IEs) を含む TLV です。
ms.assetid: 2275B8F2-1FE4-4518-AD67-E9A65F2F37DA
ms.date: 07/18/2017
keywords:
- WDI_TLV_EXTRA_ASSOCIATION_REQUEST_IES ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: e79a43bf6c1f1c8c5e3b93b9039252e90e581f4a
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56575001"
---
# <a name="wditlvextraassociationrequesties"></a>WDI\_TLV\_余分な\_アソシエーション\_要求\_IES


WDI\_TLV\_余分な\_アソシエーション\_要求\_I は、ポートによって送信されたアソシエーションの要求に含める必要がある情報要素 (IEs) を含む TLV します。

## <a name="tlv-type"></a>TLV 型


0x40

## <a name="length"></a>長さ


UINT8 の要素の配列のサイズをバイト単位で。 配列には、1 つ以上の要素を含める必要があります。

## <a name="values"></a>値


| 型      | 説明                                                                                                                                                                                                                                               |
|-----------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| UINT8\[\] | ポートによって送信されたアソシエーションの要求に含める必要がある IEs を含む UINT8 要素の配列。 これらは、任意のデバイスに関連付ける BSSID に適用されます。 これらは、共通する追加および BSSID 特定 IEs で使用する必要があります。 |

 

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

 

 





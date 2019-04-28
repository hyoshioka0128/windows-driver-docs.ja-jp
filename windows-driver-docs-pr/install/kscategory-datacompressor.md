---
title: KSCATEGORY_DATACOMPRESSOR
description: KSCATEGORY_DATACOMPRESSOR
ms.assetid: 7e4bf7b3-b3be-4a76-bc9e-0b1b020a7044
keywords:
- KSCATEGORY_DATACOMPRESSOR デバイスとドライバーのインストール
topic_type:
- apiref
api_name:
- KSCATEGORY_DATACOMPRESSOR
api_location:
- Ks.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 1272c0c4fe52eeb5589d5cd20b817737cd26b947
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63368064"
---
# <a name="kscategorydatacompressor"></a>KSCATEGORY_DATACOMPRESSOR


KSCATEGORY_DATACOMPRESSOR[デバイス インターフェイス クラス](https://msdn.microsoft.com/library/windows/hardware/ff541339)が定義されている、[カーネル ストリーミング](https://msdn.microsoft.com/library/windows/hardware/ff568277)データ ストリームを圧縮する (KS) 機能のカテゴリ。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">属性</th>
<th align="left">設定</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>識別子</p></td>
<td align="left"><p>KSCATEGORY_DATACOMPRESSOR</p></td>
</tr>
<tr class="even">
<td align="left"><p>クラス GUID</p></td>
<td align="left"><p>{1E84C900-7E70-11D0-A5D6-28DB04C10000}</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>コメント
-------

KS デバイス用のドライバーでは、オペレーティング システムに、デバイスが KSCATEGORY_DATACOMPRESSOR 機能カテゴリをサポートすることを示す KSCATEGORY_DATACOMPRESSOR のインスタンスを登録します。

KSCATEGORY_DATACOMPRESSOR 機能のカテゴリは、のいずれか、 [ **KSPROPERTY_TOPOLOGY_CATEGORIES**](https://msdn.microsoft.com/library/windows/hardware/ff565799)します。

データ ストリームを圧縮解除 KS 機能のカテゴリに対して定義されているデバイスのインターフェイス クラスについては、次を参照してください。 [ **KSCATEGORY_DATADECOMPRESSOR**](kscategory-datadecompressor.md)します。

<a name="requirements"></a>必要条件
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>Header</p></td>
<td align="left">Ks.h (Ks.h を含む)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[**KSCATEGORY_DATADECOMPRESSOR**](kscategory-datadecompressor.md)

[**KSPROPERTY_TOPOLOGY_CATEGORIES**](https://msdn.microsoft.com/library/windows/hardware/ff565799)

 

 







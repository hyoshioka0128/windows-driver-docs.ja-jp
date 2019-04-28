---
title: KSCATEGORY_BRIDGE
description: KSCATEGORY_BRIDGE
ms.assetid: 7973cac5-2b74-4af1-8912-370e922e5f4d
keywords:
- KSCATEGORY_BRIDGE デバイスとドライバーのインストール
topic_type:
- apiref
api_name:
- KSCATEGORY_BRIDGE
api_location:
- Ks.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: bc3fef53c7bf069ce37102e4801b9b6a8e7ff743
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63377310"
---
# <a name="kscategorybridge"></a>KSCATEGORY_BRIDGE


KSCATEGORY_BRIDGE[デバイス インターフェイス クラス](https://msdn.microsoft.com/library/windows/hardware/ff541339)が定義されている、[カーネル ストリーミング](https://msdn.microsoft.com/library/windows/hardware/ff568277)KS サブシステムと別のソフトウェアのソフトウェアのインターフェイスをサポートしています (KS) 機能のカテゴリコンポーネント。

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
<td align="left"><p>KSCATEGORY_BRIDGE</p></td>
</tr>
<tr class="even">
<td align="left"><p>クラス GUID</p></td>
<td align="left"><p>{085AFF00-62CE-11CF-A5D6-28DB04C10000}</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>コメント
-------

KS オーディオ アダプター デバイス用のドライバーでは、オペレーティング システムに、デバイスが KSCATEGORY_BRIDGE 機能カテゴリをサポートすることを示す KSCATEGORY_BRIDGE のインスタンスを登録します。

KSCATEGORY_BRIDGE 機能のカテゴリの詳細については、次を参照してください。 [ **KSPROPERTY_TOPOLOGY_CATEGORIES**](https://msdn.microsoft.com/library/windows/hardware/ff565799)します。

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

 

 






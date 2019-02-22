---
title: KSCATEGORY_COMMUNICATIONSTRANSFORM
description: KSCATEGORY_COMMUNICATIONSTRANSFORM
ms.assetid: a958c5a6-18a3-43e0-a6ac-84a879a981da
keywords:
- KSCATEGORY_COMMUNICATIONSTRANSFORM デバイスとドライバーのインストール
topic_type:
- apiref
api_name:
- KSCATEGORY_COMMUNICATIONSTRANSFORM
api_location:
- Ks.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 243e8237329d196b40c24f2f12e090ef2f412502
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56557487"
---
# <a name="kscategorycommunicationstransform"></a>KSCATEGORY_COMMUNICATIONSTRANSFORM


KSCATEGORY_COMMUNICATIONSTRANSFORM[デバイス インターフェイス クラス](https://msdn.microsoft.com/library/windows/hardware/ff541339)が定義されている、[カーネル ストリーミング](https://msdn.microsoft.com/library/windows/hardware/ff568277)通信変換デバイスの機能のカテゴリ (KS)。

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
<td align="left"><p>KSCATEGORY_COMMUNICATIONSTRANSFORM</p></td>
</tr>
<tr class="even">
<td align="left"><p>クラス GUID</p></td>
<td align="left"><p>{CF1DDA2C-9743-11D0-A3EE-00A0C9223196}</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>注釈
-------

KS デバイス用のドライバーでは、オペレーティング システムに、デバイスが KSCATEGORY_COMMUNICATIONSTRANSFORM 機能カテゴリをサポートすることを示す KSCATEGORY_COMMUNICATIONSTRANSFORM のインスタンスを登録します。

KSCATEGORY_COMMUNICATIONSTRANSFORM 機能のカテゴリは、のいずれか、 [ **KSPROPERTY_TOPOLOGY_CATEGORIES**](https://msdn.microsoft.com/library/windows/hardware/ff565799)します。

<a name="requirements"></a>要件
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


[**KSPROPERTY_TOPOLOGY_CATEGORIES**](https://msdn.microsoft.com/library/windows/hardware/ff565799)

 

 







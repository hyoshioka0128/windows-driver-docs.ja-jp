---
title: KSCATEGORY_CLOCK
description: KSCATEGORY_CLOCK
ms.assetid: 1a5afadd-f76f-4184-a93e-af82769ecc1b
keywords:
- KSCATEGORY_CLOCK デバイスとドライバーのインストール
topic_type:
- apiref
api_name:
- KSCATEGORY_CLOCK
api_location:
- Ks.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 4cc770e4647f0d62c51f1e6d82aa4dcaf995c8d1
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56536716"
---
# <a name="kscategoryclock"></a>KSCATEGORY_CLOCK


KSCATEGORY_CLOCK[デバイス インターフェイス クラス](https://msdn.microsoft.com/library/windows/hardware/ff541339)が定義されている、[カーネル ストリーミング](https://msdn.microsoft.com/library/windows/hardware/ff568277)クロック デバイスの機能のカテゴリ (KS)。

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
<td align="left"><p>KSCATEGORY_CLOCK</p></td>
</tr>
<tr class="even">
<td align="left"><p>クラス GUID</p></td>
<td align="left"><p>{53172480-4791-11D0-A5D6-28DB04C10000}</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>注釈
-------

KS デバイス用のドライバーでは、オペレーティング システムに、デバイスが KSCATEGORY_CLOCK 機能カテゴリをサポートすることを示す KSCATEGORY_CLOCK のインスタンスを登録します。

カーネルのクロックのストリームの詳細については、[KS ミニドライバー アーキテクチャ](https://msdn.microsoft.com/library/windows/hardware/ff567656)、 [KS クロック](https://msdn.microsoft.com/library/windows/hardware/ff567307)、および[AVStream クロック](https://msdn.microsoft.com/library/windows/hardware/ff554208)を参照してください。

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

 

 






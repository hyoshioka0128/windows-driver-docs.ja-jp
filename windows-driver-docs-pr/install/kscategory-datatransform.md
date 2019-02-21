---
title: KSCATEGORY_DATATRANSFORM
description: KSCATEGORY_DATATRANSFORM
ms.assetid: 2e5ff89a-6ec4-4bdf-b935-675c2a337efb
keywords:
- KSCATEGORY_DATATRANSFORM デバイスとドライバーのインストール
topic_type:
- apiref
api_name:
- KSCATEGORY_DATATRANSFORM
api_location:
- Ks.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 1102c962f517c6f47ebbd2290c708eef7e4b6a67
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56552066"
---
# <a name="kscategorydatatransform"></a>KSCATEGORY_DATATRANSFORM


KSCATEGORY_DATATRANSFORM[デバイス インターフェイス クラス](https://msdn.microsoft.com/library/windows/hardware/ff541339)が定義されている、[カーネル ストリーミング](https://msdn.microsoft.com/library/windows/hardware/ff568277)オーディオ データ ストリームを変換する (KS) 機能のカテゴリ。

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
<td align="left"><p>KSCATEGORY_DATATRANSFORM</p></td>
</tr>
<tr class="even">
<td align="left"><p>クラス GUID</p></td>
<td align="left"><p>{2EB07EA0-7E70-11D0-A5D6-28DB04C10000}</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>注釈
-------

KS デバイス用のドライバーでは、オペレーティング システムに、デバイスが KSCATEGORY_DATATRANSFORM 機能カテゴリをサポートすることを示す KSCATEGORY_DATATRANSFORM のインスタンスを登録します。

INF ファイルでこの機能のカテゴリを登録する方法の例は、次を参照してください、 *Ddksynth.inf* INF ファイルでのソフトウェアのシンセサイザー サンプルに含まれている、 *src\\オーディオ\\ddksynth。* WDK のディレクトリ。

この機能のカテゴリの詳細については、次を参照してください[オーディオ アダプターのデバイスのインターフェイスをインストールする](https://msdn.microsoft.com/library/windows/hardware/ff536813)、 [ **KSPROPERTY_TOPOLOGY_CATEGORIES**](https://msdn.microsoft.com/library/windows/hardware/ff565799)、および[。GFX 要件フィルター ファクトリ](https://msdn.microsoft.com/library/windows/hardware/ff537839)します。

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

 

 






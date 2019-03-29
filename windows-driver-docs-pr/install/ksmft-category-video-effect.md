---
title: KSMFT_CATEGORY_VIDEO_EFFECT
description: KSMFT_CATEGORY_VIDEO_EFFECT
ms.assetid: 81286240-d6eb-4872-a06c-34046767a2cc
keywords:
- KSMFT_CATEGORY_VIDEO_EFFECT デバイスとドライバーのインストール
topic_type:
- apiref
api_name:
- KSMFT_CATEGORY_VIDEO_EFFECT
api_location:
- Ks.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 3b9769bd9cc867cec18eec43aa022a8fe5ca2874
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56573590"
---
# <a name="ksmftcategoryvideoeffect"></a>KSMFT_CATEGORY_VIDEO_EFFECT


KSMFT_CATEGORY_VIDEO_EFFECT[デバイス インターフェイス クラス](https://msdn.microsoft.com/library/windows/hardware/ff541339)が定義されている、[カーネル ストリーミング](https://msdn.microsoft.com/library/windows/hardware/ff560842)ビデオ デバイスの機能のカテゴリ (KS)。

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
<td align="left"><p>KSMFT_CATEGORY_VIDEO_EFFECT</p></td>
</tr>
<tr class="even">
<td align="left"><p>クラス GUID</p></td>
<td align="left"><p>{12e17c21-532c-4a6e-8a1c-40825a736397}</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>コメント
-------

MFT コーデックがサポートしている AVStream ドライバーは、デバイスが KSMFT_CATEGORY_VIDEO_EFFECT 機能カテゴリをサポートするオペレーティング システムに示すためにこのデバイスのインターフェイス クラスのインスタンスを登録します。

ハードウェアのコーデック サポート AVStream デバイスのデバイスのインターフェイス クラスの詳細については、次を参照してください。 [AVStream のコーデック サポートはハードウェアの概要](https://msdn.microsoft.com/library/windows/hardware/gg299325)します。

INF ファイルでこの機能のカテゴリを登録する方法の詳細については、次を参照してください、 *Hiddigi.inf*に含まれているファイルを、 *src\\入力\\hiddigi*サンプル。ドライバー WDK に含まれています。

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

 

 






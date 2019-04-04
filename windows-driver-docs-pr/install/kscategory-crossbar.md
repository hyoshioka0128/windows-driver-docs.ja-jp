---
title: KSCATEGORY_CROSSBAR
description: KSCATEGORY_CROSSBAR
ms.assetid: 0a5edfd5-ad50-4402-8f6d-d6c5018d1ab2
keywords:
- KSCATEGORY_CROSSBAR デバイスとドライバーのインストール
topic_type:
- apiref
api_name:
- KSCATEGORY_CROSSBAR
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: f2d0da83456ef4219aa579fc8b79f2a09b82e5f0
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56577825"
---
# <a name="kscategorycrossbar"></a>KSCATEGORY_CROSSBAR


KSCATEGORY_CROSSBAR[デバイス インターフェイス クラス](https://msdn.microsoft.com/library/windows/hardware/ff541339)が定義されている、[カーネル ストリーミング](https://msdn.microsoft.com/library/windows/hardware/ff568277)ビデオとオーディオのストリームをルーティングするクロスバー デバイスの機能のカテゴリ (KS)。

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
<td align="left"><p>KSCATEGORY_CROSSBAR</p></td>
</tr>
<tr class="even">
<td align="left"><p>クラス GUID</p></td>
<td align="left"><p>{A799A801-A46D-11D0-A18C-00A02401DCD4}</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>コメント
-------

KS デバイス用のドライバーでは、オペレーティング システムに、デバイスが KSCATEGORY_CROSSBAR 機能カテゴリをサポートすることを示す KSCATEGORY_CROSSBAR のインスタンスを登録します。

INF ファイルでこの機能のカテゴリを登録する方法の例は、次を参照してください、 *Bdan.inf* INF ファイルでのソフトウェアのチューナー サンプルに含まれている、 *src\\swtuner\\algtuner。* WDK のディレクトリ。

オーディオとビデオに対するクロスバー デバイスについては、[ビデオ キャプチャ デバイスでのフィルター使用](https://msdn.microsoft.com/library/windows/hardware/ff559598)と[アナログ ビデオ カテゴリ](https://msdn.microsoft.com/library/windows/hardware/ff554095)を参照してください。

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
<td align="left">Ksmedia.h (Ksmedia.h を含む)</td>
</tr>
</tbody>
</table>

 

 






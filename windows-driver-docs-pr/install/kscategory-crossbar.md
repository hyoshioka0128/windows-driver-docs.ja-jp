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
ms.openlocfilehash: fa5ce0a7f5e56a8db1d573b4192ffb949c0b221d
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67385905"
---
# <a name="kscategorycrossbar"></a>KSCATEGORY_CROSSBAR


KSCATEGORY_CROSSBAR[デバイス インターフェイス クラス](https://docs.microsoft.com/windows-hardware/drivers/install/device-interface-classes)が定義されている、[カーネル ストリーミング](https://docs.microsoft.com/windows-hardware/drivers/stream/streaming-minidrivers2)ビデオとオーディオのストリームをルーティングするクロスバー デバイスの機能のカテゴリ (KS)。

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

オーディオとビデオに対するクロスバー デバイスについては、次を参照してください。[ビデオ キャプチャ デバイスでのフィルター使用](https://docs.microsoft.com/windows-hardware/drivers/stream/filters-used-with-the-video-capture-devices)と[アナログ ビデオ カテゴリ](https://docs.microsoft.com/windows-hardware/drivers/stream/analog-video-category)します。

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

 

 






---
title: KSCATEGORY_VPMUX
description: KSCATEGORY_VPMUX
ms.assetid: d63ecb2b-f1f7-4f02-a82e-4ed17d1f83d9
keywords:
- KSCATEGORY_VPMUX デバイスとドライバーのインストール
topic_type:
- apiref
api_name:
- KSCATEGORY_VPMUX
api_location:
- Ks.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: c8b835c7274b31514326abc311284ebf12911ca9
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67385539"
---
# <a name="kscategoryvpmux"></a>KSCATEGORY_VPMUX


KSCATEGORY_VPMUX[デバイス インターフェイス クラス](https://docs.microsoft.com/windows-hardware/drivers/install/device-interface-classes)が定義されている、[カーネル ストリーミング](https://docs.microsoft.com/windows-hardware/drivers/stream/streaming-minidrivers2)ビデオを多重化をサポートしています (KS) 機能のカテゴリ。

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
<td align="left"><p>KSCATEGORY_VPMUX</p></td>
</tr>
<tr class="even">
<td align="left"><p>クラス GUID</p></td>
<td align="left"><p>{A799A803-A46D-11D0-A18C-00A02401DCD4}</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>注釈
-------

KS デバイス用のドライバーでは、オペレーティング システムに、デバイスが KSCATEGORY_VPMUX 機能カテゴリをサポートすることを示す KSCATEGORY_VPMUX のインスタンスを登録します。

概要ビデオ デバイスについては、次を参照してください。[ビデオ キャプチャ デバイス](https://docs.microsoft.com/windows-hardware/drivers/stream/video-capture-devices)します。

ビデオ デバイスのデバイスのインターフェイス クラスについては、次を参照してください。 [ **KSCATEGORY_VIDEO**](kscategory-video.md)します。

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


[**KSCATEGORY_VIDEO**](kscategory-video.md)

 

 







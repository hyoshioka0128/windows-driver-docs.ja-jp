---
title: KSCATEGORY_VIDEO
description: KSCATEGORY_VIDEO
ms.assetid: cdcdb22b-3969-4c58-a8ce-a9d0b4b64e3b
keywords:
- KSCATEGORY_VIDEO デバイスとドライバーのインストール
topic_type:
- apiref
api_name:
- KSCATEGORY_VIDEO
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 61ed32f33e8b6671a50090a3899b5234778b874d
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67385273"
---
# <a name="kscategoryvideo"></a>KSCATEGORY_VIDEO


KSCATEGORY_VIDEO[デバイス インターフェイス クラス](https://docs.microsoft.com/windows-hardware/drivers/install/device-interface-classes)が定義されている、[カーネル ストリーミング](https://docs.microsoft.com/windows-hardware/drivers/stream/streaming-minidrivers2)ビデオ デバイスの機能のカテゴリ (KS)。

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
<td align="left"><p>KSCATEGORY_VIDEO</p></td>
</tr>
<tr class="even">
<td align="left"><p>クラス GUID</p></td>
<td align="left"><p>{6994AD05-93EF-11D0-A3CC-00A0C9223196}</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>注釈
-------

KS ビデオ デバイスのドライバーでは、オペレーティング システムに、デバイスが KSCATEGORY_VIDEO 機能カテゴリをサポートすることを示す KSCATEGORY_VIDEO のインスタンスを登録します。

INF ファイルでこの機能のカテゴリを登録する方法の例は、次を参照してください。、 *Bdan.inf* INF ファイルでのソフトウェアのチューナー サンプルに含まれている、 *src/swtuner/algtuner* WDK のディレクトリ。

この機能のカテゴリの詳細については、次を参照してください。 [UVC INF ファイルを提供する](https://docs.microsoft.com/windows-hardware/drivers/stream/providing-a-uvc-inf-file)します。

概要ビデオ デバイスについては、次を参照してください。[ビデオ キャプチャ デバイス](https://docs.microsoft.com/windows-hardware/drivers/stream/video-capture-devices)します。

ビデオ デバイスの他のデバイスのインターフェイス クラスについては、次を参照してください[ **KSCATEGORY_TVAUDIO** ](kscategory-tvaudio.md)と[ **KSCATEGORY_TVTUNER** ](kscategory-tvtuner.md) .

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
<td align="left">Ksmedia.h (Ksmedia.h を含む)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[**KSCATEGORY_TVAUDIO**](kscategory-tvaudio.md)

[**KSCATEGORY_TVTUNER**](kscategory-tvtuner.md)

 

 







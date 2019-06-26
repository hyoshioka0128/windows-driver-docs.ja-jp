---
title: KSCATEGORY_VBICODEC
description: KSCATEGORY_VBICODEC
ms.assetid: c69857e5-19ca-44aa-ae42-bc015be2b0f8
keywords:
- KSCATEGORY_VBICODEC デバイスとドライバーのインストール
topic_type:
- apiref
api_name:
- KSCATEGORY_VBICODEC
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 6477b7e7c12fbcd1a5f1f16840d46ec386935358
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67385542"
---
# <a name="kscategoryvbicodec"></a>KSCATEGORY_VBICODEC


KSCATEGORY_VBICODEC[デバイス インターフェイス クラス](https://docs.microsoft.com/windows-hardware/drivers/install/device-interface-classes)が定義されている、[カーネル ストリーミング](https://docs.microsoft.com/windows-hardware/drivers/stream/streaming-minidrivers2)帰線消去期間 (VBI) のビデオ コーデックのデバイスの機能のカテゴリ (KS)。

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
<td align="left"><p>KSCATEGORY_VBICODEC</p></td>
</tr>
<tr class="even">
<td align="left"><p>クラス GUID</p></td>
<td align="left"><p>{07DAD660-22F1-11D1-A9F4-00C04FBBDE8F}</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>注釈
-------

KS デバイス用のドライバーでは、オペレーティング システムに、デバイスが KSCATEGORY_VBICODEC 機能カテゴリをサポートすることを示す KSCATEGORY_VBICODEC のインスタンスを登録します。

概要ビデオ デバイスについては、次を参照してください。[ビデオ キャプチャ デバイス](https://docs.microsoft.com/windows-hardware/drivers/stream/video-capture-devices)します。

ビデオの非表示の詳細については、次を参照してください。[ビデオ キャプチャ デバイスからのデータのストリーミング](https://docs.microsoft.com/windows-hardware/drivers/stream/streaming-data-from-a-video-capture-device)と[VBI カテゴリ](https://docs.microsoft.com/windows-hardware/drivers/stream/vbi-category)します。

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


[**KSCATEGORY_VIDEO**](kscategory-video.md)

 

 







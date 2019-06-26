---
title: KSPROPERTY\_VIDEOCOMPRESSION\_オーバーライド\_フレーム\_サイズ
description: KSPROPERTY\_VIDEOCOMPRESSION\_オーバーライド\_フレーム\_サイズ プロパティは、フレーム サイズ (バイト数) を一時的に上書きします。 このプロパティは省略可能です。
ms.assetid: 626b0dcf-3087-407b-8e7f-00314de7d2f2
keywords:
- KSPROPERTY_VIDEOCOMPRESSION_OVERRIDE_FRAME_SIZE ストリーミング メディア デバイス
topic_type:
- apiref
api_name:
- KSPROPERTY_VIDEOCOMPRESSION_OVERRIDE_FRAME_SIZE
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 14d084503742671b06aa54aee6723dba7472c74f
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67355925"
---
# <a name="kspropertyvideocompressionoverrideframesize"></a>KSPROPERTY\_VIDEOCOMPRESSION\_オーバーライド\_フレーム\_サイズ


KSPROPERTY\_VIDEOCOMPRESSION\_オーバーライド\_フレーム\_サイズ プロパティは、フレーム サイズ (バイト数) を一時的に上書きします。 このプロパティは省略可能です。

## <span id="ddk_ksproperty_videocompression_override_frame_size_ks"></span><span id="DDK_KSPROPERTY_VIDEOCOMPRESSION_OVERRIDE_FRAME_SIZE_KS"></span>


### <a name="usage-summary-table"></a>使用状況の概要テーブル

<table>
<colgroup>
<col width="20%" />
<col width="20%" />
<col width="20%" />
<col width="20%" />
<col width="20%" />
</colgroup>
<thead>
<tr class="header">
<th>取得</th>
<th>設定</th>
<th>対象</th>
<th>プロパティ記述子の型</th>
<th>プロパティ値の型</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>X</p></td>
<td><p>〇</p></td>
<td><p>フィルター</p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-ksproperty_videocompression_s" data-raw-source="[&lt;strong&gt;KSPROPERTY_VIDEOCOMPRESSION_S&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-ksproperty_videocompression_s)"><strong>KSPROPERTY_VIDEOCOMPRESSION_S</strong></a></p></td>
<td><p>LONG</p></td>
</tr>
</tbody>
</table>

 

プロパティ値 (データの操作) が値をオーバーライドする一時的なフレーム サイズを指定します。

<a name="remarks"></a>注釈
-------

**値**、KSPROPERTY のメンバー\_VIDEOCOMPRESSION\_の構造は、フレームのオーバーライドするデータ レートを指定します。

このプロパティをサポートするミニドライバーを設定する必要があります、 **KS\_CompressionCaps\_CanCrunch**フラグ、**機能**のメンバー、 [ **KSPROPERTY\_VIDEOCOMPRESSION\_GETINFO\_S** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-ksproperty_videocompression_getinfo_s)デバイスのビデオの圧縮機能を取得する構造体。

ビデオ キャプチャ ミニドライバーでは、このプロパティがサポートされていません。

<a name="requirements"></a>必要条件
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Header</p></td>
<td>Ksmedia.h (Ksmedia.h を含む)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[**KSPROPERTY**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksidentifier)

[**KSPROPERTY\_VIDEOCOMPRESSION\_S**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-ksproperty_videocompression_s)

[**KSPROPERTY\_VIDEOCOMPRESSION\_GETINFO\_S**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-ksproperty_videocompression_getinfo_s)

 

 







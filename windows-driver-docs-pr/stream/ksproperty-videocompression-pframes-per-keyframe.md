---
title: KSK プロパティ\_VIDEOCOMPRESSION\_PFRAMES\_\_キーフレームごとに
description: KSK プロパティ\_VIDEOCOMPRESSION\_PFRAMES\_\_のキーフレームプロパティによって、予測フレーム (P フレーム) の間隔が制御されます。 このプロパティを実装する必要があります。
ms.assetid: feb839b4-32fc-4fe9-b015-019d9d683c66
keywords:
- KSPROPERTY_VIDEOCOMPRESSION_PFRAMES_PER_KEYFRAME ストリーミングメディアデバイス
topic_type:
- apiref
api_name:
- KSPROPERTY_VIDEOCOMPRESSION_PFRAMES_PER_KEYFRAME
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: f527ea071c16b7763e966b6a6292a54bb7fac9d0
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72837881"
---
# <a name="ksproperty_videocompression_pframes_per_keyframe"></a>KSK プロパティ\_VIDEOCOMPRESSION\_PFRAMES\_\_キーフレームごとに


KSK プロパティ\_VIDEOCOMPRESSION\_PFRAMES\_\_のキーフレームプロパティによって、予測フレーム (P フレーム) の間隔が制御されます。 このプロパティを実装する必要があります。

## <span id="ddk_ksproperty_videocompression_pframes_per_keyframe_ks"></span><span id="DDK_KSPROPERTY_VIDEOCOMPRESSION_PFRAMES_PER_KEYFRAME_KS"></span>


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
<td><p>対応</p></td>
<td><p>対応</p></td>
<td><p>フィルター</p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_videocompression_s" data-raw-source="[&lt;strong&gt;KSPROPERTY_VIDEOCOMPRESSION_S&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_videocompression_s)"><strong>KSPROPERTY_VIDEOCOMPRESSION_S</strong></a></p></td>
<td><p>長い</p></td>
</tr>
</tbody>
</table>

 

プロパティ値 (操作データ) は、キーフレームごとに予測されるフレームの数を指定する LONG です。

<a name="remarks"></a>注釈
-------

KSK プロパティの**値**メンバー\_videocompression\_S 構造体は、キーフレームごとの P フレームの数を指定します。 設定要求で負の値が**指定**されている場合、ミニドライバーは P フレームレートを既定値に設定する必要があります。

このプロパティをサポートするミニドライバーは、 [**ksproperty\_VIDEOCOMPRESSION\_GETINFO\_S**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_videocompression_getinfo_s)構造体の VideoCompressionCaps プロパティの**Capabilities**メンバーで、KS\_\_を設定する必要があります。ミニドライバーのビデオ圧縮機能を取得します。

<a name="requirements"></a>要件
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Header</p></td>
<td>Ksmedia .h (Ksk を含む)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[**KSPROPERTY**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksidentifier)

[**KSK プロパティ\_VIDEOCOMPRESSION\_S**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_videocompression_s)

[**KSK プロパティ\_VIDEOCOMPRESSION\_GETINFO\_S**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_videocompression_getinfo_s)

 

 







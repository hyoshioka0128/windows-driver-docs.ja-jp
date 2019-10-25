---
title: KSK プロパティ\_VIDEOCOMPRESSION\_品質
description: KSK プロパティ\_VIDECOMPRESSION\_QUALITY プロパティは、ビデオの圧縮品質設定を制御します。 このプロパティを実装する必要があります。
ms.assetid: 7566f60e-fe49-4009-bd61-b29d2adb4e8c
keywords:
- KSPROPERTY_VIDEOCOMPRESSION_QUALITY ストリーミングメディアデバイス
topic_type:
- apiref
api_name:
- KSPROPERTY_VIDEOCOMPRESSION_QUALITY
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 79ad71a6dde954232db80118201ce690150d0bfd
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72837880"
---
# <a name="ksproperty_videocompression_quality"></a>KSK プロパティ\_VIDEOCOMPRESSION\_品質


KSK プロパティ\_VIDECOMPRESSION\_QUALITY プロパティは、ビデオの圧縮品質設定を制御します。 このプロパティを実装する必要があります。

## <span id="ddk_ksproperty_videocompression_quality_ks"></span><span id="DDK_KSPROPERTY_VIDEOCOMPRESSION_QUALITY_KS"></span>


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
<th>[購入]</th>
<th>設定</th>
<th>対象</th>
<th>プロパティ記述子の型</th>
<th>プロパティ値の型</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>[はい]</p></td>
<td><p>[はい]</p></td>
<td><p>フィルター</p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_videocompression_s" data-raw-source="[&lt;strong&gt;KSPROPERTY_VIDEOCOMPRESSION_S&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_videocompression_s)"><strong>KSPROPERTY_VIDEOCOMPRESSION_S</strong></a></p></td>
<td><p>長い</p></td>
</tr>
</tbody>
</table>

 

プロパティ値 (操作データ) は、ビデオ圧縮の品質値を指定する LONG です。

<a name="remarks"></a>注釈
-------

KSK プロパティの**値**メンバー\_videocompression\_S 構造体は、品質評価基準を指定します。

このプロパティの値の範囲は 0 ~ 1万です。 0は、最も低い品質を示し、最大値は1万です。 ミニドライバーによって、独自の既定値が決定されます。

このプロパティをサポートするミニドライバーは、 [**ksproperty\_VIDEOCOMPRESSION\_GETINFO\_S**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_videocompression_getinfo_s)構造体の**機能**メンバーで**KS\_CompressionCaps\_canquality**フラグを設定する必要があります。ミニドライバーのビデオ圧縮機能を取得します。 ミニドライバーで KS\_CompressionCaps\_CanQuality が設定されている場合は、プロパティに対して get と set の両方の要求をサポートする必要があります。

このプロパティの値の範囲は 0 ~ 1万です。 0は、最も低い品質を示し、最大値は1万です。 ミニドライバーによって、独自の既定値が決定されます。

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

 

 







---
title: KSPROPERTY\_VIDEOCOMPRESSION\_品質
description: KSPROPERTY\_VIDECOMPRESSION\_品質プロパティは、ビデオの圧縮品質の設定を制御します。 このプロパティを実装する必要があります。
ms.assetid: 7566f60e-fe49-4009-bd61-b29d2adb4e8c
keywords:
- KSPROPERTY_VIDEOCOMPRESSION_QUALITY ストリーミング メディア デバイス
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
ms.openlocfilehash: 39f1e1e8f4f2a4ed9ba8cd650eb9cb479172e4b2
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56531692"
---
# <a name="kspropertyvideocompressionquality"></a>KSPROPERTY\_VIDEOCOMPRESSION\_品質


KSPROPERTY\_VIDECOMPRESSION\_品質プロパティは、ビデオの圧縮品質の設定を制御します。 このプロパティを実装する必要があります。

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
<th>取得</th>
<th>設定</th>
<th>対象</th>
<th>プロパティ記述子の型</th>
<th>プロパティ値の型</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>〇</p></td>
<td><p>〇</p></td>
<td><p>フィルター</p></td>
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff566018" data-raw-source="[&lt;strong&gt;KSPROPERTY_VIDEOCOMPRESSION_S&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff566018)"><strong>KSPROPERTY_VIDEOCOMPRESSION_S</strong></a></p></td>
<td><p>長い</p></td>
</tr>
</tbody>
</table>

 

プロパティの値 (データの操作) は、ビデオの圧縮品質の値を指定する LONG が。

<a name="remarks"></a>注釈
-------

**値**、KSPROPERTY のメンバー\_VIDEOCOMPRESSION\_構造が品質基準を指定します。

このプロパティ範囲を 0 から 10000 の値。 0 は、最低の品質、10000 を示します。 最高の値。 ミニドライバーは、既定値を決定します。

このプロパティをサポートするミニドライバーを設定する必要があります、 **KS\_CompressionCaps\_CanQuality**フラグ、**機能**のメンバー、 [ **KSPROPERTY\_VIDEOCOMPRESSION\_GETINFO\_S** ](https://msdn.microsoft.com/library/windows/hardware/ff565979)ミニドライバーのビデオの圧縮機能を取得する構造体。 ミニドライバーは、KS を設定する場合\_CompressionCaps\_CanQuality をサポートすることが両方を取得し、要求のプロパティを設定します。

このプロパティ範囲を 0 から 10000 の値。 0 は、最低の品質、10000 を示します。 最高の値。 ミニドライバーは、既定値を決定します。

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
<td>Ksmedia.h (Ksmedia.h を含む)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[**KSPROPERTY**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksidentifier)

[**KSPROPERTY\_VIDEOCOMPRESSION\_S**](https://msdn.microsoft.com/library/windows/hardware/ff566018)

[**KSPROPERTY\_VIDEOCOMPRESSION\_GETINFO\_S**](https://msdn.microsoft.com/library/windows/hardware/ff565979)

 

 







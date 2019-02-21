---
title: KSPROPERTY\_VIDEOCOMPRESSION\_PFRAMES\_1 秒あたり\_キーフレーム
description: KSPROPERTY\_VIDEOCOMPRESSION\_PFRAMES\_1 秒あたり\_キーフレームのプロパティは、予測フレーム (P フレーム) の間隔を制御します。 このプロパティを実装する必要があります。
ms.assetid: feb839b4-32fc-4fe9-b015-019d9d683c66
keywords:
- KSPROPERTY_VIDEOCOMPRESSION_PFRAMES_PER_KEYFRAME ストリーミング メディア デバイス
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
ms.openlocfilehash: a5e2e2810e2ff1f53a371cf1b90a838b6bf9ff3f
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56536401"
---
# <a name="kspropertyvideocompressionpframesperkeyframe"></a>KSPROPERTY\_VIDEOCOMPRESSION\_PFRAMES\_1 秒あたり\_キーフレーム


KSPROPERTY\_VIDEOCOMPRESSION\_PFRAMES\_1 秒あたり\_キーフレームのプロパティは、予測フレーム (P フレーム) の間隔を制御します。 このプロパティを実装する必要があります。

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
<td><p>〇</p></td>
<td><p>〇</p></td>
<td><p>フィルター</p></td>
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff566018" data-raw-source="[&lt;strong&gt;KSPROPERTY_VIDEOCOMPRESSION_S&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff566018)"><strong>KSPROPERTY_VIDEOCOMPRESSION_S</strong></a></p></td>
<td><p>長い</p></td>
</tr>
</tbody>
</table>

 

プロパティ値 (データの操作) がキー フレームごとの予測のフレームの数を指定します。

<a name="remarks"></a>注釈
-------

**値**、KSPROPERTY のメンバー\_VIDEOCOMPRESSION\_構造のキー フレームごとの P フレームの数を指定します。 セットの要求は、負の値を提供する場合**値**、ミニドライバーは、既定値に、P フレーム レートを設定する必要があります。

このプロパティをサポートするミニドライバーは、KS を設定する必要があります\_VideoCompressionCaps\_CanBFrame フラグ、**機能**のメンバー、 [ **KSPROPERTY\_VIDEOCOMPRESSION\_GETINFO\_S** ](https://msdn.microsoft.com/library/windows/hardware/ff565979)ミニドライバーのビデオの圧縮機能を取得する構造体。

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

 

 







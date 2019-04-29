---
title: KSPROPERTY\_ビデオ プロシージャ アンプ\_彩度
description: KSPROPERTY\_ビデオ プロシージャ アンプ\_彩度プロパティは、カメラの彩度、または値の彩度の向上の設定を制御します。 このプロパティは省略可能です。
ms.assetid: 1b7fd731-088b-4370-a537-9e302d28864b
keywords:
- KSPROPERTY_VIDEOPROCAMP_SATURATION ストリーミング メディア デバイス
topic_type:
- apiref
api_name:
- KSPROPERTY_VIDEOPROCAMP_SATURATION
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: a29a4e9b65af4dfde10f9524ee1ea2db3d6a02e4
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63327045"
---
# <a name="kspropertyvideoprocampsaturation"></a>KSPROPERTY\_ビデオ プロシージャ アンプ\_彩度


KSPROPERTY\_ビデオ プロシージャ アンプ\_彩度プロパティは、カメラの彩度、または値の彩度の向上の設定を制御します。 このプロパティは省略可能です。

## <span id="ddk_ksproperty_videoprocamp_saturation_ks"></span><span id="DDK_KSPROPERTY_VIDEOPROCAMP_SATURATION_KS"></span>


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
<td><p>フィルターまたはノード</p></td>
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff566089" data-raw-source="[&lt;strong&gt;KSPROPERTY_VIDEOPROCAMP_S&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff566089)"><strong>KSPROPERTY_VIDEOPROCAMP_S</strong> </a>または<a href="https://msdn.microsoft.com/library/windows/hardware/ff566080" data-raw-source="[&lt;strong&gt;KSPROPERTY_VIDEOPROCAMP_NODE_S&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff566080)"> <strong>KSPROPERTY_VIDEOPROCAMP_NODE_S</strong></a></p></td>
<td><p>LONG</p></td>
</tr>
</tbody>
</table>

 

プロパティの値 (データの操作) は、カメラの彩度 設定を指定する LONG が。 鮮やかさの設定の値は 100 倍してゲインとして表されます。

<a name="remarks"></a>注釈
-------

**値**、KSPROPERTY のメンバー\_ビデオ プロシージャ アンプ\_構造が飽和状態設定を指定します。

すべてのビデオ キャプチャ ミニドライバーには、このプロパティの値を範囲と既定値を定義する必要があります。 必要な範囲は 0 ~ 10000 である必要があります。 既定値は 100 (1 x) である必要があります。

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

[**KSPROPERTY\_ビデオ プロシージャ アンプ\_S**](https://msdn.microsoft.com/library/windows/hardware/ff566089)

 

 







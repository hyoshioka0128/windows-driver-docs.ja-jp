---
title: KSPROPERTY\_VIDEOCOMPRESSION\_オーバーライド\_キーフレーム
description: KSPROPERTY\_VIDEOCOMPRESSION\_オーバーライド\_キーフレームのプロパティは、キー フレーム レートを一時的に上書きします。 このプロパティは省略可能です。
ms.assetid: 068bd5e6-e283-4c8d-8837-c0e0cef4df65
keywords:
- KSPROPERTY_VIDEOCOMPRESSION_OVERRIDE_KEYFRAME ストリーミング メディア デバイス
topic_type:
- apiref
api_name:
- KSPROPERTY_VIDEOCOMPRESSION_OVERRIDE_KEYFRAME
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 60eb32acd4f6622727f6fd576976d6d2b4cbbd0e
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63355517"
---
# <a name="kspropertyvideocompressionoverridekeyframe"></a>KSPROPERTY\_VIDEOCOMPRESSION\_オーバーライド\_キーフレーム


KSPROPERTY\_VIDEOCOMPRESSION\_オーバーライド\_キーフレームのプロパティは、キー フレーム レートを一時的に上書きします。 このプロパティは省略可能です。

## <span id="ddk_ksproperty_videocompression_override_keyframe_ks"></span><span id="DDK_KSPROPERTY_VIDEOCOMPRESSION_OVERRIDE_KEYFRAME_KS"></span>


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
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff566018" data-raw-source="[&lt;strong&gt;KSPROPERTY_VIDEOCOMPRESSION_S&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff566018)"><strong>KSPROPERTY_VIDEOCOMPRESSION_S</strong></a></p></td>
<td><p>LONG</p></td>
</tr>
</tbody>
</table>

 

プロパティ値 (データの操作) が新しいキー フレームの画像数を指定します。

<a name="remarks"></a>注釈
-------

**値**、KSPROPERTY のメンバー\_VIDEOCOMPRESSION\_構造のキー フレームを作成するフレームの数を指定します。

ビデオ キャプチャ ミニドライバーでは、このプロパティがサポートされていません。

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

 

 







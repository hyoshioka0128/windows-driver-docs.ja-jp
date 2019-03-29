---
title: KSPROPERTY\_VIDEOCOMPRESSION\_キーフレーム\_率
description: KSPROPERTY\_VIDEOCOMPRESSION\_キーフレーム\_レート プロパティは、キー フレーム レートを制御します。 このプロパティを実装する必要があります。
ms.assetid: 2b39dbe4-5010-4454-92ca-699b3b2c21ac
keywords:
- KSPROPERTY_VIDEOCOMPRESSION_KEYFRAME_RATE ストリーミング メディア デバイス
topic_type:
- apiref
api_name:
- KSPROPERTY_VIDEOCOMPRESSION_KEYFRAME_RATE
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8350872822a8cd0ba39941b1f512e75503cd0724
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56575093"
---
# <a name="kspropertyvideocompressionkeyframerate"></a>KSPROPERTY\_VIDEOCOMPRESSION\_キーフレーム\_率


KSPROPERTY\_VIDEOCOMPRESSION\_キーフレーム\_レート プロパティは、キー フレーム レートを制御します。 このプロパティを実装する必要があります。

## <span id="ddk_ksproperty_videocompression_keyframe_rate_ks"></span><span id="DDK_KSPROPERTY_VIDEOCOMPRESSION_KEYFRAME_RATE_KS"></span>


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
<th>Set</th>
<th>移行先</th>
<th>プロパティ記述子の型</th>
<th>プロパティ値の型</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>はい</p></td>
<td><p>はい</p></td>
<td><p>フィルター</p></td>
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff566018" data-raw-source="[&lt;strong&gt;KSPROPERTY_VIDEOCOMPRESSION_S&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff566018)"><strong>KSPROPERTY_VIDEOCOMPRESSION_S</strong></a></p></td>
<td><p>長い</p></td>
</tr>
</tbody>
</table>

 

プロパティの値 (データの操作) は、キー フレーム レートを指定する LONG が。

<a name="remarks"></a>コメント
-------

**値**、KSPROPERTY のメンバー\_VIDEOCOMPRESSION\_構造、プロパティの設定を指定します。

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

[**KSPROPERTY\_VIDEOCOMPRESSION\_S**](https://msdn.microsoft.com/library/windows/hardware/ff566018)

 

 







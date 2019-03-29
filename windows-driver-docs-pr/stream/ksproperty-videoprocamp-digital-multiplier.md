---
title: KSPROPERTY\_ビデオ プロシージャ アンプ\_デジタル\_乗数
description: KSPROPERTY\_ビデオ プロシージャ アンプ\_デジタル\_乗数のプロパティは、イメージに適用するズームをデジタルの量を指定します。
ms.assetid: e566dd2b-d99a-4e7f-888e-f0f431618c2d
keywords:
- KSPROPERTY_VIDEOPROCAMP_DIGITAL_MULTIPLIER ストリーミング メディア デバイス
topic_type:
- apiref
api_name:
- KSPROPERTY_VIDEOPROCAMP_DIGITAL_MULTIPLIER
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 611cddf64c30e7fc4e4c52a87bb6400b614798cd
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56574405"
---
# <a name="kspropertyvideoprocampdigitalmultiplier"></a>KSPROPERTY\_ビデオ プロシージャ アンプ\_デジタル\_乗数


KSPROPERTY\_ビデオ プロシージャ アンプ\_デジタル\_乗数のプロパティは、イメージに適用するズームをデジタルの量を指定します。

## <span id="ddk_ksproperty_videoprocamp_digital_multiplier_ks"></span><span id="DDK_KSPROPERTY_VIDEOPROCAMP_DIGITAL_MULTIPLIER_KS"></span>


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
<td><p>フィルターまたはノード</p></td>
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff566089" data-raw-source="[&lt;strong&gt;KSPROPERTY_VIDEOPROCAMP_S&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff566089)"><strong>KSPROPERTY_VIDEOPROCAMP_S</strong> </a>または<a href="https://msdn.microsoft.com/library/windows/hardware/ff566080" data-raw-source="[&lt;strong&gt;KSPROPERTY_VIDEOPROCAMP_NODE_S&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff566080)"> <strong>KSPROPERTY_VIDEOPROCAMP_NODE_S</strong></a></p></td>
<td><p>長い</p></td>
</tr>
</tbody>
</table>

 

プロパティの値 (データの操作) は、カメラのデジタル乗数の設定を指定する LONG が。 値は、カメラが画像に適用されるデジタル乗数値を指定します。

<a name="remarks"></a>コメント
-------

クライアントがデジタル乗数値を指定する必要がありますセット要求を行うときに、**値**、KSPROPERTY のメンバー\_ビデオ プロシージャ アンプ\_ノード\_S 構造体。

デバイスによってサポートされるデジタルの乗数値の範囲を確認するのには、アプリケーションが、KSPROPERTY を発行できます\_型\_BASICSUPPORT 要求。 KSPROPERTY を指定する\_型\_で BASICSUPPORT、**フラグ**のメンバー、 [ **KSPROPERTY\_項目**](https://msdn.microsoft.com/library/windows/hardware/ff565176)構造体。

クライアントが型の値を受け取る get 要求を行うときに時間の長いで、**値**、KSPROPERTY のメンバー\_ビデオ プロシージャ アンプ\_ノード\_S 構造体。

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

[**KSPROPERTY\_ビデオ プロシージャ アンプ\_S**](https://msdn.microsoft.com/library/windows/hardware/ff566089)

 

 







---
title: KSK プロパティ\_VIDEODECODER\_出力\_有効にする
description: KSK プロパティ\_VIDEODECODER\_出力\_有効にすると、共有ビデオポートバス上に存在するビデオデコーダーの3つの状態の出力が制御されます。 このプロパティは省略可能です。
ms.assetid: 33c9a3d2-ffc0-4460-abc4-56bc83c64b55
keywords:
- KSPROPERTY_VIDEODECODER_OUTPUT_ENABLE ストリーミングメディアデバイス
topic_type:
- apiref
api_name:
- KSPROPERTY_VIDEODECODER_OUTPUT_ENABLE
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: f3ebec2f6f3816dbc7a6dc74487915c5559424eb
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72837867"
---
# <a name="ksproperty_videodecoder_output_enable"></a>KSK プロパティ\_VIDEODECODER\_出力\_有効にする


KSK プロパティ\_VIDEODECODER\_出力\_有効にすると、共有ビデオポートバス上に存在するビデオデコーダーの3つの状態の出力が制御されます。 このプロパティは省略可能です。

## <span id="ddk_ksproperty_videodecoder_output_enable_ks"></span><span id="DDK_KSPROPERTY_VIDEODECODER_OUTPUT_ENABLE_KS"></span>


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
<td><p>Pin</p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_videodecoder_s" data-raw-source="[&lt;strong&gt;KSPROPERTY_VIDEODECODER_S&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_videodecoder_s)"><strong>KSPROPERTY_VIDEODECODER_S</strong></a></p></td>
<td><p>ULONG</p></td>
</tr>
</tbody>
</table>

 

プロパティ値 (操作データ) は、3つの状態の出力有効設定を指定する ULONG です。 値が0の場合は、3つの状態の出力を示します。 0以外の値は、デバイスがビデオポートバスをアクティブに運転していることを示します。

<a name="remarks"></a>注釈
-------

KSK プロパティの**値**メンバー\_videodecoder\_S 構造体で、3つの出力の enable 設定を指定します。

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

[**KSK プロパティ\_VIDEODECODER\_S**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_videodecoder_s)

 

 







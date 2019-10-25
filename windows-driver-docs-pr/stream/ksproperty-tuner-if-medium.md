---
title: KSK プロパティ\_チューナー\_(\_中)
description: KSK プロパティ\_チューナー\_\_メディアは、デジタルテレビのチューニングをサポートするデバイスの中間周波数の pin のメディアを表します。 このプロパティは省略可能です。
ms.assetid: 1144777c-e81c-4b8f-a634-411591c71356
keywords:
- KSPROPERTY_TUNER_IF_MEDIUM ストリーミングメディアデバイス
topic_type:
- apiref
api_name:
- KSPROPERTY_TUNER_IF_MEDIUM
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: d21ef1f5a5d48c2525c3d4a74b54e447da431b3e
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72837915"
---
# <a name="ksproperty_tuner_if_medium"></a>KSK プロパティ\_チューナー\_(\_中)


KSK プロパティ\_チューナー\_\_メディアは、デジタルテレビのチューニングをサポートするデバイスの中間周波数の pin のメディアを表します。 このプロパティは省略可能です。

## <span id="ddk_ksproperty_tuner_if_medium_ks"></span><span id="DDK_KSPROPERTY_TUNER_IF_MEDIUM_KS"></span>


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
<td><p>必須ではない</p></td>
<td><p>Pin</p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_tuner_if_medium_s" data-raw-source="[&lt;strong&gt;KSPROPERTY_TUNER_IF_MEDIUM_S&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_tuner_if_medium_s)"><strong>KSPROPERTY_TUNER_IF_MEDIUM_S</strong></a></p></td>
<td><p><a href="https://docs.microsoft.com/previous-versions/ff563538(v=vs.85)" data-raw-source="[&lt;strong&gt;KSPIN_MEDIUM&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/ff563538(v=vs.85))"><strong>KSPIN_MEDIUM</strong></a></p></td>
</tr>
</tbody>
</table>

 

プロパティ値 (操作データ) は、中間周波数へのチューニングをサポートできるピンの中程度の GUID を指定する KSPIN\_中構造です。

<a name="remarks"></a>注釈
-------

中\_S 構造体\_場合は、KSK プロパティの**ifmedium**メンバー\_\_チューナーは、中間周波数の Pin の中程度の GUID を指定します。

ビデオキャプチャミニドライバーで KSK プロパティ\_チューナー\_サポートされている場合は、[メディア\_] を選択すると、*チューナーから送信*されたハードウェアベースの mpeg-2 トランスポートストリームを表す追加の pin が作成されます。 この pin は、グラフトポロジを定義するためだけに使用されます。 *Kstvtune.ax*のこの pin からユーザーモードストリームを通過するデータサンプルは、 [**KS\_TVTUNER\_CHANGE\_INFO**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagks_tvtuner_change_info)構造体で構成されています。

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

[ **\_中\_S の場合は、KSK プロパティ\_チューナー\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_tuner_if_medium_s)

 

 







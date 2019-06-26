---
title: KSPROPERTY\_クロスバー\_PININFO
description: KSPROPERTY\_クロスバー\_PININFO プロパティをデータ フローの方向、中規模の GUID(s) と暗証番号 (pin) の種類などの設定を含む暗証番号 (pin) によって表される物理接続の種類を取得します。
ms.assetid: d025b401-bc75-40d6-a367-1b98e065a48d
keywords:
- KSPROPERTY_CROSSBAR_PININFO ストリーミング メディア デバイス
topic_type:
- apiref
api_name:
- KSPROPERTY_CROSSBAR_PININFO
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: b5c5817fc58ac05639abfffb611e265738278423
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67373077"
---
# <a name="kspropertycrossbarpininfo"></a>KSPROPERTY\_クロスバー\_PININFO


KSPROPERTY\_クロスバー\_PININFO プロパティをデータ フローの方向、中規模の GUID(s) と暗証番号 (pin) の種類などの設定を含む暗証番号 (pin) によって表される物理接続の種類を取得します。 ビデオ ピンを特定のビデオ ピンに関連付けられたオーディオの pin があるかどうかをこのプロパティも示します。 このプロパティを実装する必要があります。

## <span id="ddk_ksproperty_crossbar_pininfo_ks"></span><span id="DDK_KSPROPERTY_CROSSBAR_PININFO_KS"></span>


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
<td><p>X</p></td>
<td><p>フィルター</p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-ksproperty_crossbar_pininfo_s" data-raw-source="[&lt;strong&gt;KSPROPERTY_CROSSBAR_PININFO_S&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-ksproperty_crossbar_pininfo_s)"><strong>KSPROPERTY_CROSSBAR_PININFO_S</strong></a></p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-ksproperty_crossbar_pininfo_s" data-raw-source="[&lt;strong&gt;KSPROPERTY_CROSSBAR_PININFO_S&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-ksproperty_crossbar_pininfo_s)"><strong>KSPROPERTY_CROSSBAR_PININFO_S</strong></a></p></td>
</tr>
</tbody>
</table>

 

プロパティの値 (データの操作) は、KSPROPERTY\_クロスバー\_PININFO\_S 構造体。

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

[**KSPROPERTY\_クロスバー\_PININFO\_S**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-ksproperty_crossbar_pininfo_s)

 

 







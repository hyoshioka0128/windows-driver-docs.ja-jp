---
title: KSPROPERTY\_チューナー\_場合\_中
description: KSPROPERTY\_チューナー\_場合\_中は、デジタル テレビのチューニングをサポートするデバイスの中間頻度暗証番号 (pin) の中をについて説明します。 このプロパティは省略可能です。
ms.assetid: 1144777c-e81c-4b8f-a634-411591c71356
keywords:
- KSPROPERTY_TUNER_IF_MEDIUM ストリーミング メディア デバイス
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
ms.openlocfilehash: 445074b364830feb5db04c97448226ba3ff8ad3a
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56527253"
---
# <a name="kspropertytunerifmedium"></a>KSPROPERTY\_チューナー\_場合\_中


KSPROPERTY\_チューナー\_場合\_中は、デジタル テレビのチューニングをサポートするデバイスの中間頻度暗証番号 (pin) の中をについて説明します。 このプロパティは省略可能です。

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
<td><p>Pin</p></td>
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff565848" data-raw-source="[&lt;strong&gt;KSPROPERTY_TUNER_IF_MEDIUM_S&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff565848)"><strong>KSPROPERTY_TUNER_IF_MEDIUM_S</strong></a></p></td>
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff563538" data-raw-source="[&lt;strong&gt;KSPIN_MEDIUM&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff563538)"><strong>KSPIN_MEDIUM</strong></a></p></td>
</tr>
</tbody>
</table>

 

プロパティの値 (データの操作) は、KSPIN\_が中間の頻度にチューニングをサポートできる暗証番号 (pin) の中の GUID を指定する中規模の構造体。

<a name="remarks"></a>注釈
-------

**IFMedium** 、KSPROPERTY のメンバー\_チューナー\_場合\_MEDIUM\_構造が中間頻度の暗証番号 (pin) の中の GUID を指定します。

ビデオ キャプチャ ミニドライバー KSPROPERTY をサポートしている場合\_チューナー\_場合\_中]、[ *kstvtune.ax*ハードウェア ベースの mpeg-2 トランスポート ストリームを表す追加の pin を作成します。チューナーで発生します。 この pin は、グラフのトポロジを定義するためだけに使用されます。 データのサンプルで、この暗証番号 (pin) からユーザー モードのストリームを通過*kstvtune.ax*から成る[ **KS\_tv チューナー\_変更\_情報**](https://msdn.microsoft.com/library/windows/hardware/ff567691)構造体。

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

[**KSPROPERTY\_チューナー\_場合\_MEDIUM\_S**](https://msdn.microsoft.com/library/windows/hardware/ff565848)

 

 







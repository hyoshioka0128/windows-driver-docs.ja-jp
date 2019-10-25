---
title: KSK プロパティ\_チューナー\_キャップ
description: KSK プロパティ\_チューナー\_CAPS プロパティは、チューナーの基本機能を記述します。 このプロパティを実装する必要があります。
ms.assetid: 70255053-d241-44ca-ba24-cfc442629ab3
keywords:
- KSPROPERTY_TUNER_CAPS ストリーミングメディアデバイス
topic_type:
- apiref
api_name:
- KSPROPERTY_TUNER_CAPS
api_location:
- ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 21d1bb6509b12196f41570936522165a65b21338
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72837919"
---
# <a name="ksproperty_tuner_caps"></a>KSK プロパティ\_チューナー\_キャップ


KSK プロパティ\_チューナー\_CAPS プロパティは、チューナーの基本機能を記述します。 このプロパティを実装する必要があります。

## <span id="ddk_ksproperty_tuner_caps_ks"></span><span id="DDK_KSPROPERTY_TUNER_CAPS_KS"></span>


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
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_tuner_caps_s" data-raw-source="[&lt;strong&gt;KSPROPERTY_TUNER_CAPS_S&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_tuner_caps_s)"><strong>KSPROPERTY_TUNER_CAPS_S</strong></a></p></td>
<td><p>ULONG</p></td>
</tr>
</tbody>
</table>

 

プロパティ値 (操作データ) は、streaming ミニドライバーによってサポートされるチューニングモードを指定する LONG です。

<a name="remarks"></a>注釈
-------

KSK プロパティ\_チューナー\_CAPS\_S 構造体のモードで**サポート**されているメンバーは、video capture ミニドライバーによってサポートされるチューニングモードを示します。

1つのチューニングデバイスで、デジタルテレビ、アナログテレビ、AM/FM ラジオ、およびデジタルサテライトシステム (DSS) のチューニングをサポートする場合があります。

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

[**KSK プロパティ\_チューナー\_CAPS\_S**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_tuner_caps_s)

[**KSK プロパティ\_チューナー\_モード\_キャップ**](ksproperty-tuner-mode-caps.md)

 

 







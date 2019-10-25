---
title: KSK プロパティ\_チューナー\_モード
description: ユーザーモードクライアントは、KSK プロパティ\_チューナー\_MODE プロパティを使用して、アナログテレビ、デジタルテレビ、FM、AM、DSS などのデバイスのチューニングモードを取得または設定します。 このプロパティを実装する必要があります。
ms.assetid: 84df4030-3836-48de-be83-ecd749839081
keywords:
- KSPROPERTY_TUNER_MODE ストリーミングメディアデバイス
topic_type:
- apiref
api_name:
- KSPROPERTY_TUNER_MODE
api_location:
- ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: b7e3e7891b71f706caafd3309ca3a1cc171f841e
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72837912"
---
# <a name="ksproperty_tuner_mode"></a>KSK プロパティ\_チューナー\_モード


ユーザーモードクライアントは、KSK プロパティ\_チューナー\_MODE プロパティを使用して、アナログテレビ、デジタルテレビ、FM、AM、DSS などのデバイスのチューニングモードを取得または設定します。 このプロパティを実装する必要があります。

## <span id="ddk_ksproperty_tuner_mode_ks"></span><span id="DDK_KSPROPERTY_TUNER_MODE_KS"></span>


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
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_tuner_mode_s" data-raw-source="[&lt;strong&gt;KSPROPERTY_TUNER_MODE_S&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_tuner_mode_s)"><strong>KSPROPERTY_TUNER_MODE_S</strong></a></p></td>
<td><p>ULONG</p></td>
</tr>
</tbody>
</table>

 

プロパティ値 (操作データ) は、チューナーの現在のチューニングモードを指定する ULONG です。

<a name="remarks"></a>注釈
-------

KSK プロパティ\_チューナー\_モード\_S 構造体の**モード**メンバーは、現在のチューナーモードを指定します。

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

[**KSK プロパティ\_チューナー\_モード\_S**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_tuner_mode_s)

 

 







---
title: KSK プロパティ\_VIDEOPROCAMP\_デジタル\_乗数\_制限
description: KSK プロパティ\_VIDEOPROCAMP\_DIGITAL\_乗数\_LIMIT プロパティは、イメージに適用できるデジタルズームの量の上限を指定します。
ms.assetid: 66cc1dd5-3e07-47d8-bb30-b64b90b07ad9
keywords:
- KSPROPERTY_VIDEOPROCAMP_DIGITAL_MULTIPLIER_LIMIT ストリーミングメディアデバイス
topic_type:
- apiref
api_name:
- KSPROPERTY_VIDEOPROCAMP_DIGITAL_MULTIPLIER_LIMIT
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: dc616d9ac9ae1b3c52039bfd8cf263e4dbb0f1cb
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844761"
---
# <a name="ksproperty_videoprocamp_digital_multiplier_limit"></a>KSK プロパティ\_VIDEOPROCAMP\_デジタル\_乗数\_制限


KSK プロパティ\_VIDEOPROCAMP\_DIGITAL\_乗数\_LIMIT プロパティは、イメージに適用できるデジタルズームの量の上限を指定します。

## <span id="ddk_ksproperty_videoprocamp_digital_multiplier_limit_ks"></span><span id="DDK_KSPROPERTY_VIDEOPROCAMP_DIGITAL_MULTIPLIER_LIMIT_KS"></span>


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
<td><p>フィルターまたはノード</p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_videoprocamp_s" data-raw-source="[&lt;strong&gt;KSPROPERTY_VIDEOPROCAMP_S&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_videoprocamp_s)"><strong>KSPROPERTY_VIDEOPROCAMP_S</strong></a>または<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_videoprocamp_node_s" data-raw-source="[&lt;strong&gt;KSPROPERTY_VIDEOPROCAMP_NODE_S&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_videoprocamp_node_s)"> <strong>KSPROPERTY_VIDEOPROCAMP_NODE_S</strong></a></p></td>
<td><p>長い</p></td>
</tr>
</tbody>
</table>

 

プロパティ値 (操作データ) は、カメラのデジタル乗数の上限を指定する LONG です。 値は、デバイスが光学画像に適用できるデジタル乗数の最大値を指定します。

<a name="remarks"></a>注釈
-------

クライアントは、set 要求を行うときに、KSK プロパティ\_VIDEOPROCAMP\_NODE\_S 構造体の**値**メンバーにデジタル乗数値を指定する必要があります。

クライアントは、設定要求を使用して、ユーザー定義のデジタルズームの上限を設定できます。

Get 要求を行うと、クライアントは、VIDEOPROCAMP\_NODE\_S 構造体\_、KSPROPERTY の**値**メンバーの前の値のいずれかを受け取ります。

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

[**KSK プロパティ\_VIDEOPROCAMP\_S**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_videoprocamp_s)

 

 







---
title: KSPROPERTY\_VIDEOPROCAMP\_の鮮明度
description: KSK プロパティ\_VIDEOPROCAMP\_鮮明度プロパティは、カメラの鮮明度の設定を制御します。 このプロパティは省略可能です。
ms.assetid: d6b10876-313b-420a-9d81-348030e580dd
keywords:
- KSPROPERTY_VIDEOPROCAMP_SHARPNESS ストリーミングメディアデバイス
topic_type:
- apiref
api_name:
- KSPROPERTY_VIDEOPROCAMP_SHARPNESS
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7a372f585649fbce5bdbf91b52df817815664dc0
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842413"
---
# <a name="ksproperty_videoprocamp_sharpness"></a>KSPROPERTY\_VIDEOPROCAMP\_の鮮明度


KSK プロパティ\_VIDEOPROCAMP\_鮮明度プロパティは、カメラの鮮明度の設定を制御します。 このプロパティは省略可能です。

## <span id="ddk_ksproperty_videoprocamp_sharpness_ks"></span><span id="DDK_KSPROPERTY_VIDEOPROCAMP_SHARPNESS_KS"></span>


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

 

プロパティ値 (操作データ) は、カメラの鮮明度の設定を指定する LONG です。 鮮明度は任意の単位で表現されます。

<a name="remarks"></a>注釈
-------

VIDEOPROCAMP\_S 構造体\_KSK プロパティの**値**メンバーは、鮮明度の設定を指定します。

すべてのビデオキャプチャミニドライバーで、このプロパティの値の範囲と既定値を定義する必要があります。 必要な範囲は 0 ~ 100 でなければなりません。 既定値は50である必要があります。

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

 

 







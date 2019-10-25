---
title: KSK プロパティ\_CAMERACONTROL\_PANTILT
description: KSK プロパティ\_CAMERACONTROL\_PANTILT プロパティは、絶対パンと傾きの設定を指定します。
ms.assetid: d6f151c9-a428-4d76-9854-5064d901643e
keywords:
- KSPROPERTY_CAMERACONTROL_PANTILT ストリーミングメディアデバイス
topic_type:
- apiref
api_name:
- KSPROPERTY_CAMERACONTROL_PANTILT
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 807c81955d5c52d724a9d7d6e855b63f04c2ce87
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843342"
---
# <a name="ksproperty_cameracontrol_pantilt"></a>KSK プロパティ\_CAMERACONTROL\_PANTILT


KSK プロパティ\_CAMERACONTROL\_PANTILT プロパティは、絶対パンと傾きの設定を指定します。

## <span id="ddk_ksproperty_cameracontrol_pantilt_ks"></span><span id="DDK_KSPROPERTY_CAMERACONTROL_PANTILT_KS"></span>


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
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_cameracontrol_s2" data-raw-source="[&lt;strong&gt;KSPROPERTY_CAMERACONTROL_S2&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_cameracontrol_s2)"><strong>KSPROPERTY_CAMERACONTROL_S2</strong></a>または<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_cameracontrol_node_s2" data-raw-source="[&lt;strong&gt;KSPROPERTY_CAMERACONTROL_NODE_S2&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_cameracontrol_node_s2)"><strong>KSPROPERTY_CAMERACONTROL_NODE_S2</strong></a>は、要求がフィルターとノードのどちらであるかによって異なります。</p></td>
<td><p>長整数のペア</p></td>
</tr>
</tbody>
</table>

 

プロパティ値 (操作データ) は、カメラの絶対パンと傾きの設定を指定する長整数のペアです。 これらの値は、アーク秒単位で表現されます。

1つ目の弧は、1度の1/3600 です。 使用可能な値の範囲は、− 180\*3600 ~ + 180\*3600 arc 秒です。 パンまたは傾きの値が指定されていない場合、既定値は0です。

パン要求を行うときは、正の値を指定してカメラを右に回転させ、負の値を指定してカメラを左に回転させます。

チルト要求を行うとき、正の値はカメラを上に傾斜させ、負の値を指定するとカメラが下がります。

<a name="remarks"></a>注釈
-------

[**Ksk プロパティ\_CAMERACONTROL\_s2**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_cameracontrol_s2)または[**KSK プロパティ\_CAMERACONTROL\_ノード\_s2**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_cameracontrol_node_s2)構造体の**Value1**メンバーは、pan 設定を指定します。 **Value2**メンバーは、傾きの設定を指定します。

<a name="requirements"></a>要件
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>バージョン</p></td>
<td><p>Windows Vista 以降のバージョンの Windows オペレーティングシステムで使用できます。</p></td>
</tr>
<tr class="even">
<td><p>Header</p></td>
<td>Ksmedia .h (Ksk を含む)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[**KSK プロパティ\_CAMERACONTROL\_S2**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_cameracontrol_s2)

[**KSPROPERTY\_CAMERACONTROL\_NODE\_S2**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_cameracontrol_node_s2)

 

 







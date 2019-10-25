---
title: KSK プロパティ\_CAMERACONTROL\_焦点\_の長さ
description: KSK プロパティ\_CAMERACONTROL\_焦点\_長さのプロパティは、カメラの焦点となる長さの情報を取得します。
ms.assetid: a7fba5e4-abd1-46ae-b93c-5fede0249771
keywords:
- KSPROPERTY_CAMERACONTROL_FOCAL_LENGTH ストリーミングメディアデバイス
topic_type:
- apiref
api_name:
- KSPROPERTY_CAMERACONTROL_FOCAL_LENGTH
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 28eef3519d1cf657f2a1e239a7aa00d8be8098d0
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72840465"
---
# <a name="ksproperty_cameracontrol_focal_length"></a>KSK プロパティ\_CAMERACONTROL\_焦点\_の長さ


KSK プロパティ\_CAMERACONTROL\_焦点\_長さのプロパティは、カメラの焦点となる長さの情報を取得します。

## <span id="ddk_ksproperty_cameracontrol_focal_length_ks"></span><span id="DDK_KSPROPERTY_CAMERACONTROL_FOCAL_LENGTH_KS"></span>


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
<td><p>フィルターまたはノード</p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_cameracontrol_focal_length_s" data-raw-source="[&lt;strong&gt;KSPROPERTY_CAMERACONTROL_FOCAL_LENGTH_S&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_cameracontrol_focal_length_s)"><strong>KSPROPERTY_CAMERACONTROL_FOCAL_LENGTH_S</strong></a>または<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_cameracontrol_node_focal_length_s" data-raw-source="[&lt;strong&gt;KSPROPERTY_CAMERACONTROL_NODE_FOCAL_LENGTH_S&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_cameracontrol_node_focal_length_s)"> <strong>KSPROPERTY_CAMERACONTROL_NODE_FOCAL_LENGTH_S</strong></a></p></td>
<td><p>長い</p></td>
</tr>
</tbody>
</table>

 

プロパティ値 (操作データ) は、カメラの焦点距離を指定する LONG です。

<a name="remarks"></a>注釈
-------

このプロパティ要求を使用して、ズーム値を解釈できます。 ズームの範囲は、 **lObjectiveFocalLengthMin**/**lOcularFocalLength**と**lObjectiveFocalLengthMax**/**lOcularFocalLength**の間である必要があります。 (**lOcularFocalLength**、 **LObjectiveFocalLengthMin**、および**lObjectiveFocalLengthMax**は、 [**KSK プロパティ\_CAMERACONTROL\_\_の長さ\_S**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_cameracontrol_focal_length_s)および ksproperty のメンバーです[ **\_CAMERACONTROL\_ノード\_、\_の長さ\_S**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_cameracontrol_node_focal_length_s)構造体を中心にしています。)

たとえば、 **lObjectiveFocalLengthMax** = 105 および**lOcularFocalLength** = 35 の場合、このカメラは、最大光学ズーム比105/35 または3に対応しています。

USB Video Class Device Class specification の「*光学ズーム*」セクションも参照してください。 この仕様は、 [USB 実装者フォーラム](https://go.microsoft.com/fwlink/p/?linkid=8780)の web サイトで入手できます。

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


[**KSK プロパティ\_CAMERACONTROL\_焦点\_の長さ\_S**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_cameracontrol_focal_length_s)

[**KSPROPERTY\_CAMERACONTROL\_NODE\_の\_の長さ\_秒**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_cameracontrol_node_focal_length_s)

[**KSK プロパティ\_CAMERACONTROL\_ZOOM**](ksproperty-cameracontrol-zoom.md)

[**KSK プロパティ\_CAMERACONTROL\_ZOOM\_相対**](ksproperty-cameracontrol-zoom-relative.md)

 

 







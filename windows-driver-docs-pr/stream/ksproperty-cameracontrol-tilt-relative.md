---
title: KSPROPERTY\_CAMERACONTROL\_傾き\_相対
description: KSK プロパティ\_CAMERACONTROL\_傾き\_相対プロパティは、カメラの垂直方向の傾ける状態を指定します。
ms.assetid: 82702eec-38dc-44a1-bf57-56c9f04bb2d0
keywords:
- KSPROPERTY_CAMERACONTROL_TILT_RELATIVE ストリーミングメディアデバイス
topic_type:
- apiref
api_name:
- KSPROPERTY_CAMERACONTROL_TILT_RELATIVE
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: fd8909c8ddb385755857b534f499361326bd9113
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842480"
---
# <a name="ksproperty_cameracontrol_tilt_relative"></a>KSPROPERTY\_CAMERACONTROL\_傾き\_相対


KSK プロパティ\_CAMERACONTROL\_傾き\_相対プロパティは、カメラの垂直方向の傾ける状態を指定します。

## <span id="ddk_ksproperty_cameracontrol_tilt_relative_ks"></span><span id="DDK_KSPROPERTY_CAMERACONTROL_TILT_RELATIVE_KS"></span>


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
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_cameracontrol_s" data-raw-source="[&lt;strong&gt;KSPROPERTY_CAMERACONTROL_S&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_cameracontrol_s)"><strong>KSPROPERTY_CAMERACONTROL_S</strong></a>または<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_cameracontrol_node_s" data-raw-source="[&lt;strong&gt;KSPROPERTY_CAMERACONTROL_NODE_S&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_cameracontrol_node_s)"> <strong>KSPROPERTY_CAMERACONTROL_NODE_S</strong></a></p></td>
<td><p>長い</p></td>
</tr>
</tbody>
</table>

 

プロパティ値 (操作データ) は、カメラの相対傾き設定を指定する LONG です。 値のサイズは、必要な傾き速度を表します。値が大きいほど、より高速になります。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>Value</th>
<th>説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>0</p></td>
<td><p>傾けるを停止します。</p></td>
</tr>
<tr class="even">
<td><p>正の値</p></td>
<td><p>傾けるを起動します。</p></td>
</tr>
<tr class="odd">
<td><p>負の値</p></td>
<td><p>傾けるを開始します。</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>注釈
-------

[**Ksk プロパティ\_CAMERACONTROL\_NODE\_S**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_cameracontrol_node_s)構造体の**値**メンバーは、相対傾きを指定します。

特定のデバイスでは特定の速度範囲のみがサポートされる場合があることに注意してください。 デバイスでサポートされる速度の範囲を決定するために、アプリケーションは\_BASICSUPPORT 要求の種類\_KSK プロパティを発行できます。 Ksk プロパティ[ **\_ITEM**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksproperty_item)構造体の**Flags**メンバーで、\_BASICSUPPORT という種類の\_を指定できます。

一部のデバイスでは、1つの傾き速度しかサポートしていません。 この場合、**値**メンバーの符号は、傾ける方向を示します。

クライアントは、set 要求を行うときに、前の表の値のいずれかを\_CAMERACONTROL\_NODE\_S 構造体の KSK プロパティの**値**のメンバーに指定する必要があります。

Get 要求を行うと、クライアントは、前の表の値のいずれかを、\_CAMERACONTROL\_NODE\_S 構造体の KSK プロパティの**値**メンバーで受け取ります。 値は、カメラの現在の傾きの状態を示します。

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


[**KSPROPERTY\_CAMERACONTROL\_NODE\_S**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_cameracontrol_node_s)

 

 







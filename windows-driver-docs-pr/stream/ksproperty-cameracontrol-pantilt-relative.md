---
title: KSK プロパティ\_CAMERACONTROL\_PANTILT\_相対
description: KSK プロパティ\_CAMERACONTROL\_PANTILT\_相対プロパティは、カメラの水平方向または垂直方向の回転を指定し、両方を同時に指定できます。
ms.assetid: c2c9405c-7713-439f-a150-51969a2a5e6b
keywords:
- KSPROPERTY_CAMERACONTROL_PANTILT_RELATIVE ストリーミングメディアデバイス
topic_type:
- apiref
api_name:
- KSPROPERTY_CAMERACONTROL_PANTILT_RELATIVE
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 227c13b5ad520bcd839843748076b0ea5cc45c72
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843343"
---
# <a name="ksproperty_cameracontrol_pantilt_relative"></a>KSK プロパティ\_CAMERACONTROL\_PANTILT\_相対


KSK プロパティ\_CAMERACONTROL\_PANTILT\_相対プロパティは、カメラの水平方向または垂直方向の回転を指定し、両方を同時に指定できます。

## <span id="ddk_ksproperty_cameracontrol_pantilt_relative_ks"></span><span id="DDK_KSPROPERTY_CAMERACONTROL_PANTILT_RELATIVE_KS"></span>


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
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_cameracontrol_node_s2" data-raw-source="[&lt;strong&gt;KSPROPERTY_CAMERACONTROL_NODE_S2&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_cameracontrol_node_s2)"><strong>KSPROPERTY_CAMERACONTROL_NODE_S2</strong></a>または<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_cameracontrol_s2" data-raw-source="[&lt;strong&gt;KSPROPERTY_CAMERACONTROL_S2&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_cameracontrol_s2)"><strong>KSPROPERTY_CAMERACONTROL_S2</strong></a>は、要求がフィルターとノードのどちらであるかによって異なります。</p></td>
<td><p>長整数のペア</p></td>
</tr>
</tbody>
</table>

 

プロパティ値 (操作データ) は、カメラの相対パンと傾きの設定を指定する長整数のペアです。 値のサイズは、必要なパン速度を表します。値が大きいほど、より高速になります。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>Value1</th>
<th>説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>0</p></td>
<td><p>カメラの水平モーションを停止します。</p></td>
</tr>
<tr class="even">
<td><p>正の値</p></td>
<td><p>右へのパンを開始します。</p></td>
</tr>
<tr class="odd">
<td><p>負の値</p></td>
<td><p>左へのパンを開始します。</p></td>
</tr>
</tbody>
</table>

 

値のサイズは、必要な傾き速度を表します。値が大きいほど、より高速になります。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>Value2</th>
<th>説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>0</p></td>
<td><p>カメラの垂直方向の動きを停止します。</p></td>
</tr>
<tr class="even">
<td><p>正の値</p></td>
<td><p>カメラの回転を開始します。</p></td>
</tr>
<tr class="odd">
<td><p>負の値</p></td>
<td><p>カメラの回転を開始します。</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>注釈
-------

設定要求を作成してカメラをパンする場合、クライアントは、プロパティ記述子構造の**Value1**メンバーで、前の表のいずれかの値を指定する必要があります。

同様に、セット要求を作成してカメラを傾けると、クライアントは、プロパティ記述子構造の**Value2**メンバーの前のテーブルの値のいずれかを指定します。

Get 要求を行うと、クライアントは、 **Value1**\_プロパティの**VALUE2**メンバーの CAMERACONTROL\_S2 または ksk プロパティ\_CAMERACONTROL\_ノード\_s2 のパン値を受け取ります。データ. 値は、カメラの現在のパンまたは傾きの状態を示します。

特定のデバイスでは特定の速度範囲のみがサポートされる場合があることに注意してください。 デバイスでサポートされる速度の範囲を決定するために、アプリケーションは\_BASICSUPPORT 要求の種類\_KSK プロパティを発行できます。 Ksk プロパティ[ **\_ITEM**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksproperty_item)構造体の**Flags**メンバーで、\_BASICSUPPORT という種類の\_を指定できます。

一部のデバイスは、1つのパンまたはチルト速度のみをサポートしています。 この場合、 **Value1**または**Value2**メンバーの符号は、パンする方向を示します。

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

 

 







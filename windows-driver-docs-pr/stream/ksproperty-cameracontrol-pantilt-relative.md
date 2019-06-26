---
title: KSPROPERTY\_CAMERACONTROL\_PANTILT\_相対
description: KSPROPERTY\_CAMERACONTROL\_PANTILT\_相対プロパティは、カメラの水平方向または垂直方向の回転を指定し、両方同時に指定できます。
ms.assetid: c2c9405c-7713-439f-a150-51969a2a5e6b
keywords:
- KSPROPERTY_CAMERACONTROL_PANTILT_RELATIVE ストリーミング メディア デバイス
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
ms.openlocfilehash: 0c857001f3be6d5c2c6279990403784765e3f944
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67353211"
---
# <a name="kspropertycameracontrolpantiltrelative"></a>KSPROPERTY\_CAMERACONTROL\_PANTILT\_相対


KSPROPERTY\_CAMERACONTROL\_PANTILT\_相対プロパティは、カメラの水平方向または垂直方向の回転を指定し、両方同時に指定できます。

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
<td><p>〇</p></td>
<td><p>フィルターまたはノード</p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-ksproperty_cameracontrol_node_s2" data-raw-source="[&lt;strong&gt;KSPROPERTY_CAMERACONTROL_NODE_S2&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-ksproperty_cameracontrol_node_s2)"><strong>KSPROPERTY_CAMERACONTROL_NODE_S2</strong> </a>または<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-ksproperty_cameracontrol_s2" data-raw-source="[&lt;strong&gt;KSPROPERTY_CAMERACONTROL_S2&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-ksproperty_cameracontrol_s2)"> <strong>KSPROPERTY_CAMERACONTROL_S2</strong> </a>要求をフィルターまたはノードがあるかによって</p></td>
<td><p>長整数のペア</p></td>
</tr>
</tbody>
</table>

 

プロパティの値 (データの操作) は、カメラの相対的な pan を指定する設定を傾ける長整数のペアです。 値のサイズは、必要なパンの速度; を表します。高い値は、高速を表します。

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
<td><p>カメラの水平方向の動きを停止します。</p></td>
</tr>
<tr class="even">
<td><p>正の値</p></td>
<td><p>右にパンを開始します。</p></td>
</tr>
<tr class="odd">
<td><p>負の値</p></td>
<td><p>左にパンを開始します。</p></td>
</tr>
</tbody>
</table>

 

値のサイズは、目的の傾き速度を表します。高い値は、高速を表します。

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
<td><p>下のカメラの回転を開始します。</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>注釈
-------

クライアントがで上記の表に、値のいずれかを指定する必要がありますカメラへパンするセットの要求を行うときに**Value1**プロパティ記述子構造体のメンバー。

同様に、傾きのカメラにセットの要求を行うときに、クライアントが指定の前のテーブル内の値のいずれかの**Value2**プロパティ記述子構造体のメンバー。

クライアントでのパン値を受け取る get 要求を行うときに、 **Value1**メンバーおよび傾きの値で、 **Value2** 、KSPROPERTY のメンバー\_CAMERACONTROL\_S2 またはKSPROPERTY\_CAMERACONTROL\_ノード\_S2 構造体。 値を現在のパンを示すか傾きのカメラの状態。

特定のデバイスが一定の速度の範囲だけをサポート可能性がありますに注意してください。 アプリケーションの速度、デバイスでサポートされている範囲を決定する、KSPROPERTY を発行できます\_型\_BASICSUPPORT 要求。 KSPROPERTY を指定する\_型\_で BASICSUPPORT、**フラグ**のメンバー、 [ **KSPROPERTY\_項目**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksproperty_item)構造体。

一部のデバイスでは、パンが 1 つのみをサポートするか、傾きの速度。 ここでの符号、 **Value1**または**Value2**メンバーをパンする方向を示します。

<a name="requirements"></a>必要条件
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>バージョン</p></td>
<td><p>Windows Vista および Windows オペレーティング システムの以降のバージョンで使用できます。</p></td>
</tr>
<tr class="even">
<td><p>Header</p></td>
<td>Ksmedia.h (Ksmedia.h を含む)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[**KSPROPERTY\_CAMERACONTROL\_S2**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-ksproperty_cameracontrol_s2)

[**KSPROPERTY\_CAMERACONTROL\_ノード\_S2**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-ksproperty_cameracontrol_node_s2)

 

 







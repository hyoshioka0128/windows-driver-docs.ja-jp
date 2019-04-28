---
title: KSPROPERTY\_CAMERACONTROL\_パン\_相対
description: KSPROPERTY\_CAMERACONTROL\_パン\_相対プロパティが垂直の軸を中心にカメラの回転を指定します。
ms.assetid: 11b6ac3e-e65e-4a85-bfcc-f45e8e96c8fb
keywords:
- KSPROPERTY_CAMERACONTROL_PAN_RELATIVE ストリーミング メディア デバイス
topic_type:
- apiref
api_name:
- KSPROPERTY_CAMERACONTROL_PAN_RELATIVE
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: a114d62d61926242fca5152e9ae705f629c14b1c
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63363158"
---
# <a name="kspropertycameracontrolpanrelative"></a>KSPROPERTY\_CAMERACONTROL\_パン\_相対


KSPROPERTY\_CAMERACONTROL\_パン\_相対プロパティが垂直の軸を中心にカメラの回転を指定します。

## <span id="ddk_ksproperty_cameracontrol_pan_relative_ks"></span><span id="DDK_KSPROPERTY_CAMERACONTROL_PAN_RELATIVE_KS"></span>


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
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff564439" data-raw-source="[&lt;strong&gt;KSPROPERTY_CAMERACONTROL_S&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff564439)"><strong>KSPROPERTY_CAMERACONTROL_S</strong> </a>または<a href="https://msdn.microsoft.com/library/windows/hardware/ff564420" data-raw-source="[&lt;strong&gt;KSPROPERTY_CAMERACONTROL_NODE_S&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff564420)"> <strong>KSPROPERTY_CAMERACONTROL_NODE_S</strong></a></p></td>
<td><p>LONG</p></td>
</tr>
</tbody>
</table>

 

プロパティの値 (データの操作) は、カメラの相対的なパンの設定を指定する LONG が。 値のサイズは、必要なパンの速度; を表します。高い値は、高速を表します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>値</th>
<th>説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>0</p></td>
<td><p>パンを停止します。</p></td>
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

 

<a name="remarks"></a>注釈
-------

**値**のメンバー、 [ **KSPROPERTY\_CAMERACONTROL\_ノード\_S** ](https://msdn.microsoft.com/library/windows/hardware/ff564420)構造が相対的な pan を指定します。

特定のデバイスが一定の速度の範囲だけをサポート可能性がありますに注意してください。 アプリケーションの速度、デバイスでサポートされている範囲を決定する、KSPROPERTY を発行できます\_型\_BASICSUPPORT 要求。 KSPROPERTY を指定する\_型\_で BASICSUPPORT、**フラグ**のメンバー、 [ **KSPROPERTY\_項目**](https://msdn.microsoft.com/library/windows/hardware/ff565176)構造体。

一部のデバイスでは、1 つのパンの速度のみをサポートします。 ここでの符号、**値**メンバーをパンする方向を示します。

クライアントがで上記の表に、値のいずれかを指定する必要がありますセット要求を行うときに、**値**、KSPROPERTY のメンバー\_CAMERACONTROL\_ノード\_S 構造体。

Get 要求を行うときに、クライアントは受信値のいずれかで上記の表に、**値**、KSPROPERTY のメンバー\_CAMERACONTROL\_ノード\_S 構造体。 値は、カメラの現在のパンの状態を示します。

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


[**KSPROPERTY\_CAMERACONTROL\_ノード\_S**](https://msdn.microsoft.com/library/windows/hardware/ff564420)

 

 







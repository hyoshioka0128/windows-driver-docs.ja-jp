---
title: KSPROPERTY\_CAMERACONTROL\_ロール\_相対
description: KSPROPERTY\_CAMERACONTROL\_ロール\_相対プロパティが軸を表示するイメージの周囲のカメラの回転を指定します。
ms.assetid: cd16369b-558c-48b6-9a0a-ffd4e4561a30
keywords:
- KSPROPERTY_CAMERACONTROL_ROLL_RELATIVE ストリーミング メディア デバイス
topic_type:
- apiref
api_name:
- KSPROPERTY_CAMERACONTROL_ROLL_RELATIVE
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: c053a8e7f10e725f30add5f03b8758f09092dcad
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67373192"
---
# <a name="kspropertycameracontrolrollrelative"></a>KSPROPERTY\_CAMERACONTROL\_ロール\_相対


KSPROPERTY\_CAMERACONTROL\_ロール\_相対プロパティが軸を表示するイメージの周囲のカメラの回転を指定します。

## <span id="ddk_ksproperty_cameracontrol_roll_relative_ks"></span><span id="DDK_KSPROPERTY_CAMERACONTROL_ROLL_RELATIVE_KS"></span>


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
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-ksproperty_cameracontrol_s" data-raw-source="[&lt;strong&gt;KSPROPERTY_CAMERACONTROL_S&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-ksproperty_cameracontrol_s)"><strong>KSPROPERTY_CAMERACONTROL_S</strong> </a>または<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-ksproperty_cameracontrol_node_s" data-raw-source="[&lt;strong&gt;KSPROPERTY_CAMERACONTROL_NODE_S&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-ksproperty_cameracontrol_node_s)"> <strong>KSPROPERTY_CAMERACONTROL_NODE_S</strong></a></p></td>
<td><p>LONG</p></td>
</tr>
</tbody>
</table>

 

プロパティの値 (データの操作) は、カメラの相対的なロールの設定を指定する LONG が。 値のサイズは、必要な回転速度を表します。高い値は、高速を表します。

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
<td><p>ロールを停止します。</p></td>
</tr>
<tr class="even">
<td><p>正の値</p></td>
<td><p>表示軸を中心に時計回りに回転を開始します。</p></td>
</tr>
<tr class="odd">
<td><p>負の値</p></td>
<td><p>表示する軸を中心に反時計回りに回転を開始します。</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>注釈
-------

**値**のメンバー、 [ **KSPROPERTY\_CAMERACONTROL\_ノード\_S** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-ksproperty_cameracontrol_node_s)構造が相対のロールを指定します。

特定のデバイスが一定の速度の範囲だけをサポート可能性がありますに注意してください。 アプリケーションの速度、デバイスでサポートされている範囲を決定する、KSPROPERTY を発行できます\_型\_BASICSUPPORT 要求。 KSPROPERTY を指定する\_型\_で BASICSUPPORT、**フラグ**のメンバー、 [ **KSPROPERTY\_項目**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksproperty_item)構造体。

一部のデバイスでは、1 つの回転速度のみをサポートします。 ここでの符号、**値**メンバーは、回転の方向を示します。

クライアントがで上記の表に、値のいずれかを指定する必要がありますセット要求を行うときに、**値**、KSPROPERTY のメンバー\_CAMERACONTROL\_ノード\_S 構造体。

Get 要求を行うときに、クライアントは受信値のいずれかで上記の表に、**値**、KSPROPERTY のメンバー\_CAMERACONTROL\_ノード\_S 構造体。 値は、カメラの現在の回転の状態を示します。

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


[**KSPROPERTY\_CAMERACONTROL\_ノード\_S**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-ksproperty_cameracontrol_node_s)

 

 







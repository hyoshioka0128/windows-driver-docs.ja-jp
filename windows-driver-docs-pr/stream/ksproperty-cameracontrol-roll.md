---
title: KSK プロパティ\_CAMERACONTROL\_ROLL
description: ユーザーモードのクライアントは、KSK プロパティ\_CAMERACONTROL\_ROLL プロパティを使用して、カメラのロール設定を取得または設定します。 このプロパティは省略可能です。
ms.assetid: 58b09e8d-7c0c-4e32-b124-5722bd09f011
keywords:
- KSPROPERTY_CAMERACONTROL_ROLL ストリーミングメディアデバイス
topic_type:
- apiref
api_name:
- KSPROPERTY_CAMERACONTROL_ROLL
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: ea4343a3df475a1884b42e40293ba5a6d4a0ab62
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72826914"
---
# <a name="ksproperty_cameracontrol_roll"></a>KSK プロパティ\_CAMERACONTROL\_ROLL


ユーザーモードのクライアントは、KSK プロパティ\_CAMERACONTROL\_ROLL プロパティを使用して、カメラのロール設定を取得または設定します。 このプロパティは省略可能です。

## <span id="ddk_ksproperty_cameracontrol_roll_ks"></span><span id="DDK_KSPROPERTY_CAMERACONTROL_ROLL_KS"></span>


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

 

プロパティ値 (操作データ) は、カメラのロール設定を指定する LONG です。 この値は度数で表されます。

正の値を指定すると、画像を表示する軸に沿ってカメラが時計回りに回転します。 負の値を指定すると、次の図に示すように、カメラが反時計回りに回転します。

![カメラのロール値を示す図](images/cam-roll-1.png)

このプロパティをサポートするすべてのビデオキャプチャミニドライバーで、このプロパティの範囲と既定値を定義する必要があります。 デバイスの範囲は-180 ~ + 180 で、既定値は0にする必要があります。

<a name="remarks"></a>注釈
-------

CAMERACONTROL\_S 構造体\_KSK プロパティの**値**メンバーは、ロール設定を指定します。

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

[**KSK プロパティ\_CAMERACONTROL\_S**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_cameracontrol_s)

 

 







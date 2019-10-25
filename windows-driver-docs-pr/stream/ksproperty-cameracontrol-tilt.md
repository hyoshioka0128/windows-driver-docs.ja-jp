---
title: KSK プロパティ\_CAMERACONTROL\_チルト
description: ユーザーモードのクライアントは、KSK プロパティ\_CAMERACONTROL\_傾きプロパティを使用して、カメラの傾き設定を取得または設定します。 このプロパティは省略可能です。
ms.assetid: 265315ce-6f35-4f5a-907f-b5595e7fb5af
keywords:
- KSPROPERTY_CAMERACONTROL_TILT ストリーミングメディアデバイス
topic_type:
- apiref
api_name:
- KSPROPERTY_CAMERACONTROL_TILT
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: a4e66166604023b658300d4c4f4b0d72b09a0c41
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842486"
---
# <a name="ksproperty_cameracontrol_tilt"></a>KSK プロパティ\_CAMERACONTROL\_チルト


ユーザーモードのクライアントは、KSK プロパティ\_CAMERACONTROL\_傾きプロパティを使用して、カメラの傾き設定を取得または設定します。 このプロパティは省略可能です。

## <span id="ddk_ksproperty_cameracontrol_tilt_ks"></span><span id="DDK_KSPROPERTY_CAMERACONTROL_TILT_KS"></span>


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

 

プロパティ値 (操作データ) は、カメラの傾き設定を指定する LONG です。 この値は度数で表されます。

正の値は、イメージの平面を上にポイントします。 負の値は、次の図に示すように、画像平面を下方向に指します。

![カメラの傾きの値を示す図](images/cam-tilt-1.png)

このプロパティをサポートするすべてのビデオキャプチャミニドライバーで、このプロパティの範囲と既定値を定義する必要があります。 デバイスの範囲は-180 ~ + 180 である必要があります。 既定値は0である必要があります。

**注意**  アプリの作成時またはテスト時には、実際には、一部のドライバーで、傾きの値のカスタム範囲と、通常の単位に基づいていないカスタムのステップ値が定義されていることに注意してください。 ドライバーは、物理的またはデジタル的にチルトコントロールを実装する場合があります。

 

<a name="remarks"></a>注釈
-------

CAMERACONTROL\_S 構造体\_KSK プロパティの**値**メンバーは、傾きの設定を指定します。

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

 

 







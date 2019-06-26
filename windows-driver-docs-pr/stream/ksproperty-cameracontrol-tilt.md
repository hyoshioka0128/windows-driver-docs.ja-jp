---
title: KSPROPERTY\_CAMERACONTROL\_傾き
description: ユーザー モードのクライアントの使用、KSPROPERTY\_CAMERACONTROL\_傾きプロパティを取得またはカメラの傾きの設定を設定します。 このプロパティは省略可能です。
ms.assetid: 265315ce-6f35-4f5a-907f-b5595e7fb5af
keywords:
- KSPROPERTY_CAMERACONTROL_TILT ストリーミング メディア デバイス
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
ms.openlocfilehash: ed0d05ecaf76b5661db7cfc661dfc6e257b91d2e
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67373186"
---
# <a name="kspropertycameracontroltilt"></a>KSPROPERTY\_CAMERACONTROL\_傾き


ユーザー モードのクライアントの使用、KSPROPERTY\_CAMERACONTROL\_傾きプロパティを取得またはカメラの傾きの設定を設定します。 このプロパティは省略可能です。

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

 

プロパティの値 (データの操作) は、カメラの傾きの設定を指定する LONG が。 この値は度数で表されます。

正の値は、画像の平面をポイントします。 負の値は、次の図に示すように、画像の平面をポイントします。

![図が表示されたカメラの傾きの値](images/cam-tilt-1.png)

このプロパティをサポートするすべてのビデオ キャプチャ ミニドライバーには、このプロパティの値を範囲と既定値を定義する必要があります。 デバイスの範囲には、-180 +180 経由する必要があります。 既定値は 0 である必要があります。

**注意**  書き込みや、アプリケーションのテスト、ときに注意する必要が実際には、一部のドライバーが定義傾きの値と標準的な単位に基づかないがカスタム ステップ値のカスタムの範囲。 ドライバーは、物理的にまたはデジタルの傾きのコントロールを実装できます。

 

<a name="remarks"></a>注釈
-------

**値**、KSPROPERTY のメンバー\_CAMERACONTROL\_S 構造体の傾きの設定を指定します。

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
<td>Ksmedia.h (Ksmedia.h を含む)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[**KSPROPERTY**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksidentifier)

[**KSPROPERTY\_CAMERACONTROL\_S**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-ksproperty_cameracontrol_s)

 

 







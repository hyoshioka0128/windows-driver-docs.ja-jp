---
title: KSPROPERTY\_CAMERACONTROL\_方向へパンします。
description: ユーザー モードのクライアントの使用、KSPROPERTY\_CAMERACONTROL\_パン プロパティを取得またはカメラのパンの設定を設定します。 このプロパティは省略可能です。
ms.assetid: 765eecbf-ecde-4268-9ab5-c0c099c06d2f
keywords:
- KSPROPERTY_CAMERACONTROL_PAN ストリーミング メディア デバイス
topic_type:
- apiref
api_name:
- KSPROPERTY_CAMERACONTROL_PAN
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: ad2c911c08d940eae2bcf004ba2f44d9c93f9a3c
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67353245"
---
# <a name="kspropertycameracontrolpan"></a>KSPROPERTY\_CAMERACONTROL\_方向へパンします。


ユーザー モードのクライアントの使用、KSPROPERTY\_CAMERACONTROL\_パン プロパティを取得またはカメラのパンの設定を設定します。 このプロパティは省略可能です。

## <span id="ddk_ksproperty_cameracontrol_pan_ks"></span><span id="DDK_KSPROPERTY_CAMERACONTROL_PAN_KS"></span>


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

 

プロパティの値 (データの操作) は、カメラのパンの設定を指定する LONG が。 この値は度数で表されます。

正の値は、カメラが時計回りに回転することを示します。 負の値は、カメラは、次の図に示すように、反時計回りに回転を示します。

![図が表示されたカメラのパンの値](images/cam-pan-1.png)

このプロパティをサポートするすべてのビデオ キャプチャ ミニドライバーには、このプロパティの値を範囲と既定値を定義する必要があります。 デバイスの範囲は、-180 +180 経由である必要があります。 既定値は 0 である必要があります。

**注意**  記述またはアプリをテストする場合を実際には、ドライバーによって、カスタムの範囲を定義パンの値と標準的な単位に基づかないがカスタム ステップ値に注意してくださかった。 ドライバーは、物理的にまたはデジタル署名、パン コントロールを実装できます。

 

<a name="remarks"></a>注釈
-------

**値**、KSPROPERTY のメンバー\_CAMERACONTROL\_の構造をパン設定を指定します。

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

 

 







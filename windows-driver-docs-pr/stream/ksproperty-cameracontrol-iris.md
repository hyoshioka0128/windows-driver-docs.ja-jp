---
title: KSPROPERTY\_CAMERACONTROL\_IRIS
description: ユーザー モードのクライアントの使用、KSPROPERTY\_CAMERACONTROL\_IRIS プロパティを取得またはカメラの絞り設定を設定します。 このプロパティは省略可能です。
ms.assetid: 000fc146-f6bb-490b-93b6-ebf5ad83b92f
keywords:
- KSPROPERTY_CAMERACONTROL_IRIS ストリーミング メディア デバイス
topic_type:
- apiref
api_name:
- KSPROPERTY_CAMERACONTROL_IRIS
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0b30944b5357e1bf1320d67d0ea241a920666ad3
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67385386"
---
# <a name="kspropertycameracontroliris"></a>KSPROPERTY\_CAMERACONTROL\_IRIS


ユーザー モードのクライアントの使用、KSPROPERTY\_CAMERACONTROL\_IRIS プロパティを取得またはカメラの絞り設定を設定します。 このプロパティは省略可能です。

## <span id="ddk_ksproperty_cameracontrol_iris_ks"></span><span id="DDK_KSPROPERTY_CAMERACONTROL_IRIS_KS"></span>


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

 

プロパティの値 (データの操作) は、カメラの絞り設定を指定する LONG が。 この値が fstop 単位で表された\*10。

<a name="remarks"></a>注釈
-------

**値**、KSPROPERTY のメンバー\_CAMERACONTROL\_構造がカメラの絞り設定を指定します。

このプロパティをサポートするすべてのビデオ キャプチャ ミニドライバーは、このプロパティの独自の範囲と既定値を定義する必要があります。

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

 

 







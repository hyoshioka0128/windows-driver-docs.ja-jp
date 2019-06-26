---
title: KSPROPERTY\_ビデオ プロシージャ アンプ\_ホワイト バランス\_コンポーネント
description: KSPROPERTY\_ビデオ プロシージャ アンプ\_ホワイト バランス\_コンポーネントのプロパティは、ホワイト バランス設定をビデオ形式の青と赤の値を指定します。
ms.assetid: ed5faffa-7e31-47ac-bf11-2201d616c6aa
keywords:
- KSPROPERTY_VIDEOPROCAMP_WHITEBALANCE_COMPONENT ストリーミング メディア デバイス
topic_type:
- apiref
api_name:
- KSPROPERTY_VIDEOPROCAMP_WHITEBALANCE_COMPONENT
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8d9f49b85d314e5cd1886cb100f0d56aeea8882f
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67381907"
---
# <a name="kspropertyvideoprocampwhitebalancecomponent"></a>KSPROPERTY\_ビデオ プロシージャ アンプ\_ホワイト バランス\_コンポーネント


KSPROPERTY\_ビデオ プロシージャ アンプ\_ホワイト バランス\_コンポーネントのプロパティは、ホワイト バランス設定をビデオ形式の青と赤の値を指定します。

## <span id="ddk_ksproperty_videoprocamp_whitebalance_component_ks"></span><span id="DDK_KSPROPERTY_VIDEOPROCAMP_WHITEBALANCE_COMPONENT_KS"></span>


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
<td><p>node</p></td>
<td><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-ksproperty_videoprocamp_node_s2" data-raw-source="[&lt;strong&gt;KSPROPERTY_VIDEOPROCAMP_NODE_S2&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-ksproperty_videoprocamp_node_s2)"><strong>KSPROPERTY_VIDEOPROCAMP_NODE_S2</strong></a></td>
<td><p>長整数のペア</p></td>
</tr>
</tbody>
</table>

 

プロパティの値 (データの操作) は、カメラのホワイト バランス設定の赤、青のコンポーネントを指定する LONG 整数のペアです。 値は、カメラの現在の赤、青のコンポーネントの値を示します。

<a name="remarks"></a>注釈
-------

サポートされている範囲とホワイト バランス コンポーネントの既定値は、実装に依存が。

クライアントの赤要素値を指定する必要がありますセット要求を行うときに、 **Value1**メンバーと青要素値、 **Value2** 、KSPROPERTY のメンバー\_ビデオ プロシージャ アンプ\_ノード\_S2 構造体。

デバイスでサポートされているホワイト バランス値の範囲を確認するのには、アプリケーションが、KSPROPERTY を発行できます\_型\_BASICSUPPORT 要求。 KSPROPERTY を指定する\_型\_で BASICSUPPORT、**フラグ**のメンバー、 [ **KSPROPERTY\_項目**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksproperty_item)構造体。

クライアントで赤の値を受け取る get 要求を行うときに、 **Value1**メンバーと青要素値、 **Value2** 、KSPROPERTY のメンバー\_ビデオ プロシージャ アンプ\_ノード\_S2 構造体。

<a name="requirements"></a>必要条件
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

[**KSPROPERTY\_ビデオ プロシージャ アンプ\_ノード\_S2**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-ksproperty_videoprocamp_node_s2)

 

 







---
title: KSPROPERTY\_VIDEOPROCAMP\_ホワイトバランス\_コンポーネント
description: VIDEOPROCAMP\_ホワイトバランス\_コンポーネントのプロパティ\_は、ホワイトバランスの設定を青と赤の値で指定します。
ms.assetid: ed5faffa-7e31-47ac-bf11-2201d616c6aa
keywords:
- KSPROPERTY_VIDEOPROCAMP_WHITEBALANCE_COMPONENT ストリーミングメディアデバイス
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
ms.openlocfilehash: c8d911dfa6aca6b42c1163bb65f0eba3cbcf94b0
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842820"
---
# <a name="ksproperty_videoprocamp_whitebalance_component"></a>KSPROPERTY\_VIDEOPROCAMP\_ホワイトバランス\_コンポーネント


VIDEOPROCAMP\_ホワイトバランス\_コンポーネントのプロパティ\_は、ホワイトバランスの設定を青と赤の値で指定します。

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
<td><p>ノード</p></td>
<td><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_videoprocamp_node_s2" data-raw-source="[&lt;strong&gt;KSPROPERTY_VIDEOPROCAMP_NODE_S2&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_videoprocamp_node_s2)"><strong>KSPROPERTY_VIDEOPROCAMP_NODE_S2</strong></a></td>
<td><p>長整数のペア</p></td>
</tr>
</tbody>
</table>

 

プロパティ値 (操作データ) は、カメラの白いバランス設定の赤と青のコンポーネントを指定する長整数のペアです。 値は、カメラの現在の赤と青のコンポーネントの値を示します。

<a name="remarks"></a>注釈
-------

ホワイトバランスコンポーネントでサポートされる範囲と既定値は、実装に依存します。

クライアントは、set 要求を行うときに、 **VALUE1**プロパティ\_VIDEOPROCAMP\_NODE\_S2 構造体の**Value2**メンバーの中で、赤色のコンポーネント値を指定する必要があります。

デバイスでサポートされている白のバランス値の範囲を決定するために、アプリケーションは\_BASICSUPPORT 要求\_種類の KSK プロパティを発行できます。 Ksk プロパティ[ **\_ITEM**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksproperty_item)構造体の**Flags**メンバーで、\_BASICSUPPORT という種類の\_を指定できます。

Get 要求を行うと、クライアントは**Value1**メンバーの赤の値を受け取り、ksproperty\_VIDEOPROCAMP\_NODE\_S2 構造体の**Value2**メンバーの青のコンポーネントの値を受け取ります。

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

[**KSPROPERTY\_VIDEOPROCAMP\_NODE\_S2**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_videoprocamp_node_s2)

 

 







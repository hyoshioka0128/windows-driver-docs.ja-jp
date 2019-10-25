---
title: KSK プロパティ\_BDA\_ノード\_イベント
description: クライアントは、KSK プロパティ\_BDA\_NODE\_イベントを使用して、ノードでサポートされているイベントの一覧を取得します。
ms.assetid: 4923a88b-abb3-4608-95b3-b0e74eeadaa8
keywords:
- KSPROPERTY_BDA_NODE_EVENTS ストリーミングメディアデバイス
topic_type:
- apiref
api_name:
- KSPROPERTY_BDA_NODE_EVENTS
api_location:
- Bdamedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: c704c4253ef1b5f979a418548dabbfa936b1639c
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72833687"
---
# <a name="ksproperty_bda_node_events"></a>KSK プロパティ\_BDA\_ノード\_イベント


クライアントは、KSK プロパティ\_BDA\_NODE\_イベントを使用して、ノードでサポートされているイベントの一覧を取得します。

## <span id="ddk_ksproperty_bda_node_events_ks"></span><span id="DDK_KSPROPERTY_BDA_NODE_EVENTS_KS"></span>


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
<th>セット</th>
<th>的を絞る</th>
<th>プロパティ記述子の型</th>
<th>プロパティ値の型</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>はい</p></td>
<td><p>いいえ</p></td>
<td><p>filter</p></td>
<td><p>KSPROPERTY</p></td>
<td><p>Guid の一覧</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>解説
-------

ノードでサポートされるイベントの一覧は、Guid の一覧です。

ネットワークプロバイダーは、このプロパティを使用して、BDA テンプレート接続リスト内の各ノードの機能を照会します。

<a name="requirements"></a>前提条件
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>ヘッダー</p></td>
<td>Bdamedia (Bdamedia を含む)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[**BdaPropertyNodeEvents**](https://docs.microsoft.com/windows-hardware/drivers/ddi/bdasup/nf-bdasup-bdapropertynodeevents)

[**KSPROPERTY**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksidentifier)

 

 







---
title: KSPROPERTY\_BDA\_ノード\_イベント
description: クライアントを使用して、KSPROPERTY\_BDA\_ノード\_ノードでサポートされているイベントの一覧を取得するイベントです。
ms.assetid: 4923a88b-abb3-4608-95b3-b0e74eeadaa8
keywords:
- KSPROPERTY_BDA_NODE_EVENTS ストリーミング メディア デバイス
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
ms.openlocfilehash: 12624c84d7755ea80cdbebc9bbf1d58402511b18
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67386918"
---
# <a name="kspropertybdanodeevents"></a>KSPROPERTY\_BDA\_ノード\_イベント


クライアントを使用して、KSPROPERTY\_BDA\_ノード\_ノードでサポートされているイベントの一覧を取得するイベントです。

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
<th>設定</th>
<th>対象</th>
<th>プロパティ記述子の型</th>
<th>プロパティ値の型</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>〇</p></td>
<td><p>X</p></td>
<td><p>フィルター</p></td>
<td><p>KSPROPERTY</p></td>
<td><p>Guid のリスト</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>注釈
-------

ノードによってサポートされているイベントの一覧は、Guid の一覧を示します。

ネットワーク プロバイダーでは、このプロパティを使用して、BDA テンプレートの接続リスト内の各ノードの機能のクエリを実行します。

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
<td>Bdamedia.h (Bdamedia.h を含む)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[**BdaPropertyNodeEvents**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/bdasup/nf-bdasup-bdapropertynodeevents)

[**KSPROPERTY**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksidentifier)

 

 







---
title: KSPROPERTY\_トポロジ\_接続
description: KSPROPERTY\_トポロジ\_接続プロパティは、KS フィルターのノード間のすべての接続を照会します。
ms.assetid: 8ea77244-14c1-4e27-9b96-e0f5a6c491e9
keywords:
- KSPROPERTY_TOPOLOGY_CONNECTIONS ストリーミング メディア デバイス
topic_type:
- apiref
api_name:
- KSPROPERTY_TOPOLOGY_CONNECTIONS
api_location:
- ks.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: e1b19b3141e0845e01547a1e66016aab7a382164
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67383997"
---
# <a name="kspropertytopologyconnections"></a>KSPROPERTY\_トポロジ\_接続


KSPROPERTY\_トポロジ\_接続プロパティは、KS フィルターのノード間のすべての接続を照会します。

## <span id="ddk_ksproperty_topology_connections_ks"></span><span id="DDK_KSPROPERTY_TOPOLOGY_CONNECTIONS_KS"></span>


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
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksidentifier" data-raw-source="[&lt;strong&gt;KSPROPERTY&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksidentifier)"><strong>KSPROPERTY</strong></a></p></td>
<td><p>A <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksmultiple_item" data-raw-source="[&lt;strong&gt;KSMULTIPLE_ITEM&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksmultiple_item)"> <strong>KSMULTIPLE_ITEM</strong> </a>のシーケンスに続く構造<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-kstopology_connection" data-raw-source="[&lt;strong&gt;KSTOPOLOGY_CONNECTION&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-kstopology_connection)"> <strong>KSTOPOLOGY_CONNECTION</strong> </a>構造体。</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>注釈
-------

KSMULTIPLE\_項目ヘッダーの後に、KSTOPOLOGY\_接続の構造は、KS フィルター内の 1 つのデータ パス接続について説明します。

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
<td>Ks.h (Ks.h を含む)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[**KSPROPERTY**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksidentifier)

[**KSMULTIPLE\_項目**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksmultiple_item)

[**KSTOPOLOGY\_接続**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-kstopology_connection)

 

 







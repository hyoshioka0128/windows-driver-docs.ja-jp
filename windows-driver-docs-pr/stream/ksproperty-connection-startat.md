---
title: KSPROPERTY\_接続\_STARTAT
description: KSPROPERTY\_接続\_STARTAT は指定されたイベントが発生した場合の起動をサポートするフィルターによって実装される省略可能なプロパティです。
ms.assetid: fcf76316-4016-4218-8530-5ef79794769a
keywords:
- KSPROPERTY_CONNECTION_STARTAT ストリーミング メディア デバイス
topic_type:
- apiref
api_name:
- KSPROPERTY_CONNECTION_STARTAT
api_location:
- ks.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0d20d6da973b5a5a49bd7f0e5bf7c24adee375c0
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56551808"
---
# <a name="kspropertyconnectionstartat"></a>KSPROPERTY\_接続\_STARTAT


KSPROPERTY\_接続\_STARTAT は指定されたイベントが発生した場合の起動をサポートするフィルターによって実装される省略可能なプロパティです。

## <span id="ddk_ksproperty_connection_startat_ks"></span><span id="DDK_KSPROPERTY_CONNECTION_STARTAT_KS"></span>


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
<td><p>X</p></td>
<td><p>〇</p></td>
<td><p>フィルター</p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksidentifier" data-raw-source="[&lt;strong&gt;KSPROPERTY&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksidentifier)"><strong>KSPROPERTY</strong></a></p></td>
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff566776" data-raw-source="[&lt;strong&gt;KSRELATIVEEVENT&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff566776)"><strong>KSRELATIVEEVENT</strong></a></p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>注釈
-------

このプロパティは、暗証番号 (pin) が、暗証番号 (pin) を実行状態に遷移するの一時停止状態のときにのみ要求する必要があります。

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
<td>Ks.h (Ks.h を含む)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[**KSRELATIVEEVENT**](https://msdn.microsoft.com/library/windows/hardware/ff566776)

[**KSEVENT\_項目**](https://msdn.microsoft.com/library/windows/hardware/ff561862)

 

 







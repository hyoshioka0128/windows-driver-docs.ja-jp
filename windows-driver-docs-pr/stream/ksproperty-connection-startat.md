---
title: KSK プロパティ\_接続\_STARTAT
description: KSK プロパティ\_接続\_STARTAT は、指定されたイベントが発生したときの開始をサポートするフィルターによって実装されるオプションのプロパティです。
ms.assetid: fcf76316-4016-4218-8530-5ef79794769a
keywords:
- KSPROPERTY_CONNECTION_STARTAT ストリーミングメディアデバイス
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
ms.openlocfilehash: 67d6752a4452298f3ff0ca3a81951c6d63e67954
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72826782"
---
# <a name="ksproperty_connection_startat"></a>KSK プロパティ\_接続\_STARTAT


KSK プロパティ\_接続\_STARTAT は、指定されたイベントが発生したときの開始をサポートするフィルターによって実装されるオプションのプロパティです。

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
<th>[購入]</th>
<th>設定</th>
<th>対象</th>
<th>プロパティ記述子の型</th>
<th>プロパティ値の型</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>必須ではない</p></td>
<td><p>[はい]</p></td>
<td><p>フィルター</p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksidentifier" data-raw-source="[&lt;strong&gt;KSPROPERTY&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksidentifier)"><strong>KSPROPERTY</strong></a></p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksrelativeevent" data-raw-source="[&lt;strong&gt;KSRELATIVEEVENT&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksrelativeevent)"><strong>KSRELATIVEEVENT</strong></a></p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>注釈
-------

Pin を実行状態に切り替えるには、pin が一時停止状態のときにのみ、このプロパティを要求する必要があります。

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
<td>Ks (Ks を含む)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[**KSRELATIVEEVENT**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksrelativeevent)

[**KSEVENT\_項目**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksevent_item)

 

 







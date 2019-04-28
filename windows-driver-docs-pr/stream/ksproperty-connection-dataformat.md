---
title: KSPROPERTY\_接続\_DATAFORMAT
description: クライアントの使用、KSPROPERTY\_接続\_DATAFORMAT プロパティを現在のデータ形式を設定します。
ms.assetid: c5f37f1b-7dc6-46d2-aba2-b6c03f07228d
keywords:
- KSPROPERTY_CONNECTION_DATAFORMAT ストリーミング メディア デバイス
topic_type:
- apiref
api_name:
- KSPROPERTY_CONNECTION_DATAFORMAT
api_location:
- ks.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0d8cb821104bce1395a55b8ade2404fcf51fed20
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63368691"
---
# <a name="kspropertyconnectiondataformat"></a>KSPROPERTY\_接続\_DATAFORMAT


クライアントの使用、KSPROPERTY\_接続\_DATAFORMAT プロパティを現在のデータ形式を設定します。

## <span id="ddk_ksproperty_connection_dataformat_ks"></span><span id="DDK_KSPROPERTY_CONNECTION_DATAFORMAT_KS"></span>


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
<td><p>Pin</p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksidentifier" data-raw-source="[&lt;strong&gt;KSPROPERTY&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksidentifier)"><strong>KSPROPERTY</strong></a></p></td>
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff561656" data-raw-source="[&lt;strong&gt;KSDATAFORMAT&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff561656)"><strong>KSDATAFORMAT</strong></a></p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>注釈
-------

このプロパティは、 [ **KSDATAFORMAT** ](https://msdn.microsoft.com/library/windows/hardware/ff561656)要求されたデータ形式を指定します。

のみ、KS フィルターは、クライアントが現在のプロパティをリセットすることを許可する場合、または指定された不完全なデータ形式で接続ができる場合は、このプロパティをサポートする必要があります。

KSPROPERTY の詳細については\_接続\_DATAFORMAT のプロパティを参照してください[KS データ形式とデータ範囲](https://msdn.microsoft.com/library/windows/hardware/ff567632)と[AVStream のデータ範囲の交差部分](https://msdn.microsoft.com/library/windows/hardware/ff558680)します。

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


[**KSSTREAM\_ヘッダー**](https://msdn.microsoft.com/library/windows/hardware/ff567138)

[**KSPROPERTY\_接続\_PROPOSEDATAFORMAT**](ksproperty-connection-proposedataformat.md)

[**KSPROPERTY\_PIN\_PROPOSEDATAFORMAT**](ksproperty-pin-proposedataformat.md)

 

 







---
title: KSK プロパティ\_接続\_ACQUIREORDERING
description: KSK プロパティ\_CONNECTION\_ACQUIREORDERING プロパティは、状態の変更順序が重要な場合に pin に実装する必要があるオプションのプロパティです。
ms.assetid: b0d27615-bece-49b1-8497-f3c389ea37fc
keywords:
- KSPROPERTY_CONNECTION_ACQUIREORDERING ストリーミングメディアデバイス
topic_type:
- apiref
api_name:
- KSPROPERTY_CONNECTION_ACQUIREORDERING
api_location:
- ks.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: e0a989d17655c03a8402c6f2c2fff079fa52790a
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72826854"
---
# <a name="ksproperty_connection_acquireordering"></a>KSK プロパティ\_接続\_ACQUIREORDERING


KSK プロパティ\_CONNECTION\_ACQUIREORDERING プロパティは、状態の変更順序が重要な場合に pin に実装する必要があるオプションのプロパティです。 たとえば、シンクが通信ソースピンに接続されているピンが、シンク pin が設定される前に取得状態に設定されるようにする必要がある場合は、通信シンクの pin にプロパティを実装する必要があります。

## <span id="ddk_ksproperty_connection_acquireordering_ks"></span><span id="DDK_KSPROPERTY_CONNECTION_ACQUIREORDERING_KS"></span>


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
<td><p>必須ではない</p></td>
<td><p>Pin</p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksidentifier" data-raw-source="[&lt;strong&gt;KSPROPERTY&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksidentifier)"><strong>KSPROPERTY</strong></a></p></td>
<td><p>型</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>注釈
-------

このプロパティは、状態変更の順序が重要な場合に**TRUE**を返します。 **FALSE**が返される場合は、プロパティを実装する必要はありません。

この読み取り専用プロパティを使用して、この通信シンクの pin に対して、取得までの状態の変更を停止するかどうかを判断します。 プロパティが実装されていない場合、順序付けは重要ではないと想定されます。 IRP ベースのデータフローでは、要求に対して新しい Irp を作成するのではなく、ストリーミングの Irp を転送するときに pin によって実装されます。したがって、接続されたソースの pin に対する正しいスタックの深さを示す必要があります。 Pin が Irp を転送しなかった場合、フィルターのスタックの深さが静的であるため、スタックの深さの再計算は重要ではありません。

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


[KSPROPSETID\_接続](kspropsetid-connection.md)

 

 







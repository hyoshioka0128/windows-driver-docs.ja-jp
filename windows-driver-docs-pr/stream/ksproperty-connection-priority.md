---
title: KSPROPERTY\_接続\_優先順位
description: クライアントの使用、KSPROPERTY\_接続\_PRIORITY プロパティを取得または接続の優先順位を設定します。
ms.assetid: 2037fe95-e176-4714-ad36-65a0e25b29e0
keywords:
- KSPROPERTY_CONNECTION_PRIORITY ストリーミング メディア デバイス
topic_type:
- apiref
api_name:
- KSPROPERTY_CONNECTION_PRIORITY
api_location:
- ks.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1da8feeb8df2bf19637ea68cc4d3cbbc5f84fc7c
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67373112"
---
# <a name="kspropertyconnectionpriority"></a>KSPROPERTY\_接続\_優先順位


クライアントの使用、KSPROPERTY\_接続\_PRIORITY プロパティを取得または接続の優先順位を設定します。

## <span id="ddk_ksproperty_connection_priority_ks"></span><span id="DDK_KSPROPERTY_CONNECTION_PRIORITY_KS"></span>


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
<td><p>Pin</p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksidentifier" data-raw-source="[&lt;strong&gt;KSPROPERTY&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksidentifier)"><strong>KSPROPERTY</strong></a></p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-kspriority" data-raw-source="[&lt;strong&gt;KSPRIORITY&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-kspriority)"><strong>KSPRIORITY</strong></a></p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>注釈
-------

このプロパティは、型の構造体を返す[ **KSPRIORITY** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-kspriority)格納している、優先度クラスとサブクラスです。

1 つの優先度がもう 1 つの場合よりも大きい、 **PriorityClass**メンバー値が大きい場合は、 **PriorityClass**メンバーが同じ、 **PrioritySubClass**メンバーは、大きい。

次の値を定義済み**PriorityClass**利用します。KSPRIORITY\_低、KSPRIORITY\_標準、KSPRIORITY\_高、および KSPRIORITY\_排他。 優先度の既定値は KSPRIORITY\_標準。 KSPRIORITY\_排他的では、接続は、pin で使用されるリソースへの排他アクセスを示します。

優先度の値があるグローバルな有意性: クライアントは、報告された値を使用して、2 つのカーネルが関連付けられていないストリーム フィルターに 2 つの異なる pin の間の優先順位を設定します。

KSPROPERTY\_接続\_優先順位は省略可能です。 クライアントが KSPRIORITY の優先順位を持つものとしてはサポートしないピンを扱う\_標準。

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


[**KSPRIORITY**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-kspriority)

[**KSPIN\_接続**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-kspin_connect)

 

 







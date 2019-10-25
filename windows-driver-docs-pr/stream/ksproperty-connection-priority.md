---
title: KSK プロパティ\_接続\_優先度
description: クライアントは、KSK プロパティ\_接続\_PRIORITY プロパティを使用して、接続の優先順位を取得または設定します。
ms.assetid: 2037fe95-e176-4714-ad36-65a0e25b29e0
keywords:
- KSPROPERTY_CONNECTION_PRIORITY ストリーミングメディアデバイス
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
ms.openlocfilehash: 53ef527df994157b0da2f6775e7dd225589789ce
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72826784"
---
# <a name="ksproperty_connection_priority"></a>KSK プロパティ\_接続\_優先度


クライアントは、KSK プロパティ\_接続\_PRIORITY プロパティを使用して、接続の優先順位を取得または設定します。

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
<td><p>Pin</p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksidentifier" data-raw-source="[&lt;strong&gt;KSPROPERTY&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksidentifier)"><strong>KSPROPERTY</strong></a></p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-kspriority" data-raw-source="[&lt;strong&gt;KSPRIORITY&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-kspriority)"><strong>KSPRIORITY</strong></a></p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>注釈
-------

このプロパティは、優先度クラスとサブクラスを含む[**KSPRIORITY**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-kspriority)型の構造体を返します。

優先度**クラス**のメンバーが大きい場合、または優先**度クラスの**メンバーが等しい場合、または優先度**サブ**クラスのメンバーが大きい場合、1つの優先順位はもう一方の優先順位よりも大きくなります。

優先**順位クラス**の次の定義済みの値を使用できます: KSPRIORITY\_LOW、KSPRIORITY\_NORMAL、KSPRIORITY\_HIGH、および KSPRIORITY\_EXCLUSIVE。 優先順位の既定値は KSPRIORITY\_NORMAL です。 KSPRIORITY\_EXCLUSIVE は、接続が pin によって使用されるリソースに排他的にアクセスできることを示します。

優先順位値にはグローバルな意味があります。クライアントは、報告された値を使用して、2つの関連のないカーネルストリーミングフィルターで2つの異なるピン間に優先順位を設定できます。

KSK プロパティ\_接続\_優先順位は省略可能です。 クライアントは、それをサポートしていない pin を、優先度 KSPRIORITY\_通常のものとして扱います。

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


[**KSPRIORITY**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-kspriority)

[**KSPIN\_接続**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-kspin_connect)

 

 







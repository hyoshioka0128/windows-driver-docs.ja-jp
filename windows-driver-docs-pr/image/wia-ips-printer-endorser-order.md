---
title: WIA\_IP\_プリンター\_裏書き\_順序
description: WIA\_IP\_プリンター\_裏書き\_順序プロパティを使用して、スキャンと imprinting/動作保証済みの操作の相対的な実行される順序を構成します。 WIA ミニドライバーは、作成し、このプロパティを保持します。
ms.assetid: DE146E16-C956-497D-BAF5-F7CE6FAF382B
keywords:
- WIA_IPS_PRINTER_ENDORSER_ORDER イメージング デバイス
topic_type:
- apiref
api_name:
- WIA_IPS_PRINTER_ENDORSER_ORDER
api_location:
- Wiadef.h
api_type:
- HeaderDef
ms.date: 05/22/2018
ms.localizationpriority: medium
ms.openlocfilehash: e6f322a6a021c5c4a965ea7a32ba34c1750b88fa
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56528807"
---
# <a name="wiaipsprinterendorserorder"></a>WIA\_IP\_プリンター\_裏書き\_順序


**WIA\_IP\_プリンター\_裏書き\_順序**プロパティは、スキャンと imprinting/動作保証済みの操作のそれぞれに対して相対的に実行される順序を構成するために使用その他。 WIA ミニドライバーは、作成し、このプロパティを保持します。




プロパティの種類:VT\_I4

有効な値 :WIA\_PROP\_NONE

アクセス権:読み取り専用かどうか

<a name="remarks"></a>注釈
-------

次の表では有効な定数、 [ **WIA\_IP\_プレビュー\_型**](wia-ips-preview-type.md)プロパティ。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>Value</th>
<th>定義</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>WIA_PRINTER_ENDORSER_BEFORE_SCAN</p></td>
<td><p>このドキュメントのページがスキャンされる前に印刷/保証がドキュメントのページで実行します。</p></td>
</tr>
<tr class="even">
<td><p>WIA_PRINTER_ENDORSER_AFTER_SCAN</p></td>
<td><p>このドキュメントのページがスキャンされた後、ドキュメントのページで印刷/保証実行されます。</p></td>
</tr>
</tbody>
</table>

 

このプロパティは、すべて・ インプリント ・/裏書きデータ ソース アイテムをサポートする必要があります。 必要な既定値はありません。

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
<td>Wiadef.h (Wiadef.h を含む)</td>
</tr>
</tbody>
</table>

 

 






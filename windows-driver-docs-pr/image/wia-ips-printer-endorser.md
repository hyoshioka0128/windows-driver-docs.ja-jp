---
title: WIA\_IP\_プリンター\_裏書き
description: WIA\_IP\_プリンター\_裏書きプロパティは、プリンター/裏書きデバイスが、および、imprinting を有効にするこれらの場所のいずれかを選択して、アプリケーションが使用場所を一覧表示する WIA ミニドライバーによって使用されます/保証します。
ms.assetid: A9BAC8D3-AB06-4600-9EF7-E9F4846B5215
keywords:
- WIA_IPS_PRINTER_ENDORSER イメージング デバイス
topic_type:
- apiref
api_name:
- WIA_IPS_PRINTER_ENDORSER
api_location:
- Wiadef.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7ddbd707ae477f799c02d9a09f5cd30855b5f148
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56537255"
---
# <a name="wiaipsprinterendorser"></a>WIA\_IP\_プリンター\_裏書き


**WIA\_IP\_プリンター\_裏書き**プロパティは、プリンター/裏書きデバイスが利用しのいずれかを選択して、アプリケーションが使用場所を一覧表示する WIA ミニドライバーによって使用されますこれらの場所/imprinting 保証を有効にします。 WIA ミニドライバーは、作成し、このプロパティを保持します。




プロパティの種類:VT\_I4

有効な値 :WIA\_PROP\_一覧

アクセス権:読み取り/書き込み

<a name="remarks"></a>注釈
-------

次の表に、必要な値を**WIA\_IP\_プリンター\_裏書き**プロパティ。

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
<td><p>WIA_PRINTER_ENDORSER_DISABLED</p></td>
<td><p>印刷/保証が無効です。 これは、プロパティの必要な既定値です。</p></td>
</tr>
<tr class="even">
<td><p>WIA_PRINTER_ENDORSER_AUTO</p></td>
<td><p>印刷/保証が有効になっているとします。 場所 (複数の場所がこの・ インプリント ・/裏書きの使用可能な) 場合は、アクティブなスキャンの入力ソースによって実行時にデバイスで自動的に選択されます。</p></td>
</tr>
</tbody>
</table>

 

WIA ミニドライバーは、プロパティの構成を受け入れるように許可されていますが、スキャン時に非アクティブなスキャンの入力ソースに印刷/保証を有効にする要求は無視されます。

次の表の省略可能な値、 **WIA\_IP\_プリンター\_裏書き**プロパティ。

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
<td><p>WIA_PRINTER_ENDORSER_FLATBED</p></td>
<td><p>フラット ベッド スキャナーでスキャンされたドキュメントの印刷/保証が有効になっています。</p></td>
</tr>
<tr class="even">
<td><p>WIA_PRINTER_ENDORSER_FEEDER_FRONT</p></td>
<td><p>印刷/保証 (一方向または双方向の画像のスキャン モードのいずれか) フィーダーをスキャンしたドキュメントの前面にある有効です。</p></td>
</tr>
<tr class="odd">
<td><p>WIA_PRINTER_ENDORSER_FEEDER_BACK</p></td>
<td><p>印刷/保証 (一方向または双方向の画像のスキャン モードのいずれか) フィーダーをスキャンしたドキュメントの背面にある有効です。</p></td>
</tr>
<tr class="even">
<td><p>WIA_PRINTER_ENDORSER_FEEDER_DUPLEX</p></td>
<td><p>(一方向または双方向の画像のスキャン モードのいずれか) フィーダーをスキャンしたドキュメントの両方の側の印刷/保証が有効になっています。</p></td>
</tr>
</tbody>
</table>

 

このプロパティは、すべて・ インプリント ・/裏書きデータ ソース アイテムをサポートする必要があります。 必要な既定値は**WIA\_プリンター\_裏書き\_無効**します。

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

 

 






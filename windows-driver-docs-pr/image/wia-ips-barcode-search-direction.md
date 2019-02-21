---
title: WIA\_IP\_バーコード\_検索\_方向
description: WIA\_IP\_バーコード\_検索\_DIRECTION プロパティは、バーコードをスキャンしたドキュメントの各ページ上のデバイスを検索する (スキャン方向) の相対方向の構成に使用されます。
ms.assetid: 8A328AEE-EAFD-4282-B902-D29BB8175461
keywords:
- WIA_IPS_BARCODE_SEARCH_DIRECTION イメージング デバイス
topic_type:
- apiref
api_name:
- WIA_IPS_BARCODE_SEARCH_DIRECTION
api_location:
- Wiadef.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: b727e046055c0baf2de077f4e916b6824b8823d4
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56535699"
---
# <a name="wiaipsbarcodesearchdirection"></a>WIA\_IP\_バーコード\_検索\_方向


**WIA\_IP\_バーコード\_検索\_方向**プロパティを使用して、各でバーコードのデバイスを検索する (スキャン方向) の相対方向の構成スキャンしたドキュメントのページです。




プロパティの種類:VT\_I4

有効な値 :WIA\_PROP\_一覧

アクセス権:読み取り/書き込み

<a name="remarks"></a>注釈
-------

次の表に、有効な値、 **WIA\_IP\_バーコード\_検索\_方向**プロパティ。

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
<td><p>WIA_BARCODE_HORIZONTAL_SEARCH</p></td>
<td><p>デバイスは、バーコードの水平方向に検索します。</p></td>
</tr>
<tr class="even">
<td><p>WIA_BARCODE_VERTICAL_SEARCH</p></td>
<td><p>デバイスは、バーコードの垂直方向に検索します。</p></td>
</tr>
<tr class="odd">
<td><p>WIA_BARCODE_HORIZONTAL_VERTICAL_SEARCH</p></td>
<td><p>水平方向、垂直方向に、デバイスは最初のバーコードを検索します。</p></td>
</tr>
<tr class="even">
<td><p>WIA_BARCODE_VERTICAL_HORIZONTAL_SEARCH</p></td>
<td><p>垂直方向にし、水平方向に、デバイスは最初のバーコードを検索します。</p></td>
</tr>
<tr class="odd">
<td><p>WIA_BARCODE_AUTO_SEARCH</p></td>
<td><p>デバイスは、独自の方向に自動的に実行時に検出したり、定義済みのバーコードを検索します。</p></td>
</tr>
</tbody>
</table>

 

このプロパティは、バーコード リーダーのすべてのアイテムに必要な WIA のみをサポートするために実装することが\_バーコード\_自動\_検索値。

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

 

 






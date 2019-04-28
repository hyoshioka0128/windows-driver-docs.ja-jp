---
title: WIA\_IP\_PATCH\_コード\_検索\_方向
description: WIA\_IP\_PATCH\_コード\_検索\_DIRECTION プロパティは、デバイスがスキャン ドキュメントのそれぞれで修正プログラム コードを検索する (スキャン方向) の相対方向の構成に使用されますページです。
ms.assetid: 24541B0D-4B9B-439F-8454-AFDD3D16A448
keywords:
- WIA_IPS_PATCH_CODE_SEARCH_DIRECTION イメージング デバイス
topic_type:
- apiref
api_name:
- WIA_IPS_PATCH_CODE_SEARCH_DIRECTION
api_location:
- Wiadef.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4a7a85ef48aeddb01938814acb7fdbd2ce1bc53e
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63366786"
---
# <a name="wiaipspatchcodesearchdirection"></a>WIA\_IP\_PATCH\_コード\_検索\_方向


**WIA\_IP\_PATCH\_コード\_検索\_方向**(スキャン方向) の相対方向を構成するプロパティが使用されるデバイス各スキャンのドキュメント ページで、修正プログラム コードを検索します。




プロパティの種類:VT\_I4

有効な値 :WIA\_PROP\_一覧

アクセス権:[読み取り/書き込み]

<a name="remarks"></a>注釈
-------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>値</th>
<th>定義</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>WIA_PATCH_CODE_HORIZONTAL_SEARCH</p></td>
<td><p>デバイスは、水平方向に修正プログラム コードを検索します。</p></td>
</tr>
<tr class="even">
<td><p>WIA_PATCH_CODE_VERTICAL_SEARCH</p></td>
<td><p>デバイスは、垂直方向に修正プログラム コードを検索します。</p></td>
</tr>
<tr class="odd">
<td><p>WIA_PATCH_CODE_HORIZONTAL_VERTICAL_SEARCH</p></td>
<td><p>水平方向、垂直方向に、デバイスは最初に修正プログラム コードを検索します。</p></td>
</tr>
<tr class="even">
<td><p>WIA_PATCH_CODE_VERTICAL_HORIZONTAL_SEARCH</p></td>
<td><p>垂直方向にし、水平方向に、デバイスは最初に修正プログラム コードを検索します。</p></td>
</tr>
<tr class="odd">
<td><p>WIA_PATCH_CODE_AUTO_SEARCH</p></td>
<td><p>デバイスは、実行時または定義済みで自動的に検出されますが、独自の方向に修正プログラム コードを検索します。</p></td>
</tr>
</tbody>
</table>

 

このプロパティは必須の修正プログラム コード リーダーのすべての項目が、WIA のみをサポートするために実装できます\_パッチ\_コード\_自動\_検索値。

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

 

 






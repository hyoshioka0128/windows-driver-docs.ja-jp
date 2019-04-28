---
title: WIA\_IP\_経由で\_スキャン
description: WIA\_IP\_経由で\_スキャン プロパティを有効にして、スキャン (物理的なドキュメントの境界を越えてスキャン) 経由の構成に使用します。 WIA ミニドライバーは、作成し、このプロパティを保持します。
ms.assetid: CAE654BE-B0AC-4182-83CE-C2BDA4792FE4
keywords:
- WIA_IPS_OVER_SCAN イメージング デバイス
topic_type:
- apiref
api_name:
- WIA_IPS_OVER_SCAN
api_location:
- Wiadef.h
api_type:
- HeaderDef
ms.date: 05/22/2018
ms.localizationpriority: medium
ms.openlocfilehash: 41b1c1f5235ec72bec364c8afe8776f2b18f22ce
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63379822"
---
# <a name="wiaipsoverscan"></a>WIA\_IP\_経由で\_スキャン


**WIA\_IP\_経由で\_スキャン**を有効にし、スキャン (物理的なドキュメントの境界を越えてスキャン) に対する構成プロパティを使用します。 WIA ミニドライバーは、作成し、このプロパティを保持します。




プロパティの種類:VT\_I4

有効な値 :WIA\_PROP\_一覧

アクセス権:[読み取り/書き込み]

<a name="remarks"></a>注釈
-------

次の表に、有効な値、 **WIA\_IP\_経由で\_スキャン**プロパティ。

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
<td><p>WIA_OVER_SCAN_DISABLED</p></td>
<td><p>スキャンでは無効です。 これは、プロパティがサポートされている場合に必要な既定値です。</p></td>
</tr>
<tr class="even">
<td><p>WIA_ OVER_SCAN_TOP_BOTTOM</p></td>
<td><p>上のドキュメントの上部と下部の辺にスキャンします。</p></td>
</tr>
<tr class="odd">
<td><p>WIA_ OVER_SCAN_LEFT_RIGHT</p></td>
<td><p>上のドキュメントの左側および右側にスキャンします。</p></td>
</tr>
<tr class="even">
<td><p>すべて WIA_ OVER_SCAN_</p></td>
<td><p>上のドキュメントのすべての辺にスキャンします。</p></td>
</tr>
</tbody>
</table>

 

このプロパティは、フラット ベッドを含むすべてプログラミング可能なイメージのデータ ソース アイテムの有効な (WIA\_カテゴリ\_ベッド) とフィーダー (WIA\_カテゴリ\_フィーダー) は省略可能です。 プロパティがサポートされている、WIA\_経由で\_スキャン\_無効になっていますが、必要な既定値。

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
<td>Wiadef.h (Wiadef.h を含む)</td>
</tr>
</tbody>
</table>

 

 






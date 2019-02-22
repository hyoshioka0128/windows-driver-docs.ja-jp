---
title: WIA\_IP\_空白\_ページ
description: WIA\_IP\_空白\_ページのプロパティが空白のページの検出を構成するために使用します。 WIA ミニドライバーは、作成し、このプロパティを保持します。
ms.assetid: FB2EBC0D-6F09-4B64-9B79-7EE20CAF7023
keywords:
- WIA_IPS_BLANK_PAGES イメージング デバイス
topic_type:
- apiref
api_name:
- WIA_IPS_BLANK_PAGES
api_location:
- Wiadef.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0f8a3ab871c0188a73a86caa7078a7c1b332ac38
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56556712"
---
# <a name="wiaipsblankpages"></a>WIA\_IP\_空白\_ページ


**WIA\_IP\_空白\_ページ**プロパティが空白のページの検出を構成するために使用します。 WIA ミニドライバーは、作成し、このプロパティを保持します。




プロパティの種類:VT\_I4

有効な値 :WIA\_PROP\_一覧

アクセス権:読み取り/書き込み

<a name="remarks"></a>注釈
-------

次の表に、有効な値、 **WIA\_IP\_空白\_ページ**プロパティ。

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
<td><p>WIA_BLANK_PAGE_DETECTION_DISABLED</p></td>
<td><p>空白のページの検出を無効にします。 これは、プロパティがサポートされている場合に必要な既定値です。</p></td>
</tr>
<tr class="even">
<td><p>WIA_BLANK_PAGE_DISCARD</p></td>
<td><p>デバイス検出空白ページ、およびそれらのスキャンを自動的にスキップします (破棄は、存在する場合にデータをスキャン) のスキャンを続行します。</p></td>
</tr>
<tr class="odd">
<td><p>WIA_BLANK_PAGE_JOB_SEPARATOR</p></td>
<td><p>デバイスが空白のページを検出し、機能で構成された、 <a href="wia-ips-job-separators.md" data-raw-source="[&lt;strong&gt;WIA_IPS_JOB_SEPARATORS&lt;/strong&gt;](wia-ips-job-separators.md)"> <strong>WIA_IPS_JOB_SEPARATORS</strong> </a>プロパティ。 フィーダー項目がサポートされている場合にのみ、この値が正しく、 <strong>WIA_IPS_JOB_SEPARATORS</strong>プロパティ。</p></td>
</tr>
</tbody>
</table>

 

このプロパティは省略可能で、フィーダー付きのデータ ソース アイテムにのみ有効です (で表される、 [ **WIA\_IPA\_項目\_カテゴリ**](wia-ipa-item-category.md)として WIAプロパティ\_カテゴリ\_フィーダー)。

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

 

 






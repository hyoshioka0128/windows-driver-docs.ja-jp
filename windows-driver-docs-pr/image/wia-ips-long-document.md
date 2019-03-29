---
title: WIA\_IP\_長い\_ドキュメント
description: WIA\_IP\_長い\_ドキュメント プロパティは、長いドキュメントのスキャンがサポートされているかどうかを報告する WIA ミニドライバーとこの機能を有効にする、WIA クライアント アプリケーションで使用します。 WIA ミニドライバーは、作成し、このプロパティを保持します。
ms.assetid: FEFB77EE-8377-406C-A244-84E1BEF57808
keywords:
- WIA_IPS_LONG_DOCUMENT イメージング デバイス
topic_type:
- apiref
api_name:
- WIA_IPS_LONG_DOCUMENT
api_location:
- Wiadef.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3be2ca4a9d3f5b1842507ad9a8c79f874ed8358d
ms.sourcegitcommit: b3859d56cb393e698c698d3fb13519ff1522c7f3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/05/2019
ms.locfileid: "57348589"
---
# <a name="wiaipslongdocument"></a>WIA\_IP\_長い\_ドキュメント


**WIA\_IP\_長い\_ドキュメント**WIA クライアント アプリケーションでこの機能を有効にして長いドキュメントのスキャンがサポートされているかどうかを報告する WIA ミニドライバーによってプロパティが使用されます。 WIA ミニドライバーは、作成し、このプロパティを保持します。




プロパティの種類:VT\_I4

有効な値 :WIA\_PROP\_一覧

アクセス権:読み取り/書き込み

<a name="remarks"></a>コメント
-------

次の表に、有効な値、 **WIA\_IP\_長い\_ドキュメント**プロパティ。

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
<td><p>WIA_LONG_DOCUMENT_DISABLED</p></td>
<td><p>長いドキュメントのスキャンが無効です。 これは、プロパティがサポートされている場合に必要な既定値です。</p></td>
</tr>
<tr class="even">
<td><p>WIA_LONG_DOCUMENT_ENABLED</p></td>
<td><p>デバイスは、デバイスの可能な最大長まで長いドキュメントをスキャンします。 <a href="wia-ips-page-size.md" data-raw-source="[&lt;strong&gt;WIA_IPS_PAGE_SIZE&lt;/strong&gt;](wia-ips-page-size.md)"> <strong>WIA_IPS_PAGE_SIZE</strong> </a>プロパティは、許容されるためにこの値に対して WIA_PAGE_AUTO に設定する必要があります。</p></td>
</tr>
<tr class="odd">
<td><p>WIA_LONG_DOCUMENT_SPLIT</p></td>
<td><p>長いドキュメントは自動的に分割 (および別のイメージとして転送されます) 現在の<a href="wia-ips-page-size.md" data-raw-source="[&lt;strong&gt;WIA_IPS_PAGE_SIZE&lt;/strong&gt;](wia-ips-page-size.md)"> <strong>WIA_IPS_PAGE_SIZE</strong> </a>長さ。 最後にスキャンしたページを短くすることができます。</p></td>
</tr>
</tbody>
</table>

 

このプロパティは省略可能で、フィーダー付きのデータ ソース アイテムにのみ有効です (で表される、 [ **WIA\_IPA\_項目\_カテゴリ**](wia-ipa-item-category.md)として WIAプロパティ\_カテゴリ\_フィーダー)。

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

 

 






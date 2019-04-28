---
title: 同じ ID と名前を持つ WIA プロパティのマッピング
description: 同じ ID と名前を持つ WIA プロパティのマッピング
ms.assetid: 40a1094d-50fa-42b6-9976-ec6b05fdc384
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6a9c3b2adbc9531b84e1920b2d4c80bb1140f0a4
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63380365"
---
# <a name="mapping-wia-properties-with-the-same-ids-and-names"></a>同じ ID と名前を持つ WIA プロパティのマッピング


同じプロパティの Id と Windows Vista 対応としてプロパティ名を持つ Windows XP プロパティがあります。 これらの Windows XP ルート プロパティと Windows vista に変換されるフラット ベッドとフィーダー (ADF) のプロパティのテーブルは、次のとおりです。

<table>
<colgroup>
<col width="25%" />
<col width="25%" />
<col width="25%" />
<col width="25%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p><strong>Windows XP のプロパティ</strong></p></td>
<td><p><strong>Windows XP</strong></p>
<p><strong>アイテム/コンテキスト</strong></p></td>
<td><p><strong>Windows Vista のプロパティ</strong></p></td>
<td><p><strong>Windows Vista の項目</strong></p></td>
</tr>
<tr class="even">
<td><p>WIA_IPA_ITEM_NAME</p>
<p>読み取り専用アクセスの注参照: d</p></td>
<td><p>ルート</p>
<p>注を参照してください: c</p></td>
<td><p>WIA_IPA_ITEM_NAME</p>
<p>読み取り専用アクセスの注参照: d</p></td>
<td><p>ルート</p>
<p>注を参照してください: c</p></td>
</tr>
<tr class="odd">
<td><p>WIA_IPA_ITEM_NAME</p>
<p>または、ジェネリック。「フラット ベッド」</p>
<p>読み取り専用アクセスの「注: d および e</p></td>
<td><p>子/ベッド</p>
<p>注を参照してください: b</p></td>
<td><p>WIA_IPA_ITEM_NAME</p>
<p>読み取り専用アクセスの「注: d および e</p></td>
<td><p>フラット ベッド</p>
<p>注を参照してください: b</p></td>
</tr>
<tr class="even">
<td><p>WIA_IPA_ITEM_NAME</p>
<p>または、ジェネリック。「フィーダー」</p>
<p>読み取り専用アクセスの「注: d および e</p></td>
<td><p>子/フィーダー</p>
<p>注を参照してください、。</p></td>
<td><p>WIA_IPA_ITEM_NAME</p>
<p>読み取り専用アクセスの「注: d および e</p></td>
<td><p>フィーダー</p>
<p>注を参照してください、。</p></td>
</tr>
<tr class="odd">
<td><p>WIA_IPA_FULL_ITEM_NAME</p>
<p>読み取り専用アクセスの注参照: d</p></td>
<td><p>ルート</p>
<p>注を参照してください: c</p></td>
<td><p>WIA_IPA_FULL_ITEM_NAME</p>
<p>読み取り専用アクセスの注参照: d</p></td>
<td><p>ルート</p>
<p>注を参照してください: c</p></td>
</tr>
<tr class="even">
<td><p>WIA_IPA_FULL_ITEM_NAME</p>
<p>ジェネリックまたは:"\Root\FLATBED"</p>
<p>読み取り専用アクセスの「注: d および e</p></td>
<td><p>子/ベッド</p>
<p>注を参照してください: b</p></td>
<td><p>WIA_IPA_FULL_ITEM_NAME</p>
<p>読み取り専用アクセス</p></td>
<td><p>フラット ベッド</p>
<p>注を参照してください: b</p></td>
</tr>
<tr class="odd">
<td><p>WIA_IPA_FULL_ITEM_NAME</p>
<p>or Generic: "\Root\FEEDER"</p>
<p>読み取り専用アクセス</p></td>
<td><p>子/フィーダー</p>
<p>注を参照してください、。</p></td>
<td><p>WIA_IPA_FULL_ITEM_NAME</p>
<p>読み取り専用アクセスの「注: d および e</p></td>
<td><p>フィーダー</p>
<p>注を参照してください、。</p></td>
</tr>
<tr class="even">
<td><p>WIA_IPA_ITEM_TIME</p>
<p>読み取り専用アクセス</p></td>
<td><p>子/ベッド</p>
<p>注を参照してください: b</p></td>
<td><p>WIA_IPA_ITEM_TIME</p>
<p>読み取り専用アクセス</p></td>
<td><p>フラット ベッド</p>
<p>注を参照してください: b</p></td>
</tr>
<tr class="odd">
<td><p>WIA_IPA_ITEM_TIME</p>
<p>読み取り専用アクセス</p></td>
<td><p>子/フィーダー</p>
<p>注を参照してください、。</p></td>
<td><p>WIA_IPA_ITEM_TIME</p>
<p>読み取り専用アクセス</p></td>
<td><p>フィーダー</p>
<p>注を参照してください、。</p></td>
</tr>
<tr class="even">
<td><p>WIA_IPA_ITEM_FLAGS</p>
<p>読み取り専用アクセスの「注: d および e</p></td>
<td><p>ルート</p>
<p>注を参照してください: c</p></td>
<td><p>WIA_IPA_ITEM_FLAGS</p>
<p>読み取り専用アクセスの「注: d および e</p></td>
<td><p>ルート</p>
<p>注を参照してください: c</p></td>
</tr>
<tr class="odd">
<td><p>WIA_IPA_ITEM_FLAGS</p>
<p>読み取り専用アクセスの「注: d および e</p></td>
<td><p>子/ベッド</p>
<p>注を参照してください: b</p></td>
<td><p>WIA_IPA_ITEM_FLAGS</p>
<p>読み取り専用アクセスの「注: d および e</p></td>
<td><p>フラット ベッド</p>
<p>注を参照してください: b</p></td>
</tr>
<tr class="even">
<td><p>WIA_IPA_ITEM_FLAGS</p>
<p>読み取り専用アクセスの「注: d および e</p></td>
<td><p>子/フィーダー</p>
<p>注を参照してください、。</p></td>
<td><p>WIA_IPA_ITEM_FLAGS</p>
<p>読み取り専用アクセスの「注: d および e</p></td>
<td><p>フィーダー</p>
<p>注を参照してください、。</p></td>
</tr>
<tr class="odd">
<td><p>WIA_IPA_ACCESS_RIGHTS</p>
<p>読み取り専用アクセス</p></td>
<td><p>ルート</p>
<p>注を参照してください: c</p></td>
<td><p>WIA_IPA_ACCESS_RIGHTS</p>
<p>読み取り専用アクセス</p></td>
<td><p>ルート</p>
<p>注を参照してください: c</p></td>
</tr>
<tr class="even">
<td><p>WIA_IPA_ACCESS_RIGHTS</p>
<p>読み取り専用アクセス</p></td>
<td><p>子/ベッド</p>
<p>注を参照してください: b</p></td>
<td><p>WIA_IPA_ACCESS_RIGHTS</p>
<p>読み取り専用アクセス</p></td>
<td><p>フラット ベッド</p>
<p>注を参照してください: b</p></td>
</tr>
<tr class="odd">
<td><p>WIA_IPA_ACCESS_RIGHTS</p>
<p>読み取り専用アクセス</p></td>
<td><p>子/フィーダー</p>
<p>注を参照してください、。</p></td>
<td><p>WIA_IPA_ACCESS_RIGHTS</p>
<p>読み取り専用アクセス</p></td>
<td><p>フィーダー</p>
<p>注を参照してください、。</p></td>
</tr>
<tr class="even">
<td><p>WIA_IPA_DATATYPE</p>
<p>注を参照してください: b</p></td>
<td><p>子/ベッド</p>
<p>注を参照してください: b</p></td>
<td><p>WIA_IPA_DATATYPE</p>
<p>読み取り/書き込みアクセス</p></td>
<td><p>フラット ベッド</p>
<p>注を参照してください: b</p></td>
</tr>
<tr class="odd">
<td><p>WIA_IPA_DATATYPE</p>
<p>読み取り/書き込みアクセス</p></td>
<td><p>子/フィーダー</p>
<p>注を参照してください、。</p></td>
<td><p>WIA_IPA_DATATYPE</p>
<p>読み取り/書き込みアクセス</p></td>
<td><p>フィーダー</p>
<p>注を参照してください、。</p></td>
</tr>
<tr class="even">
<td><p>WIA_IPA_DEPTH</p>
<p>読み取り/書き込みアクセス</p></td>
<td><p>子/ベッド</p>
<p>注を参照してください: b</p></td>
<td><p>WIA_IPA_DEPTH</p>
<p>読み取り/書き込みアクセス</p></td>
<td><p>フラット ベッド</p>
<p>注を参照してください: b</p></td>
</tr>
<tr class="odd">
<td><p>WIA_IPA_DEPTH</p>
<p>読み取り/書き込みアクセス</p></td>
<td><p>子/フィーダー</p>
<p>注を参照してください、。</p></td>
<td><p>WIA_IPA_DEPTH</p>
<p>読み取り/書き込みアクセス</p></td>
<td><p>フィーダー</p>
<p>注を参照してください、。</p></td>
</tr>
<tr class="even">
<td><p>WIA_IPA_PREFERRED_FORMAT</p>
<p>読み取り専用アクセスの注参照: f#</p></td>
<td><p>子/ベッド</p>
<p>注を参照してください: b</p></td>
<td><p>WIA_IPA_PREFERRED_FORMAT</p>
<p>読み取り専用アクセスの注参照: f#</p></td>
<td><p>フラット ベッド</p>
<p>注を参照してください: b</p></td>
</tr>
<tr class="odd">
<td><p>WIA_IPA_PREFERRED_FORMAT</p>
<p>読み取り専用アクセスの注参照: f#</p></td>
<td><p>子/フィーダー</p>
<p>注を参照してください、。</p></td>
<td><p>WIA_IPA_PREFERRED_FORMAT</p>
<p>読み取り専用アクセスの注参照: f#</p></td>
<td><p>フィーダー</p>
<p>注を参照してください、。</p></td>
</tr>
<tr class="even">
<td><p>WIA_IPA_FORMAT</p>
<p>読み取り/書き込みアクセスの「注: h、i</p></td>
<td><p>子/ベッド</p>
<p>注を参照してください: b</p></td>
<td><p>WIA_IPA_FORMAT</p>
<p>読み取り/書き込みアクセスの「注: h、i</p></td>
<td><p>フラット ベッド</p>
<p>注を参照してください: b</p></td>
</tr>
<tr class="odd">
<td><p>WIA_IPA_FORMAT</p>
<p>読み取り/書き込みアクセスの「注: h、i</p></td>
<td><p>子/フィーダー</p>
<p>注を参照してください、。</p></td>
<td><p>WIA_IPA_FORMAT</p>
<p>読み取り/書き込みアクセスの「注: h、i</p></td>
<td><p>フィーダー</p>
<p>注を参照してください、。</p></td>
</tr>
<tr class="even">
<td><p>WIA_IPA_COMPRESSION</p>
<p>読み取り/書き込みアクセス</p></td>
<td><p>子/ベッド</p>
<p>注を参照してください: b</p></td>
<td><p>WIA_IPA_COMPRESSION</p>
<p>読み取り/書き込みアクセス</p></td>
<td><p>フラット ベッド</p>
<p>注を参照してください: b</p></td>
</tr>
<tr class="odd">
<td><p>WIA_IPA_COMPRESSION</p>
<p>読み取り/書き込みアクセス</p></td>
<td><p>子/フィーダー</p>
<p>注を参照してください、。</p></td>
<td><p>WIA_IPA_COMPRESSION</p>
<p>読み取り/書き込みアクセス</p></td>
<td><p>フィーダー</p>
<p>注を参照してください、。</p></td>
</tr>
<tr class="even">
<td><p>WIA_IPA_TYMED</p>
<p>読み取り/書き込みアクセスの「注: h、i、k</p></td>
<td><p>子/ベッド</p>
<p>注を参照してください: b</p></td>
<td><p>WIA_IPA_TYMED</p>
<p>読み取り/書き込みアクセスの「注: h、i、k</p></td>
<td><p>フラット ベッド</p>
<p>注を参照してください: b</p></td>
</tr>
<tr class="odd">
<td><p>WIA_IPA_TYMED</p>
<p>読み取り/書き込みアクセスの「注: h、i</p></td>
<td><p>子/フィーダー</p>
<p>注を参照してください、。</p></td>
<td><p>WIA_IPA_TYMED</p>
<p>読み取り/書き込みアクセスの「注: h、i</p></td>
<td><p>フィーダー</p>
<p>注を参照してください、。</p></td>
</tr>
<tr class="even">
<td><p>WIA_IPA_CHANNELS_PER_PIXEL</p>
<p>読み取り専用アクセス</p></td>
<td><p>子/ベッド</p>
<p>注を参照してください: b</p></td>
<td><p>WIA_IPA_CHANNELS_PER_PIXEL</p>
<p>読み取り専用アクセス</p></td>
<td><p>フラット ベッド</p>
<p>注を参照してください: b</p></td>
</tr>
<tr class="odd">
<td><p>WIA_IPA_CHANNELS_PER_PIXEL</p>
<p>読み取り専用アクセス</p></td>
<td><p>子/フィーダー</p>
<p>注を参照してください、。</p></td>
<td><p>WIA_IPA_CHANNELS_PER_PIXEL</p>
<p>読み取り専用アクセス</p></td>
<td><p>フィーダー</p>
<p>注を参照してください、。</p></td>
</tr>
<tr class="even">
<td><p>WIA_IPA_BITS_PER_CHANNEL</p>
<p>読み取り専用アクセス</p></td>
<td><p>子/ベッド</p>
<p>注を参照してください: b</p></td>
<td><p>WIA_IPA_BITS_PER_CHANNEL</p>
<p>読み取り専用アクセス</p></td>
<td><p>フラット ベッド</p>
<p>注を参照してください: b</p></td>
</tr>
<tr class="odd">
<td><p>WIA_IPA_BITS_PER_CHANNEL</p>
<p>読み取り専用アクセス</p></td>
<td><p>子/フィーダー</p>
<p>注を参照してください、。</p></td>
<td><p>WIA_IPA_BITS_PER_CHANNEL</p>
<p>読み取り専用アクセス</p></td>
<td><p>フィーダー</p>
<p>注を参照してください、。</p></td>
</tr>
<tr class="even">
<td><p>WIA_IPA_ITEM_SIZE</p>
<p>読み取り専用アクセス</p></td>
<td><p>子/ベッド</p>
<p>注を参照してください: b</p></td>
<td><p>WIA_IPA_ITEM_SIZE</p>
<p>読み取り専用アクセス</p></td>
<td><p>フラット ベッド</p>
<p>注を参照してください: b</p></td>
</tr>
<tr class="odd">
<td><p>WIA_IPA_ITEM_SIZE</p>
<p>読み取り専用アクセス</p></td>
<td><p>子/フィーダー</p>
<p>注を参照してください、。</p></td>
<td><p>WIA_IPA_ITEM_SIZE</p>
<p>読み取り専用アクセス</p></td>
<td><p>フィーダー</p>
<p>注を参照してください、。</p></td>
</tr>
<tr class="even">
<td><p>WIA_IPA_ICM_PROFILE_NAME</p>
<p>読み取り/書き込みアクセス</p></td>
<td><p>子/ベッド</p>
<p>注を参照してください: b</p></td>
<td><p>WIA_IPA_ICM_PROFILE_NAME</p>
<p>読み取り/書き込みアクセス</p></td>
<td><p>フラット ベッド</p>
<p>注を参照してください: b</p></td>
</tr>
<tr class="odd">
<td><p>WIA_IPA_ICM_PROFILE_NAME</p>
<p>読み取り/書き込みアクセス</p></td>
<td><p>子/フィーダー</p>
<p>注を参照してください: c</p></td>
<td><p>WIA_IPA_ICM_PROFILE_NAME</p>
<p>読み取り/書き込みアクセス</p></td>
<td><p>フィーダー</p>
<p>注を参照してください、。</p></td>
</tr>
<tr class="even">
<td><p>WIA_IPA_FILENAME_EXTENSION</p>
<p>読み取り専用アクセス</p></td>
<td><p>子/ベッド</p>
<p>注を参照してください: b</p></td>
<td><p>WIA_IPA_FILENAME_EXTENSION</p>
<p>読み取り専用アクセス</p></td>
<td><p>フラット ベッド</p>
<p>注を参照してください: b</p></td>
</tr>
<tr class="odd">
<td><p>WIA_IPA_FILENAME_EXTENSION</p>
<p>読み取り専用アクセス</p></td>
<td><p>子/フィーダー</p>
<p>注を参照してください、。</p></td>
<td><p>WIA_IPA_FILENAME_EXTENSION</p>
<p>読み取り専用アクセス</p></td>
<td><p>フィーダー</p>
<p>注を参照してください、。</p></td>
</tr>
<tr class="even">
<td><p>WIA_IPA_SUPPRESS_PROPERTY_PAGE</p>
<p>読み取り専用アクセス</p></td>
<td><p>子/ベッド</p>
<p>注を参照してください: b</p></td>
<td><p>WIA_IPA_SUPPRESS_PROPERTY_PAGE</p>
<p>読み取り専用アクセス</p></td>
<td><p>フラット ベッド</p>
<p>注を参照してください: b</p></td>
</tr>
<tr class="odd">
<td><p>WIA_IPA_SUPPRESS_PROPERTY_PAGE</p>
<p>読み取り専用アクセス</p></td>
<td><p>子/フィーダー</p>
<p>注を参照してください、。</p></td>
<td><p>WIA_IPA_SUPPRESS_PROPERTY_PAGE</p>
<p>読み取り専用アクセス</p></td>
<td><p>フィーダー</p></td>
</tr>
<tr class="even">
<td><p>ジェネリックの場合:WIA_CATEGORY_ROOT</p></td>
<td><p>ルート</p>
<p>注を参照してください: c</p></td>
<td><p>WIA_IPA_ITEM_CATEGORY</p>
<p>読み取り専用アクセスの注参照: f#</p></td>
<td><p>ルート</p></td>
</tr>
<tr class="odd">
<td><p>ジェネリックの場合:WIA_CATEGORY_FLATBED</p></td>
<td><p>子/ベッド</p>
<p>注を参照してください: b</p></td>
<td><p>WIA_IPA_ITEM_CATEGORY</p>
<p>読み取り専用アクセスの注参照: f#</p></td>
<td><p>フラット ベッド</p>
<p>注を参照してください: b</p></td>
</tr>
<tr class="even">
<td><p>ジェネリックの場合:WIA_CATEGORY_FEEDER</p></td>
<td><p>子/フィーダー</p>
<p>注を参照してください、。</p></td>
<td><p>WIA_IPA_ITEM_CATEGORY</p>
<p>読み取り専用アクセスの注参照: f#</p></td>
<td><p>フィーダー</p>
<p>注を参照してください、。</p></td>
</tr>
<tr class="odd">
<td><p>WIA_DPS_DOCUMENT_HANDLING_CAPABILITIES</p>
<p>読み取り専用アクセスには、「」を参照に注意してください。 l</p></td>
<td><p>ルート</p>
<p>注を参照してください: c</p></td>
<td><p>WIA_DPS_DOCUMENT_HANDLING_CAPABILITIES</p>
<p>読み取り専用アクセスには、「」を参照に注意してください。 l</p></td>
<td><p>ルート</p>
<p>注を参照してください: c</p></td>
</tr>
<tr class="even">
<td><p>WIA_IPA_BUFFER_SIZE</p>
<p>読み取り専用アクセスには、「」を参照に注意してください。 l</p></td>
<td><p>子/ベッド</p>
<p>注を参照してください: b</p></td>
<td><p>WIA_IPA_BUFFER_SIZE</p>
<p>読み取り専用アクセスには、「」を参照に注意してください。 l</p></td>
<td><p>フラット ベッド</p>
<p>注を参照してください: b</p></td>
</tr>
<tr class="odd">
<td><p>WIA_IPA_BUFFER_SIZE</p>
<p>読み取り専用アクセスには、「」を参照に注意してください。 l</p></td>
<td><p>子/フィーダー</p>
<p>注を参照してください、。</p></td>
<td><p>WIA_IPA_BUFFER_SIZE</p>
<p>読み取り専用アクセスには、「」を参照に注意してください。 l</p></td>
<td><p>フィーダー</p>
<p>注を参照してください、。</p></td>
</tr>
<tr class="even">
<td><p>WIA_IPA_MIN_BUFFER_SIZE</p>
<p>読み取り専用アクセスには、「」を参照に注意してください。 l</p></td>
<td><p>子/ベッド</p>
<p>注を参照してください: b</p></td>
<td><p>WIA_IPA_MIN_BUFFER_SIZE</p>
<p>読み取り専用アクセスには、「」を参照に注意してください。 l</p></td>
<td><p>フラット ベッド</p>
<p>注を参照してください: b</p></td>
</tr>
<tr class="odd">
<td><p>WIA_IPA_MIN_BUFFER_SIZE</p>
<p>読み取り専用アクセスには、「」を参照に注意してください。 l</p></td>
<td><p>子/フィーダー</p>
<p>注を参照してください、。</p></td>
<td><p>WIA_IPA_MIN_BUFFER_SIZE</p>
<p>読み取り専用アクセスには、「」を参照に注意してください。 l</p></td>
<td><p>フィーダー</p>
<p>注を参照してください、。</p></td>
</tr>
<tr class="even">
<td><p>WIA_IPA_PIXELS_PER_LINE</p>
<p>読み取り専用アクセスの注参照: m</p></td>
<td><p>子/ベッド</p>
<p>注を参照してください: b</p></td>
<td><p>WIA_IPA_PIXELS_PER_LINE</p>
<p>読み取り専用アクセスの注参照: m</p></td>
<td><p>フラット ベッド</p>
<p>注を参照してください: b</p></td>
</tr>
<tr class="odd">
<td><p>WIA_IPA_PIXELS_PER_LINE</p>
<p>読み取り専用アクセスの注参照: m</p></td>
<td><p>子/フィーダー</p>
<p>注を参照してください、。</p></td>
<td><p>WIA_IPA_PIXELS_PER_LINE</p>
<p>読み取り専用アクセスの注参照: m</p></td>
<td><p>フィーダー</p>
<p>注を参照してください、。</p></td>
</tr>
<tr class="even">
<td><p>WIA_IPA_NUMBER_OF_LINES</p>
<p>読み取り専用アクセスの注参照: m</p></td>
<td><p>子/ベッド</p>
<p>注を参照してください: b</p></td>
<td><p>WIA_IPA_NUMBER_OF_LINES</p>
<p>読み取り専用アクセスの注参照: m</p></td>
<td><p>フラット ベッド</p>
<p>注を参照してください: b</p></td>
</tr>
<tr class="odd">
<td><p>WIA_IPA_NUMBER_OF_LINES</p>
<p>読み取り専用アクセスの注参照: m</p></td>
<td><p>子/フィーダー</p>
<p>注を参照してください、。</p></td>
<td><p>WIA_IPA_NUMBER_OF_LINES</p>
<p>読み取り専用アクセスの注参照: m</p></td>
<td><p>フィーダー</p>
<p>注を参照してください、。</p></td>
</tr>
<tr class="even">
<td><p>WIA_IPA_BYTES_PER_LINE</p>
<p>読み取り専用アクセスの注参照: m</p></td>
<td><p>子/ベッド</p>
<p>注を参照してください: b</p></td>
<td><p>WIA_IPA_BYTES_PER_LINE</p>
<p>読み取り専用アクセスの注参照: m</p></td>
<td><p>フラット ベッド</p>
<p>注を参照してください: b</p></td>
</tr>
<tr class="odd">
<td><p>WIA_IPA_BYTES_PER_LINE</p>
<p>読み取り専用アクセスの注参照: m</p></td>
<td><p>子/フィーダー</p>
<p>注を参照してください、。</p></td>
<td><p>WIA_IPA_BYTES_PER_LINE</p>
<p>読み取り専用アクセスの注参照: m</p></td>
<td><p>フィーダー</p>
<p>注を参照してください、。</p></td>
</tr>
<tr class="even">
<td><p>WIA_IPA_PLANAR</p>
<p>読み取り専用アクセス</p></td>
<td><p>子/ベッド</p>
<p>注を参照してください: b</p></td>
<td><p>WIA_IPA_PLANAR</p>
<p>読み取り専用アクセス</p></td>
<td><p>フラット ベッド</p>
<p>注を参照してください: b</p></td>
</tr>
<tr class="odd">
<td><p>WIA_IPA_PLANAR</p>
<p>読み取り専用アクセス</p></td>
<td><p>子/フィーダー</p>
<p>注を参照してください、。</p></td>
<td><p>WIA_IPA_PLANAR</p>
<p>読み取り専用アクセス</p></td>
<td><p>フィーダー</p>
<p>注を参照してください、。</p></td>
</tr>
<tr class="even">
<td><p>WIA_DPS_MAX_SCAN_TIME</p>
<p>読み取り専用アクセス</p></td>
<td><p>ルート</p>
<p>注を参照してください: c</p></td>
<td><p>WIA_DPS_MAX_SCAN_TIME</p>
<p>読み取り専用アクセス</p></td>
<td><p>ルート</p>
<p>注を参照してください: c</p></td>
</tr>
</tbody>
</table>

 

<a href="" id="note-a-"></a>A: に注意してください。  
フィーダー項目 (ADF) または Windows XP のルートまたは子項目にフィーダー コンテキスト (WIA\_DPS\_ドキュメント\_処理\_選択は、フィーダーに設定されます)。

<a href="" id="note-b-"></a>B: に注意してください。  
フラット ベッド項目または Windows XP のルートまたは子項目のフラット ベッド コンテキスト (WIA\_DPS\_ドキュメント\_処理\_選択は、フラット ベッドに設定されます)。

<a href="" id="note-c-"></a>C: に注意してください。  
ルート アイテム、コンテキストなしで Windows XP を指定します。

<a href="" id="note-d-"></a>D: に注意してください。  
WIA サービスによって管理されます。

<a href="" id="note-e-"></a>E: に注意してください。  
アプリケーションのアプリケーション項目ツリー (A AIT) 用にカスタマイズします。

<a href="" id="note-f-"></a>F: に注意してください。  
ドライバーのアプリケーション項目ツリー (D AIT) ではサポートされていない場合でも、待ち時間を追加します。 設定**WiaImgFmt\_BMP**します。

<a href="" id="note-g-"></a>G: に注意してください。  
Windows Vista Windows XP への変換からでは、追加**WiaImgFmt\_MEMORYBMP**で使用する[TYMED\_コールバック](understanding-tymed.md)します。

<a href="" id="note-h-"></a>注: %m:  
Windows Vista Windows XP への変換からでは、追加 TYMED\_コールバックと**WiaImgFmt\_MEMORYBMP**します。 Windows xp、Windows Vista の翻訳だけ[TYMED\_ファイル](understanding-tymed.md)と TYMED\_マルチページ\_ファイルが変換されます。

<a href="" id="note-i-"></a>操作に注意してください。  
Windows xp Windows Vista への変換からの場合にのみ変換します。

TYMED\_ファイル

TYMED\_マルチページ\_ファイル

J: に注意してください。Windows xp Windows Vista への変換からの場合にのみ変換します。

DUP

フィード

フラット

検出\_フィード

検出\_フラット

検出\_スキャン

注 k:D AIT でサポートされていない場合でも、待ち時間を追加します。 TYMED に設定\_ファイル。

L: に注意してください。D AIT でサポートされていない場合でも、待ち時間を追加します。

M: に注意してください。すべての転送が有効なデバイスの Windows Vista の省略可能です。 これらのプロパティが実装されている場合、レガシ アプリケーションは、1 行、スキャン ライン、および画像のスキャン ラインの合計数ごとに必要なバイト数のピクセルの数の概数を取得できます。 イメージ処理のフィルターがこれらのプロパティが表す実際の値を変更するため、これらの値は正確ではありません。

これらのプロパティは、Windows Vista ドライバーによって指定されていない場合、WIA サービスで互換レイヤーはこれらのプロパティを追加します。 WIA サービスによっては、これらのプロパティが追加される、プロパティを使用してそれらが更新されます。WIA\_IPA\_深さ、WIA\_IP\_XEXTENT、および WIA\_IP\_YEXTENT します。

**注**  可能であれば、アプリケーションのイメージの正確な情報を取得するイメージ ヘッダー データに常に解析する必要があります。 正確ではないためこのプロパティに依存する必要があります。

 

 

 





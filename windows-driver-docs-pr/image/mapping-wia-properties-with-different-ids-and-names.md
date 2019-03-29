---
title: 異なる ID と名前を持つ WIA プロパティのマッピング
description: 異なる ID と名前を持つ WIA プロパティのマッピング
ms.assetid: e3a352fc-c817-466e-bd04-0ec8b029d500
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a6373f74f0fb71a04845a2d73678bc10935f8106
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56574352"
---
# <a name="mapping-wia-properties-with-different-ids-and-names"></a>異なる ID と名前を持つ WIA プロパティのマッピング


さまざまなプロパティの Id と Windows Vista の対応するさまざまなプロパティ名を持つ Windows XP プロパティがあります。 これらの Windows XP ルート プロパティと Windows vista に変換されるフラット ベッドとフィーダー (ADF) のプロパティのテーブルは、次のとおりです。

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
<p><strong>item/context</strong></p></td>
<td><p><strong>Windows Vista のプロパティ</strong></p></td>
<td><p><strong>Windows Vista</strong> <strong>項目</strong></p></td>
</tr>
<tr class="even">
<td><p>WIA_DPS_HORIZONTAL_BED_SIZE</p>
<p>読み取り専用アクセス</p></td>
<td><p>ルート</p>
<p>注を参照してください、。</p></td>
<td><p>WIA_IPS_MAX_HORIZONTAL_SIZE</p>
<p>読み取り専用アクセス</p></td>
<td><p>フラット ベッド</p>
<p>注を参照してください: b</p></td>
</tr>
<tr class="odd">
<td><p>WIA_DPS_VERTICAL_BED_SIZE</p>
<p>読み取り専用アクセス</p></td>
<td><p>ルート</p>
<p>注を参照してください、。</p></td>
<td><p>WIA_IPS_MAX_VERTICAL_SIZE</p>
<p>読み取り専用アクセス</p></td>
<td><p>フラット ベッド</p>
<p>注を参照してください: b</p></td>
</tr>
<tr class="even">
<td><p>WIA_DPS_HORIZONTAL_SHEET_FEED_SIZE</p>
<p>読み取り専用アクセス</p></td>
<td><p>ルート</p>
<p>注を参照してください、。</p></td>
<td><p>WIA_IPS_MAX_HORIZONTAL_SIZE</p>
<p>読み取り専用アクセス</p></td>
<td><p>フィーダー</p>
<p>注を参照してください: c</p></td>
</tr>
<tr class="odd">
<td><p>WIA_DPS_VERTICAL_SHEET_FEED_SIZE</p>
<p>読み取り専用アクセス</p></td>
<td><p>ルート</p>
<p>注を参照してください、。</p></td>
<td><p>WIA_IPS_MAX_HORIZONTAL_SIZE</p>
<p>読み取り専用アクセス</p></td>
<td><p>フィーダー</p>
<p>注を参照してください: c</p></td>
</tr>
<tr class="even">
<td><p>WIA_DPS_MIN_HORIZONTAL_SHEET_FEED_SIZE</p>
<p>読み取り専用アクセス</p></td>
<td><p>ルート</p>
<p>注を参照してください、。</p></td>
<td><p>WIA_IPS_MIN_HORIZONTAL_SIZE</p>
<p>読み取り専用アクセス</p></td>
<td><p>フィーダー</p>
<p>注を参照してください: c</p></td>
</tr>
<tr class="odd">
<td><p>WIA_DPS_MIN_VERTICAL_SHEET_FEED_SIZE</p>
<p>読み取り専用アクセス</p></td>
<td><p>ルート</p>
<p>注を参照してください、。</p></td>
<td><p>WIA_IPS_MIN_VERTICAL_SIZE</p>
<p>読み取り専用アクセス</p></td>
<td><p>フィーダー</p>
<p>注を参照してください: c</p></td>
</tr>
<tr class="even">
<td><p>ジェネリックな値:1</p></td>
<td><p>該当なし</p></td>
<td><p>WIA_IPS_MIN_HORIZONTAL_SIZE</p>
<p>読み取り専用アクセス</p></td>
<td><p>フラット ベッド</p>
<p>注を参照してください: c</p></td>
</tr>
<tr class="odd">
<td><p>ジェネリックな値:1</p></td>
<td><p>該当なし</p></td>
<td><p>WIA_IPS_MIN_VERTICAL_SIZE</p>
<p>読み取り専用アクセス</p></td>
<td><p>フラット ベッド</p>
<p>注を参照してください: c</p></td>
</tr>
</tbody>
</table>

 

<a href="" id="note-a-"></a>A: に注意してください。  
ルート アイテム、コンテキストなしで Windows XP の指定

<a href="" id="note-b-"></a>B: に注意してください。  
フラット ベッド項目または Windows XP のルートまたは子項目のフラット ベッド コンテキスト (WIA\_DPS\_ドキュメント\_処理\_ベッドに選択が設定されている)

<a href="" id="note-c-"></a>C: に注意してください。  
フィーダー項目 (ADF) または Windows XP のルートまたは子項目にフィーダー コンテキスト (WIA\_DPS\_ドキュメント\_処理\_フィーダーに選択が設定されている)

 

 





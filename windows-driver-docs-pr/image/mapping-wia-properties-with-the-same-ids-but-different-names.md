---
title: 同じ ID で異なる名前を持つ WIA プロパティのマッピング
description: 同じ ID で異なる名前を持つ WIA プロパティのマッピング
ms.assetid: 0321db59-74a1-4294-bbaf-ec0b9317464b
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 12b5e4b21bc58c97c2e04130ceb3181e6f0719f1
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63380360"
---
# <a name="mapping-wia-properties-with-the-same-ids-but-different-names"></a>同じ ID で異なる名前を持つ WIA プロパティのマッピング


Windows Vista 対応よりもさまざまなプロパティ名が同じプロパティ Id を持つ Windows XP プロパティがあります。 これらの Windows XP ルート プロパティと Windows vista に変換されるフラット ベッドとフィーダー (ADF) のプロパティのテーブルは、次のとおりです。

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
<td><p><strong>Windows Vista</strong> <strong>項目</strong></p></td>
</tr>
<tr class="even">
<td><p>WIA_DPS_DOCUMENT_HANDLING_SELECT</p>
<p>読み取り/書き込みアクセスの「注: d</p></td>
<td><p>ルート</p>
<p>注を参照してください: c</p></td>
<td><p>WIA_IPS_DOCUMENT_HANDLING_SELECT</p>
<p>読み取り/書き込みアクセスの「注: d</p></td>
<td><p>フィーダー</p>
<p>注を参照してください、。</p></td>
</tr>
<tr class="odd">
<td><p>WIA_DPS_SHEET_FEEDER_REGISTRATION</p>
<p>読み取り専用アクセス</p></td>
<td><p>ルート/フィーダー</p>
<p>注を参照してください、。</p></td>
<td><p>WIA_IPS_SHEET_FEEDER_REGISTRATION</p>
<p>読み取り専用アクセス</p></td>
<td><p>フィーダー</p>
<p>注を参照してください、。</p></td>
</tr>
<tr class="even">
<td><p>WIA_DPS_OPTICAL_XRES</p>
<p>読み取り専用アクセス</p></td>
<td><p>ルート/ベッド</p>
<p>注を参照してください: b</p></td>
<td><p>WIA_IPS_OPTICAL_XRES</p>
<p>読み取り専用アクセス</p></td>
<td><p>フラット ベッド</p>
<p>注を参照してください: b</p></td>
</tr>
<tr class="odd">
<td><p>WIA_DPS_OPTICAL_XRES</p>
<p>読み取り専用アクセス</p></td>
<td><p>ルート/フィーダー</p>
<p>注を参照してください、。</p></td>
<td><p>WIA_IPS_OPTICAL_XRES</p>
<p>読み取り専用アクセス</p></td>
<td><p>フィーダー</p>
<p>注を参照してください、。</p></td>
</tr>
<tr class="even">
<td><p>WIA_DPS_OPTICAL_YRES</p>
<p>読み取り専用アクセス</p></td>
<td><p>ルート/ベッド</p>
<p>注を参照してください: b</p></td>
<td><p>WIA_IPS_OPTICAL_YRES</p>
<p>読み取り専用アクセス</p></td>
<td><p>フラット ベッド</p>
<p>注を参照してください: b</p></td>
</tr>
<tr class="odd">
<td><p>WIA_DPS_OPTICAL_YRES</p>
<p>読み取り専用アクセス</p></td>
<td><p>ルート/フィーダー</p>
<p>注を参照してください、。</p></td>
<td><p>WIA_IPS_OPTICAL_YRES</p>
<p>読み取り専用アクセス</p></td>
<td><p>フィーダー</p>
<p>注を参照してください、。</p></td>
</tr>
<tr class="even">
<td><p>WIA_DPS_PAGES</p>
<p>読み取り/書き込みアクセス</p></td>
<td><p>ルート/フィーダー</p>
<p>注を参照してください、。</p></td>
<td><p>WIA_IPS_PAGES</p>
<p>読み取り/書き込みアクセス</p></td>
<td><p>フィーダー</p>
<p>注を参照してください、。</p></td>
</tr>
<tr class="odd">
<td><p>WIA_DPS_PAGE_SIZE</p>
<p>読み取り/書き込みアクセスに注意してください。: e を参照してください。</p></td>
<td><p>ルート/フィーダー</p>
<p>注を参照してください、。</p></td>
<td><p>WIA_IPS_PAGE_SIZE</p>
<p>読み取り/書き込みアクセスに注意してください。: e を参照してください。</p></td>
<td><p>フィーダー</p>
<p>注を参照してください、。</p></td>
</tr>
<tr class="even">
<td><p>WIA_DPS_PAGE_WIDTH</p>
<p>読み取り専用アクセス</p></td>
<td><p>ルート/フィーダー</p>
<p>注を参照してください、。</p></td>
<td><p>WIA_IPS_PAGE_WIDTH</p>
<p>読み取り専用アクセス</p></td>
<td><p>フィーダー</p>
<p>注を参照してください、。</p></td>
</tr>
<tr class="odd">
<td><p>WIA_DPS_PAGE_HEIGHT</p>
<p>読み取り専用アクセス</p></td>
<td><p>ルート/フィーダー</p>
<p>注を参照してください、。</p></td>
<td><p>WIA_IPS_PAGE_WIDTH</p>
<p>読み取り専用アクセス</p></td>
<td><p>フィーダー</p>
<p>注を参照してください、。</p></td>
</tr>
<tr class="even">
<td><p>WIA_DPS_PREVIEW</p>
<p>読み取り/書き込みアクセス</p></td>
<td><p>ルート/ベッド</p>
<p>注を参照してください: b</p></td>
<td><p>WIA_IPS_PREVIEW</p>
<p>読み取り専用アクセス</p></td>
<td><p>フラット ベッド</p>
<p>注を参照してください: b</p></td>
</tr>
<tr class="odd">
<td><p>WIA_DPS_PREVIEW</p>
<p>読み取り/書き込みアクセス</p></td>
<td><p>ルート/フィーダー</p>
<p>注を参照してください、。</p></td>
<td><p>WIA_IPS_PREVIEW</p>
<p>読み取り/書き込みアクセス</p></td>
<td><p>フィーダー</p>
<p>注を参照してください、。</p></td>
</tr>
<tr class="even">
<td><p>WIA_DPS_SHOW_PREVIEW_CONTROL</p>
<p>読み取り専用アクセス</p></td>
<td><p>ルート/ベッド</p>
<p>注を参照してください: c</p></td>
<td><p>WIA_IPS_SHOW_PREVIEW_CONTROL</p>
<p>読み取り専用アクセス</p></td>
<td><p>フラット ベッド</p>
<p>注を参照してください: c</p></td>
</tr>
<tr class="odd">
<td><p>WIA_DPS_SHOW_PREVIEW_CONTROL</p>
<p>読み取り専用アクセス</p></td>
<td><p>ルート/フィーダー</p>
<p>注を参照してください、。</p></td>
<td><p>WIA_IPS_SHOW_PREVIEW_CONTROL</p>
<p>読み取り専用アクセス</p></td>
<td><p>フィーダー</p>
<p>注を参照してください、。</p></td>
</tr>
</tbody>
</table>

 

<a href="" id="note-a-"></a>A: に注意してください。  
フィーダー項目 (ADF) または Windows XP のルートまたは子項目にフィーダー コンテキスト (WIA\_DPS\_ドキュメント\_処理\_フィーダーに選択が設定されている)

<a href="" id="note-b-"></a>B: に注意してください。  
フラット ベッド項目または Windows XP のルートまたは子項目のフラット ベッド コンテキスト (WIA\_DPS\_ドキュメント\_処理\_ベッドに選択が設定されている)

<a href="" id="note-c-"></a>C: に注意してください。  
ルート アイテム、コンテキストなしで Windows XP の指定

<a href="" id="note-d-"></a>D: に注意してください。  
Windows xp から Windows Vista への変換のみの場合。

戻る\_最初

戻る\_のみ

双方向

フロント\_最初

フロント\_のみ

フロント\_既定値はこのプロパティが実装されていない場合のみです。

E: に注意してください。従来のものだけでなく、すべての値を変換 (WIA\_ページ\_カスタム、WIA\_ページ\_A4、WIA\_ページ\_文字)

適切なフラット ベッド/フィーダー コンテキストのセットに Windows XP のルート項目を構成する必要がありますに注意してください (WIA を通じて\_DPS\_ドキュメント\_処理\_選択) (両方のコンテキストに依存するプロパティにアクセスする前に読み取りおよび書き込みアクセス)。

 

 





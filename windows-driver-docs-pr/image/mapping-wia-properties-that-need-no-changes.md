---
title: WIA プロパティの割り当てを変更する必要はありません。
description: WIA プロパティの割り当てを変更する必要はありません。
ms.assetid: ceb0fe83-9803-4ba5-9a9f-7c722389db0b
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 319052c912bc371b7742a1b88e0a91b9e8022621
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56539274"
---
# <a name="mapping-wia-properties-that-need-no-changes"></a>WIA プロパティの割り当てを変更する必要はありません。


同じプロパティの Id と Windows Vista 対応としてプロパティ名を持つ Windows XP プロパティがあります。 適切な Windows XP のコンテキストを選択した場合だけです。 これらのプロパティが変換されます。その他の変更はありません。 これらの Windows XP ルート プロパティと Windows vista に変換されるフラット ベッドとフィーダー (ADF) のプロパティのテーブルは、次のとおりです。

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
<td><p><strong>Windows XP 項目/コンテキスト</strong></p></td>
<td><p><strong>Windows Vista のプロパティ</strong></p></td>
<td><p><strong>Windows Vista</strong> <strong>項目</strong></p></td>
</tr>
<tr class="even">
<td><p>WIA_IPS_CUR_INTENT</p>
<p>読み取り/書き込みアクセス</p></td>
<td><p>子/ベッド</p>
<p>注を参照してください: b</p></td>
<td><p>WIA_IPS_CUR_INTENT</p>
<p>読み取り/書き込みアクセス</p></td>
<td><p>フラット ベッド</p>
<p>注を参照してください: b</p></td>
</tr>
<tr class="odd">
<td><p>WIA_IPS_CUR_INTENT</p>
<p>読み取り/書き込みアクセス</p></td>
<td><p>子/フィーダー</p>
<p>注を参照してください、。</p></td>
<td><p>WIA_IPS_CUR_INTENT</p>
<p>読み取り/書き込みアクセス</p></td>
<td><p>フィーダー</p>
<p>注を参照してください、。</p></td>
</tr>
<tr class="even">
<td><p>WIA_IPS_XRES</p>
<p>読み取り/書き込みアクセス</p></td>
<td><p>子/ベッド</p>
<p>注を参照してください: b</p></td>
<td><p>WIA_IPS_XRES</p>
<p>読み取り/書き込みアクセス</p></td>
<td><p>フラット ベッド</p>
<p>注を参照してください: b</p></td>
</tr>
<tr class="odd">
<td><p>WIA_IPS_XRES</p>
<p>読み取り/書き込みアクセス</p></td>
<td><p>子/フィーダー</p>
<p>注を参照してください、。</p></td>
<td><p>WIA_IPS_XRES</p>
<p>読み取り/書き込みアクセス</p></td>
<td><p>フィーダー</p>
<p>注を参照してください、。</p></td>
</tr>
<tr class="even">
<td><p>WIA_IPS_YRES</p>
<p>読み取り/書き込みアクセス</p></td>
<td><p>子/ベッド</p>
<p>注を参照してください: b</p></td>
<td><p>WIA_IPS_YRES</p>
<p>読み取り/書き込みアクセス</p></td>
<td><p>フラット ベッド</p>
<p>注を参照してください: b</p></td>
</tr>
<tr class="odd">
<td><p>WIA_IPS_YRES</p>
<p>読み取り/書き込みアクセス</p></td>
<td><p>子/フィーダー</p>
<p>注を参照してください、。</p></td>
<td><p>WIA_IPS_YRES</p>
<p>読み取り/書き込みアクセス</p></td>
<td><p>フィーダー</p>
<p>注を参照してください、。</p></td>
</tr>
<tr class="even">
<td><p>WIA_IPS_XPOS</p>
<p>読み取り/書き込みアクセス</p></td>
<td><p>子/ベッド</p>
<p>注を参照してください: b</p></td>
<td><p>WIA_IPS_XPOS</p>
<p>読み取り/書き込みアクセス</p></td>
<td><p>フラット ベッド</p>
<p>注を参照してください: b</p></td>
</tr>
<tr class="odd">
<td><p>WIA_IPS_XPOS</p>
<p>読み取り/書き込みアクセス</p></td>
<td><p>子/フィーダー</p>
<p>注を参照してください、。</p></td>
<td><p>WIA_IPS_XPOS</p>
<p>読み取り/書き込みアクセス</p></td>
<td><p>フィーダー</p>
<p>注を参照してください、。</p></td>
</tr>
<tr class="even">
<td><p>WIA_IPS_YPOS</p>
<p>読み取り/書き込みアクセス</p></td>
<td><p>子/ベッド</p>
<p>注を参照してください: b</p></td>
<td><p>WIA_IPS_YPOS</p>
<p>読み取り/書き込みアクセス</p></td>
<td><p>フラット ベッド</p>
<p>注を参照してください: b</p></td>
</tr>
<tr class="odd">
<td><p>WIA_IPS_YPOS</p>
<p>読み取り/書き込みアクセス</p></td>
<td><p>子/フィーダー</p>
<p>注を参照してください、。</p></td>
<td><p>WIA_IPS_YPOS</p>
<p>読み取り/書き込みアクセス</p></td>
<td><p>フィーダー</p>
<p>注を参照してください、。</p></td>
</tr>
<tr class="even">
<td><p>WIA_IPS_XEXTENT</p>
<p>読み取り/書き込みアクセス</p></td>
<td><p>子/ベッド</p>
<p>注を参照してください: b</p></td>
<td><p>WIA_IPS_XEXTENT</p>
<p>読み取り/書き込みアクセス</p></td>
<td><p>フラット ベッド</p>
<p>注を参照してください: b</p></td>
</tr>
<tr class="odd">
<td><p>WIA_IPS_XEXTENT</p>
<p>読み取り/書き込みアクセス</p></td>
<td><p>子/フィーダー</p>
<p>注を参照してください、。</p></td>
<td><p>WIA_IPS_XEXTENT</p>
<p>読み取り/書き込みアクセス</p></td>
<td><p>フィーダー</p>
<p>注を参照してください、。</p></td>
</tr>
<tr class="even">
<td><p>WIA_IPS_YEXTENT</p>
<p>読み取り/書き込みアクセス</p></td>
<td><p>子/ベッド</p>
<p>注を参照してください: b</p></td>
<td><p>WIA_IPS_YEXTENT</p>
<p>読み取り/書き込みアクセス</p></td>
<td><p>フラット ベッド</p>
<p>注を参照してください: b</p></td>
</tr>
<tr class="odd">
<td><p>WIA_IPS_YEXTENT</p>
<p>読み取り/書き込みアクセス</p></td>
<td><p>子/フィーダー</p>
<p>注を参照してください、。</p></td>
<td><p>WIA_IPS_YEXTENT</p>
<p>読み取り/書き込みアクセス</p></td>
<td><p>フィーダー</p>
<p>注を参照してください、。</p></td>
</tr>
<tr class="even">
<td><p>WIA_IPS_PHOTOMETRIC_INTERP</p>
<p>読み取り/書き込みアクセス</p></td>
<td><p>子/ベッド</p>
<p>注を参照してください: b</p></td>
<td><p>WIA_IPS_PHOTOMETRIC_INTERP</p>
<p>読み取り/書き込みアクセス</p></td>
<td><p>フラット ベッド</p>
<p>注を参照してください: b</p></td>
</tr>
<tr class="odd">
<td><p>WIA_IPS_PHOTOMETRIC_INTERP</p>
<p>読み取り/書き込みアクセス</p></td>
<td><p>子/フィーダー</p>
<p>注を参照してください、。</p></td>
<td><p>WIA_IPS_PHOTOMETRIC_INTERP</p>
<p>読み取り/書き込みアクセス</p></td>
<td><p>フィーダー</p>
<p>注を参照してください、。</p></td>
</tr>
<tr class="even">
<td><p>WIA_IPS_BRIGHTNESS</p>
<p>読み取り/書き込みアクセス</p></td>
<td><p>子/ベッド</p>
<p>注を参照してください: b</p></td>
<td><p>WIA_IPS_BRIGHTNESS</p>
<p>読み取り/書き込みアクセス</p></td>
<td><p>フラット ベッド</p>
<p>注を参照してください: b</p></td>
</tr>
<tr class="odd">
<td><p>WIA_IPS_BRIGHTNESS</p>
<p>読み取り/書き込みアクセス</p></td>
<td><p>子/フィーダー</p>
<p>注を参照してください、。</p></td>
<td><p>WIA_IPS_BRIGHTNESS</p>
<p>読み取り/書き込みアクセス</p></td>
<td><p>フィーダー</p>
<p>注を参照してください、。</p></td>
</tr>
<tr class="even">
<td><p>WIA_IPS_CONTRAST</p>
<p>読み取り/書き込みアクセス</p></td>
<td><p>子/ベッド</p>
<p>注を参照してください: b</p></td>
<td><p>WIA_IPS_CONTRAST</p>
<p>読み取り/書き込みアクセス</p></td>
<td><p>フラット ベッド</p>
<p>注を参照してください: b</p></td>
</tr>
<tr class="odd">
<td><p>WIA_IPS_CONTRAST</p>
<p>読み取り/書き込みアクセス</p></td>
<td><p>子/フィーダー</p>
<p>注を参照してください、。</p></td>
<td><p>WIA_IPS_CONTRAST</p>
<p>読み取り/書き込みアクセス</p></td>
<td><p>フィーダー</p>
<p>注を参照してください、。</p></td>
</tr>
<tr class="even">
<td><p>WIA_IPS_ORIENTATION</p>
<p>読み取り/書き込みアクセス</p></td>
<td><p>子/ベッド</p>
<p>注を参照してください: b</p></td>
<td><p>WIA_IPS_ORIENTATION</p>
<p>読み取り/書き込みアクセス</p></td>
<td><p>フラット ベッド</p>
<p>注を参照してください: b</p></td>
</tr>
<tr class="odd">
<td><p>WIA_IPS_ORIENTATION</p>
<p>読み取り/書き込みアクセス</p></td>
<td><p>子/フィーダー</p>
<p>注を参照してください、。</p></td>
<td><p>WIA_IPS_ORIENTATION</p>
<p>読み取り/書き込みアクセス</p></td>
<td><p>フィーダー</p>
<p>注を参照してください、。</p></td>
</tr>
<tr class="even">
<td><p>WIA_IPS_ROTATION</p>
<p>読み取り/書き込みアクセス</p></td>
<td><p>子/ベッド</p>
<p>注を参照してください: b</p></td>
<td><p>WIA_IPS_ROTATION</p>
<p>読み取り/書き込みアクセス</p></td>
<td><p>フラット ベッド</p>
<p>注を参照してください: b</p></td>
</tr>
<tr class="odd">
<td><p>WIA_IPS_ROTATION</p>
<p>読み取り/書き込みアクセス</p></td>
<td><p>子/フィーダー</p>
<p>注を参照してください、。</p></td>
<td><p>WIA_IPS_ROTATION</p>
<p>読み取り/書き込みアクセス</p></td>
<td><p>フィーダー</p>
<p>注を参照してください、。</p></td>
</tr>
<tr class="even">
<td><p>WIA_IPS_THRESHOLD</p>
<p>読み取り/書き込みアクセス</p></td>
<td><p>子/ベッド</p>
<p>注を参照してください: b</p></td>
<td><p>WIA_IPS_THRESHOLD</p>
<p>読み取り/書き込みアクセス</p></td>
<td><p>フラット ベッド</p>
<p>注を参照してください: b</p></td>
</tr>
<tr class="odd">
<td><p>WIA_IPS_THRESHOLD</p>
<p>読み取り/書き込みアクセス</p></td>
<td><p>子/フィーダー</p>
<p>注を参照してください、。</p></td>
<td><p>WIA_IPS_THRESHOLD</p>
<p>読み取り/書き込みアクセス</p></td>
<td><p>フィーダー</p>
<p>注を参照してください、。</p></td>
</tr>
<tr class="even">
<td><p>WIA_IPS_WARM_UP_TIME</p>
<p>読み取り専用アクセス</p></td>
<td><p>子/ベッド</p>
<p>注を参照してください: b</p></td>
<td><p>WIA_IPS_WARM_UP_TIME</p>
<p>読み取り専用アクセス</p></td>
<td><p>フラット ベッド</p>
<p>注を参照してください: b</p></td>
</tr>
<tr class="odd">
<td><p>WIA_IPS_WARM_UP_TIME</p>
<p>読み取り専用アクセス</p></td>
<td><p>子/フィーダー</p>
<p>注を参照してください、。</p></td>
<td><p>WIA_IPS_WARM_UP_TIME</p>
<p>読み取り専用アクセス</p></td>
<td><p>フィーダー</p>
<p>注を参照してください、。</p></td>
</tr>
</tbody>
</table>

 

<a href="" id="note-a-"></a>A: に注意してください。  
フィーダー項目 (ADF) または Windows XP のルートまたは子項目にフィーダー コンテキスト (WIA\_DPS\_ドキュメント\_処理\_選択は、フィーダーに設定されます)。

<a href="" id="note-b-"></a>B: に注意してください。  
フラット ベッド項目または Windows XP のルートまたは子項目のフラット ベッド コンテキスト (WIA\_DPS\_ドキュメント\_処理\_選択は、フラット ベッドに設定されます)。

 

 





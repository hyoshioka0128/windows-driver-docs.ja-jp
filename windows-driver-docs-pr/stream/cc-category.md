---
title: CC カテゴリ
description: CC カテゴリ
ms.assetid: 742955f3-85a2-4627-b1b1-0bd85cdb1e77
keywords:
- ストリームのカテゴリ WDK ビデオ キャプチャ、クローズド キャプションのカテゴリ
- '[Cc] カテゴリの WDK ビデオ キャプチャ'
- PINNAME_VIDEO_CC
- クローズド キャプション カテゴリ WDK ビデオのキャプチャ
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7b558e688982bfaf11b975d7a324b97deb5f1729
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56578970"
---
# <a name="cc-category"></a>CC カテゴリ


次の GUID は、クローズド キャプション (CC) カテゴリに対応します。

-   **PINNAME\_ビデオ\_CC**

    [Cc] カテゴリの出力ピンは、1、21 行目のフィールドのペアをクローズド キャプションのデコードされたバイトのストリームを提供します。

指定するときに**PINNAME\_ビデオ\_CC**ピンを使用して、次の表の情報。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>属性</th>
<th>値</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>DataRange 構造体</strong></p></td>
<td><p>KS_DATARANGE</p></td>
</tr>
<tr class="even">
<td><p><strong>DataFormat 構造体</strong></p></td>
<td><p>KS_DATAFORMAT</p></td>
</tr>
<tr class="odd">
<td><p><strong>主な形式の GUID</strong></p></td>
<td><p>KSDATAFORMAT_TYPE_AUXLine21Data</p></td>
</tr>
<tr class="even">
<td><p><strong>サブ GUID を書式設定します。</strong></p></td>
<td><p>KSDATAFORMAT_SUBTYPE_Line21_BytePair</p></td>
</tr>
<tr class="odd">
<td><p><strong>GUID を指定子</strong></p></td>
<td><p>KSDATAFORMAT_SPECIFIER_NONE</p></td>
</tr>
<tr class="even">
<td><p><strong>拡張のヘッダーのサイズ</strong></p></td>
<td><p>0</p></td>
</tr>
<tr class="odd">
<td><p><strong>必要なプロパティ セット</strong></p></td>
<td><p>なし</p></td>
</tr>
<tr class="even">
<td><p><strong>必要なイベントのセット</strong></p></td>
<td><p>なし</p></td>
</tr>
<tr class="odd">
<td><p><strong>DirectShow majortype</strong></p></td>
<td><p>なし</p></td>
</tr>
<tr class="even">
<td><p><strong>DirectShow formattype</strong></p></td>
<td><p>なし</p></td>
</tr>
</tbody>
</table>

 

 

 





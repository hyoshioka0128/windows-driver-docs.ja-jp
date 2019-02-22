---
title: 文字放送のカテゴリ
description: 文字放送のカテゴリ
ms.assetid: f8eb289f-0b01-43cc-8160-f16dc6de12d9
keywords:
- ストリームのカテゴリの WDK ビデオ キャプチャ、文字放送
- 文字放送のカテゴリ WDK ビデオのキャプチャします。
- PINNAME_VIDEO_TELETEXT
- 世界標準の文字放送データ WDK ビデオ キャプチャ
- WST データ WDK ビデオのキャプチャします。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 55644df80bb964d4fb4d9094ccb042ae61cb0b9e
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56560646"
---
# <a name="teletext-category"></a>文字放送のカテゴリ


次の GUID は、文字放送のカテゴリに対応します。

-   **PINNAME\_ビデオ\_文字放送**

    文字放送のカテゴリの出力ピンは、デコードされた世界標準文字放送 (WST) データのストリームを提供します。

指定するときに**PINNAME\_ビデオ\_文字放送**ピンを使用して、次の表の情報。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>属性</th>
<th>Value</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>DataRange 構造体</strong></p></td>
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff567631" data-raw-source="[&lt;strong&gt;KS_DATARANGE_VIDEO_VBI&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff567631)"><strong>KS_DATARANGE_VIDEO_VBI</strong></a></p></td>
</tr>
<tr class="even">
<td><p><strong>DataFormat 構造体</strong></p></td>
<td><p>KS_DATAFORMAT_VIDEO_VBI</p></td>
</tr>
<tr class="odd">
<td><p><strong>主な形式の GUID</strong></p></td>
<td><p>KS_DATAFORMAT_TYPE_VBI</p></td>
</tr>
<tr class="even">
<td><p><strong>GUID を subFormat します。</strong></p></td>
<td><p>KSDATAFORMAT_SUBTYPE_TELETEXT</p></td>
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
<td><p>MEDIATYPE_VBI</p></td>
</tr>
<tr class="even">
<td><p><strong>DirectShow formattype</strong></p></td>
<td><p>FORMAT_VBI</p></td>
</tr>
</tbody>
</table>

 

 

 





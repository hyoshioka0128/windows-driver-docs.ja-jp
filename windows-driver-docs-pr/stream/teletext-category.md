---
title: テレテキスト カテゴリ
description: テレテキスト カテゴリ
ms.assetid: f8eb289f-0b01-43cc-8160-f16dc6de12d9
keywords:
- ストリームのカテゴリの WDK ビデオ キャプチャ、文字放送
- 文字放送のカテゴリ WDK ビデオのキャプチャします。
- PINNAME_VIDEO_TELETEXT
- 世界標準の文字放送データ WDK ビデオ キャプチャ
- WST データ WDK ビデオのキャプチャします。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e73268dafd6330ae10210329c9f83f5409320ad8
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67377739"
---
# <a name="teletext-category"></a>テレテキスト カテゴリ


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
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-tagks_datarange_video_vbi" data-raw-source="[&lt;strong&gt;KS_DATARANGE_VIDEO_VBI&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-tagks_datarange_video_vbi)"><strong>KS_DATARANGE_VIDEO_VBI</strong></a></p></td>
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

 

 

 





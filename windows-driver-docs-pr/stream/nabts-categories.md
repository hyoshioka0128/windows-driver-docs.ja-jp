---
title: NABTS カテゴリ
description: NABTS カテゴリ
ms.assetid: 7d064ed4-1bd9-4457-83c8-8b1fee10251c
keywords:
- カテゴリの WDK ビデオのキャプチャ、NABTS をストリーム配信します。
- PINNAME_VIDEO_NABTS
- North American ブロードキャスト文字放送標準 WDK ビデオのキャプチャ
- NABTS WDK ビデオのキャプチャ
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 70ab8fb0b906e12c40432a1128e2a257cb008720
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56530822"
---
# <a name="nabts-categories"></a>NABTS カテゴリ


次の GUID は、North American ブロードキャスト文字放送標準 (NABTS) カテゴリに対応します。

-   **PINNAME\_ビデオ\_NABTS**

    North American ブロードキャスト文字放送標準 (NABTS) カテゴリの出力ピンは、生のデコードされたストリームまたは転送エラー訂正 (FEC) NABTS データを提供します。

生の唯一の違い FEC NABTS データは、サブフォーマット GUID の値または

指定するときに**PINNAME\_ビデオ\_NABTS**ピンを使用して、次の表の情報。

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
<td><p>KS_DATARANGE</p></td>
</tr>
<tr class="even">
<td><p><strong>DataFormat 構造体</strong></p></td>
<td><p>KS_DATAFORMAT</p></td>
</tr>
<tr class="odd">
<td><p><strong>主な形式の GUID</strong></p></td>
<td><p>KS_DATAFORMAT_TYPE_NABTS</p></td>
</tr>
<tr class="even">
<td><p><strong>GUID を subFormat します。</strong></p></td>
<td><p>KSDATAFORMAT_SUBTYPE_NABTS (生 NABTS)</p>
<p>KSDATAFORMAT_SUBTYPE_NABTS_FEC (転送エラー訂正 NABTS)</p></td>
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

 

 

 





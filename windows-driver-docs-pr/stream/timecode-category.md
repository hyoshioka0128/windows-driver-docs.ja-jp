---
title: タイムコード カテゴリ
description: タイムコード カテゴリ
ms.assetid: 273e0233-357e-4e13-bf8e-77ca36834ee7
keywords:
- ストリームのカテゴリ WDK ビデオ キャプチャ、imecode
- Timecode カテゴリ WDK ビデオのキャプチャします。
- PINNAME_VIDEO_TIMECODE
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 00abaa1cc92b55dffb86b151b56023303d65341e
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63365193"
---
# <a name="timecode-category"></a>タイムコード カテゴリ


次の GUID はタイムコード カテゴリに対応します。

-   **PINNAME\_ビデオ\_タイムコード**

    カテゴリ出力ピンのタイムコード タイムコードのストリームを提供します。

作成するときに**PINNAME\_ビデオ\_タイムコード**ピンを使用して、次の表の情報。

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
<td><p>KSDATARANGE</p></td>
</tr>
<tr class="even">
<td><p><strong>DataFormat 構造体</strong></p></td>
<td><p>KSDATAFORMAT</p></td>
</tr>
<tr class="odd">
<td><p><strong>主な形式の GUID</strong></p></td>
<td><p>定義されていません。 MEDIATYPE_Timecode の直接表示するを使用して GUID を定義します。</p></td>
</tr>
<tr class="even">
<td><p><strong>サブ GUID を書式設定します。</strong></p></td>
<td><p>KSDATAFORMAT_SUBTYPE_NONE</p></td>
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
<td><p>MEDIATYPE_Timecode</p></td>
</tr>
<tr class="even">
<td><p><strong>DirectShow formattype</strong></p></td>
<td><p>MEDIASUBTYPE_None</p></td>
</tr>
</tbody>
</table>

 

 

 





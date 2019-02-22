---
title: VBI カテゴリ
description: VBI カテゴリ
ms.assetid: c33c0427-5162-435a-bb96-a230455a1035
keywords:
- カテゴリの WDK ビデオのキャプチャ、VBI をストリーム配信します。
- VBI WDK ビデオのキャプチャ
- 垂直帰線消去期間 WDK ビデオのキャプチャします。
- PINNAME_VIDEO_VBI
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c699c0a90aa83ae2405fc6afff50dbe1fe0a296c
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56561099"
---
# <a name="vbi-category"></a>VBI カテゴリ


次の GUID は、垂直帰線消去期間 (VBI) カテゴリに対応します。

-   **PINNAME\_ビデオ\_VBI**

    VBI カテゴリの出力ピンは、VBI 波形サンプルのストリームを提供します。 このストリームは、クローズド キャプション (CC)、NABTS、WST、タイムコード、およびその他のデジタル データ ストリームを抽出するコーデックをダウン ストリームに渡されます。

指定するときに**PINNAME\_ビデオ\_VBI**ピンを使用して、次の表の情報。

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
<td><p><strong>MajorFormat GUID</strong></p></td>
<td><p>KS_DATAFORMAT_TYPE_VBI</p></td>
</tr>
<tr class="even">
<td><p><strong>GUID を subFormat します。</strong></p></td>
<td><p>KSDATAFORMAT_SUBTYPE_RAW8</p></td>
</tr>
<tr class="odd">
<td><p><strong>GUID を指定子</strong></p></td>
<td><p>KSDATAFORMAT_SPECIFIER_VBI</p></td>
</tr>
<tr class="even">
<td><p><strong>拡張のヘッダーのサイズ</strong></p></td>
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff567694" data-raw-source="[&lt;strong&gt;KS_VBI_FRAME_INFO&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff567694)"><strong>KS_VBI_FRAME_INFO</strong></a></p></td>
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

 

 

 





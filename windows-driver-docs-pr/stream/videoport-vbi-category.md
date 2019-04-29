---
title: ビデオポート VBI カテゴリ
description: ビデオポート VBI カテゴリ
ms.assetid: 99a4d204-45af-4b73-8d31-d745387a38ac
keywords:
- ストリーム カテゴリ WDK ビデオのキャプチャ、VBI ビデオ ポート
- ビデオ ポート VBI カテゴリ WDK ビデオのキャプチャします。
- VBI WDK ビデオのキャプチャ
- 垂直帰線消去期間 WDK ビデオのキャプチャします。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 087b262ac037b362e7236a954840b42fe23992d1
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63329954"
---
# <a name="videoport-vbi-category"></a>ビデオポート VBI カテゴリ


次の GUID は、ビデオ ポートの垂直方向の非表示-間隔 (VBI) カテゴリに対応します。

-   **PINNAME\_ビデオ\_ビデオ ポート\_VBI**

    ビデオ ポート VBI カテゴリ ピンは、ハードウェアの接続を介して DirectDraw サーフェスを直接、アナログのデコーダーから VBI ストリームを転送します。

指定するときに**PINNAME\_ビデオ\_ビデオ ポート\_VBI**ピンを使用して、次の表の情報。

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
<td><p><strong>MajorFormat GUID</strong></p></td>
<td><p>KSDATAFORMAT_TYPE_VIDEO</p></td>
</tr>
<tr class="even">
<td><p><strong>サブ GUID を書式設定します。</strong></p></td>
<td><p>KSDATAFORMAT_SUBTYPE_VPVBIVideo</p></td>
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
<td><p>KSPROPSETID_VPVBIConfig</p></td>
</tr>
<tr class="even">
<td><p><strong>必要なイベントのセット</strong></p></td>
<td><p>KSEVENTSETID_VPVBINotify</p></td>
</tr>
<tr class="odd">
<td><p><strong>DirectShow majortype</strong></p></td>
<td><p>MEDIATYPE_Video</p></td>
</tr>
<tr class="even">
<td><p><strong>DirectShow formattype</strong></p></td>
<td><p>なし</p></td>
</tr>
</tbody>
</table>

 

 

 





---
title: ビデオポート カテゴリ
description: ビデオポート カテゴリ
ms.assetid: c11a407f-4ff0-4337-b989-e3ec42418ec3
keywords:
- ストリームのカテゴリ WDK ビデオ キャプチャ、ビデオ ポート
- ビデオ ポート カテゴリ WDK ビデオのキャプチャします。
- ビデオ ポート カテゴリ WDK ビデオのキャプチャします。
- PINNAME_VIDEO_VIDEOPORT
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6765c37b0a6172dab192afde45a3e8c66d31d6f5
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67385366"
---
# <a name="videoport-category"></a>ビデオポート カテゴリ


次の GUID は、ビデオ ポート カテゴリに対応します。

-   **PINNAME\_ビデオ\_ビデオ ポート**

    ビデオ ポート分類のピンは、ハードウェアのビデオ ポート接続を介して DirectDraw サーフェスを直接、アナログ ビデオ デコーダーから画像ストリームを転送します。

指定するときに**PINNAME\_ビデオ\_ビデオ ポート**ピンを使用して、次の表の情報。

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
<td><p>KSDATAFORMAT_TYPE_VIDEO</p></td>
</tr>
<tr class="even">
<td><p><strong>サブ GUID を書式設定します。</strong></p></td>
<td><p>KSDATAFORMAT_SUBTYPE_VPVideo</p></td>
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
<td><p>KSPROPSETID_VPConfig</p></td>
</tr>
<tr class="even">
<td><p><strong>必要なイベントのセット</strong></p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/stream/kseventsetid-vpnotify" data-raw-source="[KSEVENTSETID_VPNotify](https://docs.microsoft.com/windows-hardware/drivers/stream/kseventsetid-vpnotify)">KSEVENTSETID_VPNotify</a></p></td>
</tr>
<tr class="odd">
<td><p><strong>DirectShow majortype</strong></p></td>
<td><p>Mediatype_Video</p></td>
</tr>
<tr class="even">
<td><p><strong>DirectShow formattype</strong></p></td>
<td><p>なし</p></td>
</tr>
</tbody>
</table>

 

 

 





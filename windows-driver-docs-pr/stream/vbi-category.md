---
title: VBI カテゴリ
description: VBI カテゴリ
ms.assetid: c33c0427-5162-435a-bb96-a230455a1035
keywords:
- ストリームカテゴリ WDK ビデオキャプチャ、VBI
- VBI WDK ビデオキャプチャ
- 垂直のブランキング間隔 WDK ビデオキャプチャ
- PINNAME_VIDEO_VBI
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6cdc4c5896f5983f54e0dab6b4309e56580fc030
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844938"
---
# <a name="vbi-category"></a>VBI カテゴリ


次の GUID は、垂直ブランキング間隔 (VBI) カテゴリに対応しています。

-   **PINNAME\_VIDEO\_VBI**

    VBI カテゴリの出力ピンは、VBI の波形サンプルのストリームを提供します。 このストリームは、クローズドキャプション (CC)、NABTS、WST、タイムコード、およびその他のデジタルデータストリームを抽出する下流コーデックに渡されます。

**ビデオ\_VBI pin\_Pinname**を指定する場合は、次の表に示す情報を使用します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>備わっている</th>
<th>Value</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>DataRange 構造体</strong></p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagks_datarange_video_vbi" data-raw-source="[&lt;strong&gt;KS_DATARANGE_VIDEO_VBI&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagks_datarange_video_vbi)"><strong>KS_DATARANGE_VIDEO_VBI</strong></a></p></td>
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
<td><p><strong>サブフォーマット GUID</strong></p></td>
<td><p>KSDATAFORMAT_SUBTYPE_RAW8</p></td>
</tr>
<tr class="odd">
<td><p><strong>指定子 GUID</strong></p></td>
<td><p>KSDATAFORMAT_SPECIFIER_VBI</p></td>
</tr>
<tr class="even">
<td><p><strong>拡張ヘッダーサイズ</strong></p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagks_vbi_frame_info" data-raw-source="[&lt;strong&gt;KS_VBI_FRAME_INFO&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagks_vbi_frame_info)"><strong>KS_VBI_FRAME_INFO</strong></a></p></td>
</tr>
<tr class="odd">
<td><p><strong>必須のプロパティセット</strong></p></td>
<td><p>なし</p></td>
</tr>
<tr class="even">
<td><p><strong>必須イベントセット</strong></p></td>
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

 

 

 





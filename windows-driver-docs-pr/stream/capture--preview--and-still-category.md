---
title: キャプチャ、プレビュー、およびカテゴリを引き続き
description: キャプチャ、プレビュー、およびカテゴリを引き続き
ms.assetid: b82cc3b6-1cea-4864-9501-95919f05455f
keywords:
- ストリーム カテゴリ WDK ビデオのキャプチャ、ビデオ ストリームをキャプチャします。
- ストリーム カテゴリ WDK ビデオのキャプチャ、ビデオ ストリームをプレビュー
- ストリーム カテゴリ WDK ビデオのキャプチャ、静止画像のキャプチャ
- ビデオ ストリーム カテゴリの WDK ビデオのキャプチャのキャプチャします。
- ビデオ ストリーム カテゴリ WDK ビデオ キャプチャをプレビューします。
- 静止画像カテゴリ WDK ビデオ キャプチャをキャプチャします。
- PINNAME_VIDEO_CAPTURE
- NAME_VIDEO_PREVIEW
- PINNAME_VIDEO_STILL
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ca096532db207df77cfa9f430bab9ca81bb14def
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56530975"
---
# <a name="capture-preview-and-still-category"></a>キャプチャ、プレビュー、およびカテゴリを引き続き


次の Guid は、ビデオ ストリームをキャプチャし、ビデオのストリームをプレビューし、(ハードウェアでサポートされている) 場合、イメージ キャプチャもカテゴリに対応しています。

-   **PINNAME\_ビデオ\_キャプチャ**

    カテゴリ出力ピンがキャプチャまたは非圧縮のデジタル ビデオのストリームを提供します。 このストリームのカテゴリは、ビデオの会議へと画像分析、ディスクにムービーを書き込みに使用されます。

-   **PINNAME\_ビデオ\_プレビュー**

    カテゴリ出力ピンがプレビューでは、圧縮されていないデジタル ビデオのストリームを提供します。 このストリームのカテゴリは、DirectDraw を直接表示できる RGB または YUV のいずれかの形式で、ローカルのモニター、ビデオ ストリームの表示に使用されます。 リソースに限定された状況にはキャプチャ ミニドライバーにプレビュー ストリーム ピン ピンがストリームをキャプチャするよりも低い優先順位を設定する必要があります。

-   **PINNAME\_ビデオ\_まだ**

    まだカテゴリの出力ピンは、キャプチャ ストリームと (つまり、キャプチャ ストリームよりも高い品質の多くの場合、) 静止画像ストリームの両方を生成できるはデュアル モードのカメラで使用されます。 静止画像ストリームには、外部またはプログラムでは、画像の取得をトリガする機能が含まれています。

キャプチャ、プレビュー、およびまだストリーム暗証番号 (pin) カテゴリは、データ形式とストリーム特性の観点からはほぼ同じです。

**注**  :多くのカメラでは、1 つの出力ストリームのみを生成するため、Microsoft DirectShow にキャプチャし、プレビュー ストリームに 1 つのストリームを分割するスマート Tee フィルターが含まれます。 そのため、1 つのストリームのみを生成するカメラのミニドライバーすると、プレビュー ストリームを生成するために、データ ストリームが内部的には重複しない必要があります。

 

指定するときに**PINNAME\_ビデオ\_キャプチャ**、または**PINNAME\_ビデオ\_プレビュー**、または**PINNAME\_ビデオ\_まだ**ピンを使用して、次の表の情報。

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
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff567628" data-raw-source="[&lt;strong&gt;KS_DATARANGE_VIDEO&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff567628)"><strong>KS_DATARANGE_VIDEO</strong> </a> (フレームのみ)</p>
<p><a href="https://msdn.microsoft.com/library/windows/hardware/ff567629" data-raw-source="[&lt;strong&gt;KS_DATARANGE_VIDEO2&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff567629)"><strong>KS_DATARANGE_VIDEO2</strong> </a> (bob またはの設定を一元管理のフィールドまたはフレームを)</p>
<p><a href="https://msdn.microsoft.com/library/windows/hardware/ff567353" data-raw-source="[&lt;strong&gt;KS_DATARANGE_MPEG1_VIDEO&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff567353)"><strong>KS_DATARANGE_MPEG1_VIDEO</strong></a></p>
<p><a href="https://msdn.microsoft.com/library/windows/hardware/ff567362" data-raw-source="[&lt;strong&gt;KS_DATARANGE_MPEG2_VIDEO&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff567362)"><strong>KS_DATARANGE_MPEG2_VIDEO</strong></a></p></td>
</tr>
<tr class="even">
<td><p><strong>DataFormat 構造体</strong></p></td>
<td><p>KS_DATAFORMAT_VIDEO (フレームのみ)</p>
<p>KS_DATAFORMAT_VIDEO2 (bob またはの設定を一元管理のフィールドまたはフレームを)</p>
<p><a href="https://msdn.microsoft.com/library/windows/hardware/ff567658" data-raw-source="[&lt;strong&gt;KS_MPEG1VIDEOINFO&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff567658)"><strong>KS_MPEG1VIDEOINFO</strong> </a> (用 MPEG1)</p>
<p><a href="https://msdn.microsoft.com/library/windows/hardware/ff567667" data-raw-source="[&lt;strong&gt;KS_MPEGVIDEOINFO2&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff567667)"><strong>KS_MPEGVIDEOINFO2</strong> </a> (用 MPEG2)</p></td>
</tr>
<tr class="odd">
<td><p><strong>主な形式の GUID</strong></p></td>
<td><p>KSDATAFORMAT_TYPE_VIDEO</p></td>
</tr>
<tr class="even">
<td><p><strong>サブ GUID を書式設定します。</strong></p></td>
<td><p>RGB16、RGB24、UYVY、JPEG</p></td>
</tr>
<tr class="odd">
<td><p><strong>GUID を指定子</strong></p></td>
<td><p>KSDATAFORMAT_SPECIFIER_VIDEOINFO (フレームのみ)</p>
<p>KSDATAFORMAT_SPECIFIER_VIDEOINFO2 (フィールドまたはフレーム)</p></td>
</tr>
<tr class="even">
<td><p><strong>拡張のヘッダーのサイズ</strong></p></td>
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff567645" data-raw-source="[&lt;strong&gt;KS_FRAME_INFO&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff567645)"><strong>KS_FRAME_INFO</strong> </a>場合 MPEG フォーマットではありません。 MPEG、形式の場合は 0 します。</p></td>
</tr>
<tr class="odd">
<td><p><strong>必要なプロパティ セット</strong></p></td>
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff566568" data-raw-source="[KSPROPSETID_Connection](https://msdn.microsoft.com/library/windows/hardware/ff566568)">KSPROPSETID_Connection</a></p>
<p><a href="https://msdn.microsoft.com/library/windows/hardware/ff567806" data-raw-source="[PROPSETID_VIDCAP_DROPPEDFRAMES](https://msdn.microsoft.com/library/windows/hardware/ff567806)">PROPSETID_VIDCAP_DROPPEDFRAMES</a></p></td>
</tr>
<tr class="even">
<td><p><strong>必要なイベントのセット</strong></p></td>
<td><p>なし</p></td>
</tr>
<tr class="odd">
<td><p><strong>DirectShow majortype</strong></p></td>
<td><p>MEDIATYPE_Video</p></td>
</tr>
<tr class="even">
<td><p><strong>DirectShow formattype</strong></p></td>
<td><p>FORMAT_VideoInfo (フレームのみ)</p>
<p>FORMAT_VideoInfo2 (フィールドまたはフレーム)</p></td>
</tr>
</tbody>
</table>

 

 

 





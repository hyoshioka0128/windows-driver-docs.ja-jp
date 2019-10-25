---
title: キャプチャ、プレビュー、静止画カテゴリ
description: キャプチャ、プレビュー、静止画カテゴリ
ms.assetid: b82cc3b6-1cea-4864-9501-95919f05455f
keywords:
- ストリームカテゴリ WDK ビデオキャプチャ、ビデオストリームのキャプチャ
- ストリームカテゴリ WDK ビデオキャプチャ、ビデオストリームのプレビュー
- ストリームカテゴリ WDK ビデオキャプチャ、キャプチャ静止イメージ
- ビデオストリームのキャプチャのカテゴリ WDK ビデオキャプチャ
- ビデオストリームのプレビューカテゴリ WDK ビデオキャプチャ
- キャプチャ静止イメージカテゴリ WDK ビデオキャプチャ
- PINNAME_VIDEO_CAPTURE
- NAME_VIDEO_PREVIEW
- PINNAME_VIDEO_STILL
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 442932b257ed01e8a8677684afe511bab505881b
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844741"
---
# <a name="capture-preview-and-still-category"></a>キャプチャ、プレビュー、静止画カテゴリ


次の Guid は、ビデオストリームをキャプチャし、ビデオストリームをプレビューし、静止イメージをキャプチャするカテゴリに対応しています (ハードウェアでサポートされている場合)。

-   **ビデオ\_キャプチャ\_PINNAME**

    キャプチャカテゴリの出力ピンは、圧縮または圧縮されていないデジタルビデオのストリームを提供します。 このストリームカテゴリは、ムービーをディスク、ビデオ会議、および画像分析に書き込むために使用されます。

-   **PINNAME\_VIDEO\_PREVIEW**

    プレビューカテゴリの出力ピンは、非圧縮デジタルビデオのストリームを提供します。 このストリームカテゴリは、ローカルモニターのビデオストリームを表示するために使用されます。 RGB 形式または YUV 形式で、DirectDraw によって直接表示できます。 リソースが限られている状況では、capture ミニドライバーは、キャプチャストリームの pin より小さいプレビューストリームのピンの優先順位を設定する必要があります。

-   **ビデオ\_\_PINNAME**

    引き続きカテゴリの出力ピンは、キャプチャストリームと静止イメージストリームの両方を生成できるデュアルモードカメラで使用されます (多くの場合、キャプチャストリームよりも品質が高くなります)。 静止イメージストリームには、イメージの取得を外部またはプログラムによってトリガーする機能が含まれています。

キャプチャ、プレビュー、およびストリームピンの各カテゴリは、データ形式やストリーム特性という点でほぼ同じです。

**注**  : 多くのカメラでは1つの出力ストリームしか生成されないため、Microsoft DirectShow には、1つのストリームをキャプチャとプレビューストリームに分割するスマート t フィルターが含まれています。 そのため、1つのストリームのみを生成するカメラのミニドライバーでは、データストリームを内部で複製してプレビューストリームを生成することはできません。

 

**Pinname\_video\_CAPTURE**、または**pinname\_video\_PREVIEW**、または**PINNAME\_video\_まだ**pin を指定する場合は、次の表に示す情報を使用します。

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
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagks_datarange_video" data-raw-source="[&lt;strong&gt;KS_DATARANGE_VIDEO&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagks_datarange_video)"><strong>KS_DATARANGE_VIDEO</strong></a> (フレームのみ)</p>
<p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagks_datarange_video2" data-raw-source="[&lt;strong&gt;KS_DATARANGE_VIDEO2&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagks_datarange_video2)"><strong>KS_DATARANGE_VIDEO2</strong></a> (フィールドまたはフレーム、bob、またはの設定)</p>
<p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagks_datarange_mpeg1_video" data-raw-source="[&lt;strong&gt;KS_DATARANGE_MPEG1_VIDEO&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagks_datarange_mpeg1_video)"><strong>KS_DATARANGE_MPEG1_VIDEO</strong></a></p>
<p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagks_datarange_mpeg2_video" data-raw-source="[&lt;strong&gt;KS_DATARANGE_MPEG2_VIDEO&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagks_datarange_mpeg2_video)"><strong>KS_DATARANGE_MPEG2_VIDEO</strong></a></p></td>
</tr>
<tr class="even">
<td><p><strong>DataFormat 構造体</strong></p></td>
<td><p>KS_DATAFORMAT_VIDEO (フレームのみ)</p>
<p>KS_DATAFORMAT_VIDEO2 (フィールドまたはフレーム、bob、またはの設定)</p>
<p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagks_mpeg1videoinfo" data-raw-source="[&lt;strong&gt;KS_MPEG1VIDEOINFO&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagks_mpeg1videoinfo)"><strong>KS_MPEG1VIDEOINFO</strong></a> (MPEG1 の場合)</p>
<p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagks_mpegvideoinfo2" data-raw-source="[&lt;strong&gt;KS_MPEGVIDEOINFO2&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagks_mpegvideoinfo2)"><strong>KS_MPEGVIDEOINFO2</strong></a> (MPEG2 用)</p></td>
</tr>
<tr class="odd">
<td><p><strong>メジャー形式 GUID</strong></p></td>
<td><p>KSDATAFORMAT_TYPE_VIDEO</p></td>
</tr>
<tr class="even">
<td><p><strong>サブフォーマット GUID</strong></p></td>
<td><p>RGB16、RGB24、UYVY、JPEG</p></td>
</tr>
<tr class="odd">
<td><p><strong>指定子 GUID</strong></p></td>
<td><p>KSDATAFORMAT_SPECIFIER_VIDEOINFO (フレームのみ)</p>
<p>KSDATAFORMAT_SPECIFIER_VIDEOINFO2 (フィールドまたはフレーム)</p></td>
</tr>
<tr class="even">
<td><p><strong>拡張ヘッダーサイズ</strong></p></td>
<td><p>MPEG 形式でない場合は<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagks_frame_info" data-raw-source="[&lt;strong&gt;KS_FRAME_INFO&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagks_frame_info)"><strong>KS_FRAME_INFO</strong></a> 。 MPEG 形式の場合は0。</p></td>
</tr>
<tr class="odd">
<td><p><strong>必須のプロパティセット</strong></p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/stream/kspropsetid-connection" data-raw-source="[KSPROPSETID_Connection](https://docs.microsoft.com/windows-hardware/drivers/stream/kspropsetid-connection)">KSPROPSETID_Connection</a></p>
<p><a href="https://docs.microsoft.com/windows-hardware/drivers/stream/propsetid-vidcap-droppedframes" data-raw-source="[PROPSETID_VIDCAP_DROPPEDFRAMES](https://docs.microsoft.com/windows-hardware/drivers/stream/propsetid-vidcap-droppedframes)">PROPSETID_VIDCAP_DROPPEDFRAMES</a></p></td>
</tr>
<tr class="even">
<td><p><strong>必須イベントセット</strong></p></td>
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

 

 

 





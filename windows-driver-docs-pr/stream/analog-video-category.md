---
title: アナログ ビデオ カテゴリ
description: アナログ ビデオ カテゴリ
ms.assetid: 64564c81-b1e1-482b-ae70-59b229a5e86f
keywords:
- ストリームカテゴリ WDK ビデオキャプチャ、アナログビデオ
- アナログビデオカテゴリ WDK ビデオキャプチャ
- PINNAME_VIDEO_ANALOGVIDEOIN
- アナログオーディオ WDK ビデオキャプチャ
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f1d301379708fb7331faa9633f5deef303d07d4d
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72845582"
---
# <a name="analog-video-category"></a>アナログ ビデオ カテゴリ


次の GUID は、カテゴリのアナログビデオに対応しています。

-   **PINNAME\_VIDEO\_ANALOGVIDEOIN**

    アナログビデオのカテゴリは、ビデオデコーダーフィルターへのアナログビデオ入力のストリームを表します。

**Pinname\_VIDEO\_ANALOGVIDEOIN**、pin を指定する場合は、次の表に示す情報を使用します。

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
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagks_datarange_analogvideo" data-raw-source="[&lt;strong&gt;KS_DATARANGE_ANALOGVIDEO&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagks_datarange_analogvideo)"><strong>KS_DATARANGE_ANALOGVIDEO</strong></a></p></td>
</tr>
<tr class="even">
<td><p><strong>DataFormat 構造体</strong></p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagks_datarange_analogvideo" data-raw-source="[&lt;strong&gt;KS_DATARANGE_ANALOGVIDEO&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagks_datarange_analogvideo)"><strong>KS_DATARANGE_ANALOGVIDEO</strong></a></p></td>
</tr>
<tr class="odd">
<td><p><strong>MajorFormat GUID</strong></p></td>
<td><p>KSDATAFORMAT_TYPE_ANALOGVIDEO</p></td>
</tr>
<tr class="even">
<td><p><strong>サブフォーマット GUID</strong></p></td>
<td><p>KSDATAFORMAT_SUBTYPE_NONE</p></td>
</tr>
<tr class="odd">
<td><p><strong>指定子 GUID</strong></p></td>
<td><p>KSDATAFORMAT_SPECIFIER_ANALOGVIDEO</p></td>
</tr>
<tr class="even">
<td><p><strong>拡張ヘッダーサイズ</strong></p></td>
<td><p>0</p></td>
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
<td><p>MEDIATYPE_AnalogVideo</p></td>
</tr>
<tr class="even">
<td><p><strong>DirectShow formattype</strong></p></td>
<td><p>FORMAT_AnalogVideo</p></td>
</tr>
</tbody>
</table>

 

アナログオーディオ用に定義された特別なカテゴリはありません (TV や無線オーディオなど)。 アナログオーディオピンを持つデバイスのカテゴリを指定する場合、 **MajorFormat**メンバーの値は KSDATAFORMAT\_TYPE\_ANALOGAUDIO にする必要があります。 **指定子**メンバーの値は、KSDATAFORMAT\_指定子\_none、 **subtype**メンバー、および format BLOCK を KSDATAFORMAT\_subtype\_none に設定する必要があります。 ラジオオーディオの詳細については、「[ラジオチューナーを使用したビデオキャプチャデバイス](video-capture-devices-with-radio-tuners.md)」を参照してください。

アナログビデオストリームは基本的にアナログビデオデコーダーへの入力を模倣していますが、チューニング情報のデータ転送として同時に機能します。 テレビチューナーフィルターで送信される調整パケットは、すべてのチューニング操作の開始時と終了時に介在するクロスバーフィルターによって渡されます。 データパケットは、使用されている国/地域コード、チャネル、周波数、およびアナログビデオ標準を含む[ **\_変更\_情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagks_tvtuner_change_info)の構造を\_TVTUNER です。

キャプチャフィルターは、VBI 出力ストリームの拡張ヘッダーにあるこのチューニングパケットを下流 VBI コーデックに伝達する必要があります。

 

 





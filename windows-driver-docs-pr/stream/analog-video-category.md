---
title: アナログ ビデオ カテゴリ
description: アナログ ビデオ カテゴリ
ms.assetid: 64564c81-b1e1-482b-ae70-59b229a5e86f
keywords:
- ストリームのカテゴリ WDK ビデオ キャプチャ、アナログ ビデオ
- アナログ ビデオ カテゴリ WDK ビデオのキャプチャします。
- PINNAME_VIDEO_ANALOGVIDEOIN
- ビデオのアナログ オーディオ WDK をキャプチャします。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ff6541ffef0bcde4206b441e0d6c685c40955c25
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67386771"
---
# <a name="analog-video-category"></a>アナログ ビデオ カテゴリ


次の GUID は、カテゴリのアナログ ビデオに対応します。

-   **PINNAME\_ビデオ\_ANALOGVIDEOIN**

    アナログ ビデオのカテゴリでは、アナログ ビデオへの入力ビデオ デコーダー フィルター ストリームを表します。

指定するときに**PINNAME\_ビデオ\_ANALOGVIDEOIN**pin、次の表の情報を使用します。

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
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-tagks_datarange_analogvideo" data-raw-source="[&lt;strong&gt;KS_DATARANGE_ANALOGVIDEO&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-tagks_datarange_analogvideo)"><strong>KS_DATARANGE_ANALOGVIDEO</strong></a></p></td>
</tr>
<tr class="even">
<td><p><strong>DataFormat 構造体</strong></p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-tagks_datarange_analogvideo" data-raw-source="[&lt;strong&gt;KS_DATARANGE_ANALOGVIDEO&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-tagks_datarange_analogvideo)"><strong>KS_DATARANGE_ANALOGVIDEO</strong></a></p></td>
</tr>
<tr class="odd">
<td><p><strong>MajorFormat GUID</strong></p></td>
<td><p>KSDATAFORMAT_TYPE_ANALOGVIDEO</p></td>
</tr>
<tr class="even">
<td><p><strong>サブ GUID を書式設定します。</strong></p></td>
<td><p>KSDATAFORMAT_SUBTYPE_NONE</p></td>
</tr>
<tr class="odd">
<td><p><strong>GUID を指定子</strong></p></td>
<td><p>KSDATAFORMAT_SPECIFIER_ANALOGVIDEO</p></td>
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
<td><p>MEDIATYPE_AnalogVideo</p></td>
</tr>
<tr class="even">
<td><p><strong>DirectShow formattype</strong></p></td>
<td><p>FORMAT_AnalogVideo</p></td>
</tr>
</tbody>
</table>

 

テレビなどのアナログのオーディオまたはオーディオのラジオに対して定義されている特殊なカテゴリはありません。 アナログのオーディオ ピンの値を持つデバイスのカテゴリを指定するときに、 **MajorFormat**メンバー KSDATAFORMAT をする必要があります\_型\_アナログします。 値、**指定子**メンバー KSDATAFORMAT をする必要があります\_指定子\_NONE、**サブタイプ**KSDATAFORMATメンバーとブロックの書式設定を設定する必要があります\_サブタイプ\_NONE。 無線の音声の詳細については、次を参照してください。[ラジオ チューナーを持つビデオ キャプチャ デバイス](video-capture-devices-with-radio-tuners.md)します。

アナログ ビデオ ストリームは、基本的に、アナログ ビデオ デコーダーへの入力を模倣が同時にチューニングの詳細についてデータ転送として機能します。 パケットをチューニングするは、テレビ チューナーのフィルターで生成された先頭と末尾のすべてのチューニング操作でのすべての介在するクロスバー フィルターを通じて渡されます。 データ パケットが、 [ **KS\_tv チューナー\_変更\_情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-tagks_tvtuner_change_info)国/地域コード、チャネル、頻度、および標準のアナログ ビデオを含む構造体使用します。

キャプチャ フィルターは、ダウン ストリームの VBI コーデックを VBI 出力ストリームの拡張のヘッダー内のチューニングこのパケットを伝達する必要があります。

 

 





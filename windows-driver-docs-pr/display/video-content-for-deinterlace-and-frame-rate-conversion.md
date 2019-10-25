---
title: デインターレースおよびフレーム レート変換のビデオ コンテンツ
description: デインターレースおよびフレーム レート変換のビデオ コンテンツ
ms.assetid: 627b394e-c2e1-4327-adaa-0c3436ba3d1a
keywords:
- WDK DirectX VA のノンインターレース、受信したビデオコンテンツ
- フレームレート変換 WDK DirectX VA
- ビデオコンテンツを受信した WDK DirectX VA
- ノンインターレース WDK DirectX VA のビデオコンテンツ
- フレームレート変換のビデオコンテンツの WDK DirectX VA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 76069f968c537ee2868c5625853d2740fe095676
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72825296"
---
# <a name="video-content-for-deinterlace-and-frame-rate-conversion"></a>デインターレースおよびフレーム レート変換のビデオ コンテンツ


## <span id="ddk_video_content_for_deinterlace_and_frame_rate_conversion_gg"></span><span id="DDK_VIDEO_CONTENT_FOR_DEINTERLACE_AND_FRAME_RATE_CONVERSION_GG"></span>


ドライバーはビデオコンテンツの説明を受信して、そのようなコンテンツのインターレース解除やフレームレート変換の方法を判断できるようにします。 ドライバーは、次の関数呼び出しで、このビデオコンテンツを[**DXVA\_VideoDesc**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_videodesc)構造体へのポインターとして受信します。

-   [**DeinterlaceQueryAvailableModes**](https://docs.microsoft.com/windows-hardware/drivers/display/dxva-deinterlacecontainerdeviceclass-deinterlacequeryavailablemodes)

-   [**DeinterlaceQueryModeCaps**](https://docs.microsoft.com/windows-hardware/drivers/display/dxva-deinterlacecontainerdeviceclass-deinterlacequerymodecaps)

-   [**DeinterlaceOpenStream**](https://docs.microsoft.com/windows-hardware/drivers/display/dxva-deinterlacebobdeviceclass-deinterlaceopenstream)

次の例は、受信したビデオコンテンツに対してドライバーがインターレース解除とフレームレート変換を実行する方法を示しています。

### <a name="span-iddeinterlacing_720_x_480i_content_examplespanspan-iddeinterlacing_720_x_480i_content_examplespanspan-iddeinterlacing_720_x_480i_content_examplespandeinterlacing-720-x-480i-content-example"></a><span id="Deinterlacing_720_x_480i_Content_Example"></span><span id="deinterlacing_720_x_480i_content_example"></span><span id="DEINTERLACING_720_X_480I_CONTENT_EXAMPLE"></span>インターレース解除 720 x 480i コンテンツの例

DXVA\_VideoDesc 構造体は、29.97 Hz の頻度でサンプルあたり2つのフィールドとして供給されている 720 x 480i コンテンツをインターレース解除するようにドライバーに指示するために、次のように入力されます。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">メンバー</th>
<th align="left">Value</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><strong>SampleWidth</strong></p></td>
<td align="left"><p>720</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>SampleHeight</strong></p></td>
<td align="left"><p>480</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>SampleFormat</strong></p></td>
<td align="left"><p>DXVA_SampleFormat の<strong>DXVA_SampleFieldInterleavedOddFirst</strong>列挙子<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/dxva/ne-dxva-_dxva_sampleformat" data-raw-source="[&lt;strong&gt;DXVA_SampleFormat&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/dxva/ne-dxva-_dxva_sampleformat)"></a></p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>d3dFormat</strong></p></td>
<td align="left"><p><em>D3d8types</em>および<em>d3d9types</em>ヘッダーファイルで定義されている D3DFMT_YUY2</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>InputSampleFreq</strong></p></td>
<td align="left"><p>3万 (29.97-Hz モニターの頻度)</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>InputSampleFreq</strong></p></td>
<td align="left"><p>1001</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>OutputFrameFreq</strong></p></td>
<td align="left"><p>6万 (59.94-Hz モニターの頻度)</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>OutputFrameFreq</strong></p></td>
<td align="left"><p>1001</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-iddeinterlacing_and_frame-rate_conversion_of_720_x_480i_content_examplespanspan-iddeinterlacing_and_frame-rate_conversion_of_720_x_480i_content_examplespanspan-iddeinterlacing_and_frame-rate_conversion_of_720_x_480i_content_examplespandeinterlacing-and-frame-rate-conversion-of-720-x-480i-content-example"></a><span id="Deinterlacing_and_Frame-Rate_Conversion_of_720_x_480i_Content_Example"></span><span id="deinterlacing_and_frame-rate_conversion_of_720_x_480i_content_example"></span><span id="DEINTERLACING_AND_FRAME-RATE_CONVERSION_OF_720_X_480I_CONTENT_EXAMPLE"></span>720 x 480i コンテンツのインターレース解除とフレームレート変換の例

DXVA\_VideoDesc 構造体の**OutputFrameFreq**メンバーは、次のように入力されます。これにより、ドライバーがインターレース解除され、フレームレートが 720 x 480i コンテンツに変換されます。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">メンバー</th>
<th align="left">Value</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><strong>OutputFrameFreq</strong></p></td>
<td align="left"><p>85 (85-Hz モニターの頻度)</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>OutputFrameFreq</strong></p></td>
<td align="left"><p>1</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-iddeinterlacing_a_single_field_to_a_progressive_frame_examplespanspan-iddeinterlacing_a_single_field_to_a_progressive_frame_examplespanspan-iddeinterlacing_a_single_field_to_a_progressive_frame_examplespandeinterlacing-a-single-field-to-a-progressive-frame-example"></a><span id="Deinterlacing_a_Single_Field_to_a_Progressive_Frame_Example"></span><span id="deinterlacing_a_single_field_to_a_progressive_frame_example"></span><span id="DEINTERLACING_A_SINGLE_FIELD_TO_A_PROGRESSIVE_FRAME_EXAMPLE"></span>1つのフィールドをプログレッシブフレームにインターレース解除する例

DXVA\_VideoDesc 構造体の**OutputFrameFreq**メンバーは、次のように入力されます。これにより、ドライバーは、1つのフィールドを、後の MPEG エンコーディングのためにプログレッシブフレームにインターレース解除するように指示します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">メンバー</th>
<th align="left">Value</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><strong>OutputFrameFreq</strong></p></td>
<td align="left"><p>3万 (29.97-Hz モニターの頻度)</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>OutputFrameFreq</strong></p></td>
<td align="left"><p>1001</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idframe-rate_conversion_of__480p_content_examplespanspan-idframe-rate_conversion_of__480p_content_examplespanspan-idframe-rate_conversion_of__480p_content_examplespanframe-rate-conversion-of-480p-content-example"></a><span id="Frame-Rate_Conversion_of__480p_Content_Example"></span><span id="frame-rate_conversion_of__480p_content_example"></span><span id="FRAME-RATE_CONVERSION_OF__480P_CONTENT_EXAMPLE"></span>480p コンテンツのフレームレート変換の例

DXVA\_VideoDesc 構造体は、次のように入力されます。これにより、ドライバーが480p コンテンツに対してフレームレート変換を実行し、モニターの表示頻度に一致するように指示します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">メンバー</th>
<th align="left">Value</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><strong>SampleWidth</strong></p></td>
<td align="left"><p>720</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>SampleHeight</strong></p></td>
<td align="left"><p>480</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>SampleFormat</strong></p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/dxva/ne-dxva-_dxva_sampleformat" data-raw-source="[&lt;strong&gt;DXVA_SampleFormat&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/dxva/ne-dxva-_dxva_sampleformat)"><strong>DXVA_SampleFormat</strong></a>列挙型の<strong>DXVA_SampleProgressiveFrame</strong>列挙子</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>d3dFormat</strong></p></td>
<td align="left"><p>D3d8types および d3d9types ヘッダーファイルで定義されている D3DFMT_YUY2</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>InputSampleFreq</strong></p></td>
<td align="left"><p>60 (60 Hz モニターの頻度)</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>InputSampleFreq</strong></p></td>
<td align="left"><p>1</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>OutputFrameFreq</strong></p></td>
<td align="left"><p>85 (85 Hz モニターの頻度)</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>OutputFrameFreq</strong></p></td>
<td align="left"><p>1</p></td>
</tr>
</tbody>
</table>

 

 

 






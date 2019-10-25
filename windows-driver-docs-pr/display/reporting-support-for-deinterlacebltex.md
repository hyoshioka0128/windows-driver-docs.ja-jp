---
title: DeinterlaceBltEx に対するサポートのレポート
description: DeinterlaceBltEx に対するサポートのレポート
ms.assetid: 9cf8d05c-ef59-44a4-a377-66282e7888d5
keywords:
- DeinterlaceBltEx、レポート
- DXVA_VideoProcess_SubStreamsExtended
- DXVA_VideoProcess_YUV2RGBExtended
- DXVA_VideoProcess_AlphaBlendExtended
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ce6493015df036872e29e759f4a5735dbf929fe8
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72829590"
---
# <a name="reporting-support-for-deinterlacebltex"></a>DeinterlaceBltEx に対するサポートのレポート


**このセクションは、Windows Server 2003 SP1 以降、および Windows XP SP2 以降にのみ適用されます。**

Display driver は、DXVA\_VideoProcess\_SubStreams、DXVA\_VideoProcess\_StretchX、および DXVA\_VideoProcess を設定して、 [**DeinterlaceBltEx**](https://docs.microsoft.com/windows-hardware/drivers/display/dxva-deinterlacebobdeviceclass-deinterlacebltex)[ノンインターレース DDI](https://docs.microsoft.com/windows-hardware/drivers/display/deinterlace-ddi)関数のサポートを報告 @no__[**DXVA\_DeinterlaceCaps**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_deinterlacecaps)構造体の**videoprocessingcaps**メンバーの t_8_ 可変幅フラグ。 このドライバーは、 [**DeinterlaceQueryModeCaps**](https://docs.microsoft.com/windows-hardware/drivers/display/dxva-deinterlacecontainerdeviceclass-deinterlacequerymodecaps)関数が呼び出されたときに、DXVA\_DeinterlaceCaps へのポインターを返します。

ディスプレイドライバーは、DXVA\_VideoProcess\_サブストリームを設定して、ビデオサブストリームの合成とノンインターレースを結合します。 このドライバーは、ビデオストリームとサブストリームのピクセル縦横比が異なる可能性があり、非正方形であることがあるため、DXVA\_VideoProcess\_StretchX と DXVA\_VideoProcess\_可変幅を設定します。ドライバーは、独立している必要があります。インターレース解除用に送信されるビデオフレームと、指定されたビデオサブストリームの伸縮 (水平方向または垂直方向)。

[**DXVA\_DeinterlaceCaps**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_deinterlacecaps)構造体の DXVA **\_VIDEOPROCESS**\_YUV2RGB および DXVA\_videoprocess\_AlphaBlend フラグは、ドライバーののコンテキストでは意味がありません。[**DeinterlaceBltEx**](https://docs.microsoft.com/windows-hardware/drivers/display/dxva-deinterlacebobdeviceclass-deinterlacebltex)関数。 これらのフラグは、元の[**DeinterlaceBlt**](https://docs.microsoft.com/windows-hardware/drivers/display/dxva-deinterlacebobdeviceclass-deinterlaceblt)関数に関連しています。 *DeinterlaceBltEx*をサポートするディスプレイドライバーも*DeinterlaceBlt*をサポートする必要があるため、 *DeinterlaceBlt*のコンテキストで関連する操作をサポートしている場合は、ドライバーがこれらのフラグを報告する必要があります。

### <a name="span-iddxva_videoprocess_substreamsextended_dxva_videoprocess_yuv2rgbextended_and_dxva_videoprocess_alphablendextended_flagsspanspan-iddxva_videoprocess_substreamsextended_dxva_videoprocess_yuv2rgbextended_and_dxva_videoprocess_alphablendextended_flagsspanspan-iddxva_videoprocess_substreamsextended_dxva_videoprocess_yuv2rgbextended_and_dxva_videoprocess_alphablendextended_flagsspandxva_videoprocess_substreamsextended-dxva_videoprocess_yuv2rgbextended-and-dxva_videoprocess_alphablendextended-flags"></a><span id="DXVA_VideoProcess_SubStreamsExtended_DXVA_VideoProcess_YUV2RGBExtended_and_DXVA_VideoProcess_AlphaBlendExtended_flags"></span><span id="dxva_videoprocess_substreamsextended_dxva_videoprocess_yuv2rgbextended_and_dxva_videoprocess_alphablendextended_flags"></span><span id="DXVA_VIDEOPROCESS_SUBSTREAMSEXTENDED_DXVA_VIDEOPROCESS_YUV2RGBEXTENDED_AND_DXVA_VIDEOPROCESS_ALPHABLENDEXTENDED_FLAGS"></span>DXVA\_VideoProcess\_SubStreamsExtended DXVA\_VideoProcess\_YUV2RGBExtended および DXVA\_VideoProcess\_AlphaBlendExtended flags

[**DeinterlaceBltEx**](https://docs.microsoft.com/windows-hardware/drivers/display/dxva-deinterlacebobdeviceclass-deinterlacebltex)関数を実装するディスプレイドライバーでは、ソースとターゲットの各画面について、大幅に拡張された色情報をサポートできます。 ドライバーは、DXVA\_VideoProcess\_SubStreamsExtended、DXVA\_VideoProcess\_YUV2RGBExtended、および DXVA\_VideoProcess\_AlphaBlendExtended フラグを設定することによって、**このようなサポートを報告できます。** [**DXVA\_DeinterlaceCaps**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_deinterlacecaps)構造体の videoprocessingcaps メンバー。

DXVA\_VideoProcess\_SubStreamsExtended フラグのサポートは、表示ドライバーがソースビデオストリームおよびサブストリームに必要な色調整を実行できることを示します。 これらの調整は拡張カラーデータで示されています。ビデオは分割され、サブストリームと合成され、ターゲットサーフェスに書き込まれます。 拡張色データは、ソースサンプル配列の[**DXVA\_VideoSample2**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_videosample2)構造体の**Sampleformat**メンバーの[**DXVA\_extendedformat**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_extendedformat)構造体のメンバーによって指定されます (*lpDDSrcSurfaces*[**DeinterlaceBltEx**](https://docs.microsoft.com/windows-hardware/drivers/display/dxva-deinterlacebobdeviceclass-deinterlacebltex)呼び出しのパラメーター、または[**DXVA\_DeinterlaceBltEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_deinterlacebltex)構造体の**ソース**メンバー)。

DXVA\_VideoProcess\_YUV2RGBExtended フラグがサポートされていることは、deinterlaced および合成ピクセルがターゲットサーフェスに書き込まれるときに、表示ドライバーが色空間の変換操作を実行できることを示します。 RGB ターゲットサーフェイスがディスプレイドライバーに渡されると、VMR によって、各カラーチャネルに最低8ビットが含まれるようになります。 RGB のターゲットサーフェイスは、オフスクリーン、テクスチャ、または Direct3D レンダーターゲット、または結合されたテクスチャと Direct3D レンダーターゲットのサーフェス型になります。 VMR は、RGB ターゲットサーフェイスが使用されている場合でも、YUV 色空間の背景色パラメーターを引き続き指定します。

DXVA\_VideoProcess\_AlphaBlendExtended フラグのサポートは、deinterlaced および合成ピクセルが変換先に書き込まれるときに、表示ドライバーがターゲットサーフェスとのアルファブレンド操作を実行できることを示します。コーナー. ドライバーは、 [**DeinterlaceBltEx**](https://docs.microsoft.com/windows-hardware/drivers/display/dxva-deinterlacebobdeviceclass-deinterlacebltex)呼び出しの*fAlpha*パラメーターのアルファ値に基づいて背景色を処理する必要があります。 アルファ値が 1.0 f の場合、背景色は不透明 (透明度なし) で描画されます。 アルファ値が 0.0 f の場合、背景は描画されません (透明)。

 

 






---
title: DeinterlaceBltEx に対するサポートのレポート
description: DeinterlaceBltEx に対するサポートのレポート
ms.assetid: 9cf8d05c-ef59-44a4-a377-66282e7888d5
keywords:
- DeinterlaceBltEx、レポート作成
- DXVA_VideoProcess_SubStreamsExtended
- DXVA_VideoProcess_YUV2RGBExtended
- DXVA_VideoProcess_AlphaBlendExtended
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 914b8b97bce34b27790b581af8745583480940e2
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67364368"
---
# <a name="reporting-support-for-deinterlacebltex"></a>DeinterlaceBltEx に対するサポートのレポート


**このセクションでは、Windows Server 2003 SP1 以降、および Windows XP SP2 以降にのみ適用されます。**

ディスプレイ ドライバーのサポートの報告、 [ **DeinterlaceBltEx**](https://docs.microsoft.com/windows-hardware/drivers/display/dxva-deinterlacebobdeviceclass-deinterlacebltex)[DDI インター レースを解除](https://docs.microsoft.com/windows-hardware/drivers/display/deinterlace-ddi)するには、DXVA 関数\_VideoProcess\_サブストリーム、DXVA\_VideoProcess\_StretchX、および DXVA\_VideoProcess\_StretchY でフラグを設定、 **VideoProcessingCaps**のメンバー、 [**DXVA\_DeinterlaceCaps** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dxva/ns-dxva-_dxva_deinterlacecaps)構造体。 ドライバーは、DXVA にポインターを返します\_DeinterlaceCaps ときにその[ **DeinterlaceQueryModeCaps** ](https://docs.microsoft.com/windows-hardware/drivers/display/dxva-deinterlacecontainerdeviceclass-deinterlacequerymodecaps)関数が呼び出されます。

ディスプレイ ドライバー設定 DXVA\_VideoProcess\_ビデオを結合するサブストリーム サブストリームのインター レース解除が合成します。 ドライバー設定 DXVA\_VideoProcess\_StretchX と DXVA\_VideoProcess\_ビデオ ストリームとサブストリームのピクセル縦横比が異なると、非正方形を指定でき、ドライバーができる必要がありますので、可変幅。個別に拡張 (水平方向または垂直方向に)、ビデオ フレームを指定されたビデオ サブストリームとデインター レース用に送信されます。

DXVA\_VideoProcess\_YUV2RGB と DXVA\_VideoProcess\_AlphaBlend でフラグを設定、 **VideoProcessingCaps**のメンバー、 [ **DXVA\_DeinterlaceCaps** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dxva/ns-dxva-_dxva_deinterlacecaps)構造がある、ドライバーのコンテキストで意味ありません[ **DeinterlaceBltEx** ](https://docs.microsoft.com/windows-hardware/drivers/display/dxva-deinterlacebobdeviceclass-deinterlacebltex)関数。 これらのフラグは、元に関連[ **DeinterlaceBlt** ](https://docs.microsoft.com/windows-hardware/drivers/display/dxva-deinterlacebobdeviceclass-deinterlaceblt)関数。 ディスプレイ ドライバーをサポートするため、 *DeinterlaceBltEx*もサポートする必要があります*DeinterlaceBlt*のコンテキストでは、関連する操作をサポートしている場合、ドライバーはこれらのフラグを報告もする必要があります*DeinterlaceBlt*します。

### <a name="span-iddxvavideoprocesssubstreamsextendeddxvavideoprocessyuv2rgbextendedanddxvavideoprocessalphablendextendedflagsspanspan-iddxvavideoprocesssubstreamsextendeddxvavideoprocessyuv2rgbextendedanddxvavideoprocessalphablendextendedflagsspanspan-iddxvavideoprocesssubstreamsextendeddxvavideoprocessyuv2rgbextendedanddxvavideoprocessalphablendextendedflagsspandxvavideoprocesssubstreamsextended-dxvavideoprocessyuv2rgbextended-and-dxvavideoprocessalphablendextended-flags"></a><span id="DXVA_VideoProcess_SubStreamsExtended_DXVA_VideoProcess_YUV2RGBExtended_and_DXVA_VideoProcess_AlphaBlendExtended_flags"></span><span id="dxva_videoprocess_substreamsextended_dxva_videoprocess_yuv2rgbextended_and_dxva_videoprocess_alphablendextended_flags"></span><span id="DXVA_VIDEOPROCESS_SUBSTREAMSEXTENDED_DXVA_VIDEOPROCESS_YUV2RGBEXTENDED_AND_DXVA_VIDEOPROCESS_ALPHABLENDEXTENDED_FLAGS"></span>DXVA\_VideoProcess\_SubStreamsExtended DXVA\_VideoProcess\_YUV2RGBExtended と DXVA\_VideoProcess\_AlphaBlendExtended フラグ

実装しているディスプレイ ドライバー、 [ **DeinterlaceBltEx** ](https://docs.microsoft.com/windows-hardware/drivers/display/dxva-deinterlacebobdeviceclass-deinterlacebltex)関数は各ソースと宛先表面を大幅に強化された色の情報をサポートすることができます。 ドライバーは、このようなサポートを報告するには、DXVA\_VideoProcess\_SubStreamsExtended、DXVA\_VideoProcess\_YUV2RGBExtended、および DXVA\_VideoProcess\_AlphaBlendExtended でフラグを設定、 **VideoProcessingCaps**のメンバー、 [ **DXVA\_DeinterlaceCaps** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dxva/ns-dxva-_dxva_deinterlacecaps)構造体。

サポート、DXVA\_VideoProcess\_SubStreamsExtended フラグは、ディスプレイ ドライバーが、ソース ビデオ ストリームとサブストリームに必要な色の調整を実行できることを示します。 これらの調整は拡張カラー データの表示されたビデオは deinterlaced、サブストリームを合成し、宛先表面に書き込まれます。 メンバーで拡張カラー データが指定された、 [ **DXVA\_ExtendedFormat** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dxva/ns-dxva-_dxva_extendedformat)構造体、 **SampleFormat**のメンバー、 [ **DXVA\_VideoSample2** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dxva/ns-dxva-_dxva_videosample2)ソース サンプルの配列の構造 (*lpDDSrcSurfaces*パラメーター、 [ **DeinterlaceBltEx**](https://docs.microsoft.com/windows-hardware/drivers/display/dxva-deinterlacebobdeviceclass-deinterlacebltex)呼び出しまたは**ソース**のメンバー、 [ **DXVA\_DeinterlaceBltEx** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dxva/ns-dxva-_dxva_deinterlacebltex)構造)。

サポート、DXVA\_VideoProcess\_YUV2RGBExtended フラグは、ディスプレイ ドライバーは、deinterlaced と合成のピクセルが宛先表面に書き込まれる色空間の変換操作を実行できることを示します。 RGB の宛先表面が、ディスプレイ ドライバーに渡される場合、VMR は各カラー チャネルに 8 ビットの最小値が含まれているを確認します。 RGB の宛先表面のオフスクリーン、テクスチャでは、可能性がありますまたは Direct3D レンダー ターゲット、または結合のテクスチャと Direct3D レンダリング対象サーフェスの型。 RGB の宛先表面が使用されていて、VMR には、YUV 色空間で背景の色パラメーターでもを指定します。

サポート、DXVA\_VideoProcess\_AlphaBlendExtended フラグは、ディスプレイ ドライバーが deinterlaced と合成のピクセルが書き込む宛先表面のアルファ ブレンド操作を実行できることを示します、宛先表面。 ドライバーは、背景の色のアルファ値に基づいてを処理する必要があります、 *fAlpha*パラメーター、 [ **DeinterlaceBltEx** ](https://docs.microsoft.com/windows-hardware/drivers/display/dxva-deinterlacebobdeviceclass-deinterlacebltex)呼び出します。 アルファ値が、1.0 f、背景色は透明度) (なし不透明に描画します。 アルファ値が 0.0 f の場合は、バック グラウンドする必要がありますは描画されません (透明)。

 

 






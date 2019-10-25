---
title: ビデオ サブストリームおよび宛先サーフェスの提供
description: ビデオ サブストリームおよび宛先サーフェスの提供
ms.assetid: 53528c49-11d1-4e53-b700-f6d8d760bcfe
keywords:
- DeinterlaceBltEx、ターゲットサーフェス
- DeinterlaceBltEx、サブストリームのサーフェス
- ターゲットサーフェスの WDK DirectX VA
- サブストリームサーフェイスの WDK DirectX VA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f0112f8d13f91488d66d0a7bff383a3f42a74695
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72825704"
---
# <a name="supplying-video-substream-and-destination-surfaces"></a>ビデオ サブストリームおよび宛先サーフェスの提供


## <span id="ddk_supplying_video_substream_and_destination_surfaces_gg"></span><span id="DDK_SUPPLYING_VIDEO_SUBSTREAM_AND_DESTINATION_SURFACES_GG"></span>


**このセクションは、Windows Server 2003 SP1 以降、および Windows XP SP2 以降にのみ適用されます。**

Windows Server 2003 SP1 以降および Windows XP SP2 以降の VMR は、DXVA がサポートするサブストリーム形式のビデオサブストリームのみを提供します。 つまり、VMR は、アルファブレンドのサブストリーム (AI44、IA44、または AYUV) に対して次の*FOURCC*コードのみを提供します。 詳細については、「、 [AYUV のアルファブレンドサーフェイスの読み込み](loading-an-ayuv-alpha-blending-surface.md)」を参照してください。 複数のビデオサブストリームを指定すると、各サブストリームの形式が異なる場合があることに注意してください。 指定されたビデオサブストリームの形式はパレット surface 形式であるため、各サーフェイスの完全な16色パレットは、DXVA で渡される配列内の各[ **\_VideoSample2**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_videosample2)構造体の**パレット**メンバーに指定されます。*DeinterlaceBltEx*が呼び出されるときの*Pddsrcsurfaces*パラメーター。 このため、各ビデオサブストリーム画面のパレット情報を保持するためにドライバーは必要ありません。

また、VMR は、 [**DXVA\_DeinterlaceCaps**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_deinterlacecaps)構造体の**d3dOutputFormat**メンバーのドライバーによって指定された形式を持つターゲットサーフェスだけを提供します。 このドライバーは、 [**DeinterlaceQueryModeCaps**](https://docs.microsoft.com/windows-hardware/drivers/display/dxva-deinterlacecontainerdeviceclass-deinterlacequerymodecaps)関数が呼び出されたときに、DXVA\_DeinterlaceCaps へのポインターを返します。

 

 






---
title: ビデオ サブストリームおよび宛先サーフェスの提供
description: ビデオ サブストリームおよび宛先サーフェスの提供
ms.assetid: 53528c49-11d1-4e53-b700-f6d8d760bcfe
keywords:
- DeinterlaceBltEx、宛先表面
- DeinterlaceBltEx、サブストリーム サーフェス
- 移行先サーフェスの WDK DirectX VA
- サブストリームのサーフェス WDK DirectX VA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 07753e6988ece51c5eb7476b08ac03891c8f45c0
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67353830"
---
# <a name="supplying-video-substream-and-destination-surfaces"></a>ビデオ サブストリームおよび宛先サーフェスの提供


## <span id="ddk_supplying_video_substream_and_destination_surfaces_gg"></span><span id="DDK_SUPPLYING_VIDEO_SUBSTREAM_AND_DESTINATION_SURFACES_GG"></span>


**このセクションでは、Windows Server 2003 SP1 以降、および Windows XP SP2 以降にのみ適用されます。**

VMR Windows Server 2003 SP1 以降および Windows XP SP2 と後でのみ提供ビデオ サブストリーム DXVA をサポートするサブストリーム画面形式を使用します。 つまり、VMR でのみ、次が提供*FOURCC*サブストリーム画面形式のアルファ ブレンドのコード。AI44、IA44 または AYUV します。 詳細については、次を参照してください。 [、AYUV アルファ ブレンドの画面を読み込み](loading-an-ayuv-alpha-blending-surface.md)します。 複数のビデオ サブストリームが指定したときに各サブストリームが別の形式に注意してください。 それぞれの面の完全な 16 色のパレットがで指定した指定されたビデオ サブストリームの形式は、パレットのサーフェスの形式であるため、**パレット**のそれぞれに所属[ **DXVA\_VideoSample2** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dxva/ns-dxva-_dxva_videosample2)で渡される配列内の構造、 *pDDSrcSurfaces*パラメーターと*DeinterlaceBltEx*が呼び出されます。 そのため、ドライバーでは、各ビデオ サブストリーム サーフェスのパレットの情報を保持する必要はありません。

VMR ものみでドライバーが指定した書式の宛先表面を提供、 **d3dOutputFormat**のメンバー、 [ **DXVA\_DeinterlaceCaps** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dxva/ns-dxva-_dxva_deinterlacecaps)構造体。 ドライバーは、DXVA にポインターを返します\_DeinterlaceCaps ときにその[ **DeinterlaceQueryModeCaps** ](https://docs.microsoft.com/windows-hardware/drivers/display/dxva-deinterlacecontainerdeviceclass-deinterlacequerymodecaps)関数が呼び出されます。

 

 






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
ms.openlocfilehash: c9acc2fe84ac85ee53f80cd9f2dd4754257be911
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63375912"
---
# <a name="supplying-video-substream-and-destination-surfaces"></a>ビデオ サブストリームおよび宛先サーフェスの提供


## <span id="ddk_supplying_video_substream_and_destination_surfaces_gg"></span><span id="DDK_SUPPLYING_VIDEO_SUBSTREAM_AND_DESTINATION_SURFACES_GG"></span>


**このセクションでは、Windows Server 2003 SP1 以降、および Windows XP SP2 以降にのみ適用されます。**

VMR Windows Server 2003 SP1 以降および Windows XP SP2 と後でのみ提供ビデオ サブストリーム DXVA をサポートするサブストリーム画面形式を使用します。 つまり、VMR でのみ、次が提供*FOURCC*サブストリーム画面形式のアルファ ブレンドのコード。AI44、IA44 または AYUV します。 詳細については、次を参照してください。 [、AYUV アルファ ブレンドの画面を読み込み](loading-an-ayuv-alpha-blending-surface.md)します。 複数のビデオ サブストリームが指定したときに各サブストリームが別の形式に注意してください。 それぞれの面の完全な 16 色のパレットがで指定した指定されたビデオ サブストリームの形式は、パレットのサーフェスの形式であるため、**パレット**のそれぞれに所属[ **DXVA\_VideoSample2** ](https://msdn.microsoft.com/library/windows/hardware/ff564092)で渡される配列内の構造、 *pDDSrcSurfaces*パラメーターと*DeinterlaceBltEx*が呼び出されます。 そのため、ドライバーでは、各ビデオ サブストリーム サーフェスのパレットの情報を保持する必要はありません。

VMR ものみでドライバーが指定した書式の宛先表面を提供、 **d3dOutputFormat**のメンバー、 [ **DXVA\_DeinterlaceCaps** ](https://msdn.microsoft.com/library/windows/hardware/ff563939)構造体。 ドライバーは、DXVA にポインターを返します\_DeinterlaceCaps ときにその[ **DeinterlaceQueryModeCaps** ](https://msdn.microsoft.com/library/windows/hardware/ff563946)関数が呼び出されます。

 

 






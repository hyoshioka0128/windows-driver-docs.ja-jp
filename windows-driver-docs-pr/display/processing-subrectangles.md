---
title: サブ矩形の処理
description: サブ矩形の処理
ms.assetid: d00803c0-98e2-4101-bcfc-ef11fea07962
keywords:
- デインター レース WDK DirectX va なので、subrectangular 処理
- subrectangular 処理 WDK DirectX VA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6e50070bbba1ad2303dde2eedf6b84dbd5ddf428
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67363703"
---
# <a name="processing-subrectangles"></a>サブ矩形の処理


## <span id="ddk_processing_subrectangles_gg"></span><span id="DDK_PROCESSING_SUBRECTANGLES_GG"></span>


**このセクションでは、Windows Server 2003 SP1 以降、および Windows XP SP2 以降にのみ適用されます。**

Windows XP SP2、Windows Server 2003 SP1 以降の VMR し、後で、ソース ビデオ画像とビデオのサブストリームの subrectangular 領域を処理できるし、宛先表面上 subrectangular 領域に書き込むことができます。 VMR 内の四角形の座標を subrectangular プロセス操作を実行する、 **rcSrc**と**rcDest**のメンバー、 [ **DXVA\_VideoSample2** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dxva/ns-dxva-_dxva_videosample2)各サンプルのソースと宛先表面の座標から別の構造体。

インター ハードウェア subrectangular 処理操作をサポートする場合、ディスプレイ ドライバーは、DXVA を設定してこのサポートを報告\_VideoProcess\_SubRects フラグ、 **VideoProcessingCaps**メンバー[ **DXVA\_DeinterlaceCaps** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dxva/ns-dxva-_dxva_deinterlacecaps)構造体。 ドライバーは、DXVA にポインターを返します\_DeinterlaceCaps ときにその[ **DeinterlaceQueryModeCaps** ](https://docs.microsoft.com/windows-hardware/drivers/display/dxva-deinterlacecontainerdeviceclass-deinterlacequerymodecaps)関数が呼び出されます。

Subrectangular プロセスの操作で VMR subrectangles を拡張でき、宛先表面上で相互 subrectangles が交差することができます。

次のトピックでは、各種 subrectangular プロセス操作を実行する方法を示します。

[拡張せず Subrectangles の処理](processing-subrectangles-without-stretching.md)

[伸縮 Subrectangles](stretching-subrectangles.md)

 

 






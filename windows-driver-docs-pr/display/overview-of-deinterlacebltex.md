---
title: DeinterlaceBltEx の概要
description: DeinterlaceBltEx の概要
ms.assetid: ff487508-eb04-4d4d-9057-ed2d9ea273e0
keywords:
- DeinterlaceBltEx、DeinterlaceBltEx について
- VMR WDK DirectX VA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9fb365fdd19804999ad82ccc14cd3983d22843be
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67354695"
---
# <a name="overview-of-deinterlacebltex"></a>DeinterlaceBltEx の概要


## <span id="ddk_overview_of_deinterlacebltex_gg"></span><span id="DDK_OVERVIEW_OF_DEINTERLACEBLTEX_GG"></span>


**このセクションでは、Windows Server 2003 SP1 以降、および Windows XP SP2 以降にのみ適用されます。**

Windows XP SP2、Windows Server 2003 SP1 以降の VMR し、後で、ディスプレイ ドライバーへの呼び出しを開始することができます[ **DeinterlaceBltEx** ](https://docs.microsoft.com/windows-hardware/drivers/display/dxva-deinterlacebobdeviceclass-deinterlacebltex)デインター レースを結合してサブストリームの合成関数操作です。

Windows Server 2003 と Windows XP SP1 VMR DXVA を使用してインター レース解除するか、フレーム レートがビデオ、および、RGB32 表面にビデオ出力に変換します。 VMR は、Direct3D を使用してビデオ画像とビデオ サブストリームを結合します。 つまり、ビデオは、まず deinterlaced、サイズ変更、および色空間 Direct3D RGB32 に変換をレンダリングする、ディスプレイ ドライバーを使用してターゲット[ **DeinterlaceBlt** ](https://docs.microsoft.com/windows-hardware/drivers/display/dxva-deinterlacebobdeviceclass-deinterlaceblt)関数。 次に、ビデオのサブストリームが合成ディスプレイ ドライバーへの呼び出しを使用して、結果として得られるビデオ画像の上に[ **D3dDrawPrimitives2** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dhal/nc-d3dhal-lpd3dhal_drawprimitives2cb)関数。

使用して*DeinterlaceBltEx*なく*DeinterlaceBlt*と*D3dDrawPrimitives2*組み合わせることで、操作を実行できるより効率的に使用可能なハードウェアで.

*DeinterlaceBltEx*関数も呼び出せるプログレッシブ ビデオや複数のビデオ サブストリームとします。 このシナリオは、VMR が段階的なインター レースのビデオの組み合わせを含む DVD の再生に使用される場合に発生します。 ここでは、ドライバーは、ストリームはプログレッシブが既にあるため、ビデオ ストリームをインター レース解除する必要がありますしません。 ドライバーは、任意指定サブストリームとビデオ ストリームを結合し、必要に応じて、各ストリームのサイズを変更する必要があります。

実装する場合、 [ **DeinterlaceBltEx** ](https://docs.microsoft.com/windows-hardware/drivers/display/dxva-deinterlacebobdeviceclass-deinterlacebltex)関数、ドライバーでは、元も実装する必要があります[ **DeinterlaceBlt** ](https://docs.microsoft.com/windows-hardware/drivers/display/dxva-deinterlacebobdeviceclass-deinterlaceblt)関数。 VMR 以降では、Windows Server 2003 SP1 および Windows XP SP2 以降できます開始呼び出していずれかに、ドライバーの*DeinterlaceBltEx*または*DeinterlaceBlt*関数は、アプリケーションを制御しますVMR を使用する関数。

 

 






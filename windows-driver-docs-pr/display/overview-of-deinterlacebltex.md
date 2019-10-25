---
title: DeinterlaceBltEx の概要
description: DeinterlaceBltEx の概要
ms.assetid: ff487508-eb04-4d4d-9057-ed2d9ea273e0
keywords:
- DeinterlaceBltEx、DeinterlaceBltEx について
- VMR WDK DirectX VA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: fa0caa7581add3753a3272aa1d8bdc5f08c123a4
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72826065"
---
# <a name="overview-of-deinterlacebltex"></a>DeinterlaceBltEx の概要


## <span id="ddk_overview_of_deinterlacebltex_gg"></span><span id="DDK_OVERVIEW_OF_DEINTERLACEBLTEX_GG"></span>


**このセクションは、Windows Server 2003 SP1 以降、および Windows XP SP2 以降にのみ適用されます。**

Windows Server 2003 SP1 以降および Windows XP SP2 以降の VMR では、表示ドライバーの[**DeinterlaceBltEx**](https://docs.microsoft.com/windows-hardware/drivers/display/dxva-deinterlacebobdeviceclass-deinterlacebltex)関数の呼び出しを開始して、ノンインターレース化とサブストリームの合成操作を組み合わせることができます。

Windows Server 2003 および Windows XP SP1 の VMR では、DXVA を使用してビデオをインターレース解除またはフレームレート変換し、ビデオを RGB32 表面に出力します。 VMR は、Direct3D を使用してビデオのサブストリームをビデオイメージと結合します。 つまり、ビデオはまず、ディスプレイドライバーの[**DeinterlaceBlt**](https://docs.microsoft.com/windows-hardware/drivers/display/dxva-deinterlacebobdeviceclass-deinterlaceblt)関数を使用して、最初にインターレースを解除し、サイズを変更した後、カラースペースを Direct3D RGB32 render ターゲットに変換します。 次に、ビデオサブストリームは、表示ドライバーの[**D3dDrawPrimitives2**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dhal/nc-d3dhal-lpd3dhal_drawprimitives2cb)関数の呼び出しを使用して、結果として得られるビデオイメージの上部に合成されます。

*DeinterlaceBlt*と*D3dDrawPrimitives2*の組み合わせではなく、 *DeinterlaceBltEx*を使用すると、利用可能なハードウェアで操作をより効率的に実行できます。

*DeinterlaceBltEx*関数は、プログレッシブビデオと複数のビデオサブストリームでも呼び出すことができます。 このシナリオは、プログレッシブビデオとインターレースビデオの組み合わせを含む DVD 再生に VMR が使用されている場合に発生する可能性があります。 この場合、ストリームは既にプログレッシブであるため、ドライバーはビデオストリームのインターレースを解除しないようにする必要があります。 ドライバーは、ビデオストリームと特定のサブストリームを結合し、必要に応じて各ストリームのサイズを変更します。

ドライバーで[**DeinterlaceBltEx**](https://docs.microsoft.com/windows-hardware/drivers/display/dxva-deinterlacebobdeviceclass-deinterlacebltex)関数を実装する場合は、元の[**DeinterlaceBlt**](https://docs.microsoft.com/windows-hardware/drivers/display/dxva-deinterlacebobdeviceclass-deinterlaceblt)関数も実装する必要があります。 Windows Server 2003 SP1 以降および Windows XP SP2 以降の VMR では、ドライバーの*DeinterlaceBltEx*または*DeinterlaceBlt*関数の呼び出しを開始できます。アプリケーションでは、VMR が使用する機能を制御します。

 

 






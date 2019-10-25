---
title: Direct3D での浮動小数点演算の実行
description: Direct3D での浮動小数点演算の実行
ms.assetid: 2da736cf-d062-4c5a-b9f5-6b35f199660f
keywords:
- 浮動小数点演算の WDK Direct3D
- Direct3D WDK Windows 2000 display、浮動小数点演算
- コールバック関数 WDK Direct3D
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: db2831bbcc0b39193a3e496b07ecdec2bd0810b4
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72829807"
---
# <a name="performing-floating-point-operations-in-direct3d"></a>Direct3D での浮動小数点演算の実行


## <span id="ddk_performing_floating_point_operations_in_direct3d_gg"></span><span id="DDK_PERFORMING_FLOATING_POINT_OPERATIONS_IN_DIRECT3D_GG"></span>


DirectX ランタイムは、ディスプレイドライバーの Direct3D コールバック関数の多くを呼び出すときに、浮動小数点の状態を保存して復元します。 ただし、「 [DirectDraw での浮動小数点演算の実行](performing-floating-point-operations-in-directdraw.md)」で説明されているように、一部のドライバーの Direct3D コールバック関数では、浮動小数点演算を実行する前に浮動小数点の状態を保存する必要があり、操作が完了しました。

DirectX ランタイムは、次の Direct3D コールバック関数のために必要に応じて、浮動小数点の状態を保存および復元します。

-   [**D3dContextCreate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dhal/nc-d3dhal-lpd3dhal_contextcreatecb)

-   [**D3dContextDestroy**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dhal/nc-d3dhal-lpd3dhal_contextdestroycb)

-   [**D3dDrawPrimitives2**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dhal/nc-d3dhal-lpd3dhal_drawprimitives2cb)

-   [**D3dGetDriverState**](https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_getdriverstate)

-   [**D3dValidateTextureStageState**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dhal/nc-d3dhal-lpd3dhal_validatetexturestagestatecb)

次のコールバック関数では、Direct3D でサポートされているディスプレイドライバーは、浮動小数点演算を実行する前に浮動小数点の状態を保存し、操作が完了したときに復元する必要があります。

-   [**D3dCreateSurfaceEx**](https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_createsurfaceex)

-   [**D3dDestroyDDLocal**](https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_destroyddlocal)

-   [D3DBuffer コールバック](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)

浮動小数点演算の詳細については、「[グラフィックスドライバー関数の浮動小数点演算](floating-point-operations-in-graphics-driver-functions.md)」を参照してください。

 

 






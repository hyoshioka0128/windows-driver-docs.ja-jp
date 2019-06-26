---
title: Direct3D での浮動小数点演算の実行
description: Direct3D での浮動小数点演算の実行
ms.assetid: 2da736cf-d062-4c5a-b9f5-6b35f199660f
keywords:
- 浮動小数点演算 WDK Direct3D
- Direct3D WDK Windows 2000 の表示、浮動小数点演算
- WDK Direct3D のコールバック関数
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2b03562a8985692edeee5fd8c057cf72005a7126
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67385583"
---
# <a name="performing-floating-point-operations-in-direct3d"></a>Direct3D での浮動小数点演算の実行


## <span id="ddk_performing_floating_point_operations_in_direct3d_gg"></span><span id="DDK_PERFORMING_FLOATING_POINT_OPERATIONS_IN_DIRECT3D_GG"></span>


DirectX のランタイムでは、保存し、多くのディスプレイ ドライバーの Direct3D のコールバック関数を呼び出すときに、浮動小数点状態を復元します。 ただし、」の説明に従って[DirectDraw で浮動小数点演算の実行](performing-floating-point-operations-in-directdraw.md)、浮動小数点演算を実行する前に、浮動小数点状態を保存する必要がありますいくつかのドライバーの Direct3D のコールバック関数、および復元する必要があります操作の完了時の浮動小数点の状態。

DirectX のランタイムでは、保存し、Direct3D の次のコールバック関数の必要に応じて浮動小数点状態の復元します。

-   [**D3dContextCreate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dhal/nc-d3dhal-lpd3dhal_contextcreatecb)

-   [**D3dContextDestroy**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dhal/nc-d3dhal-lpd3dhal_contextdestroycb)

-   [**D3dDrawPrimitives2**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dhal/nc-d3dhal-lpd3dhal_drawprimitives2cb)

-   [**D3dGetDriverState**](https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_getdriverstate)

-   [**D3dValidateTextureStageState**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dhal/nc-d3dhal-lpd3dhal_validatetexturestagestatecb)

次のコールバック関数では、Direct3D でサポートされているディスプレイ ドライバーする必要があります、浮動小数点の操作を実行する前に浮動小数点状態を保存して復元する操作が完了する.

-   [**D3dCreateSurfaceEx**](https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_createsurfaceex)

-   [**D3dDestroyDDLocal**](https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_destroyddlocal)

-   [D3DBuffer コールバック](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/index)

浮動小数点演算の詳細については、次を参照してください。[グラフィックス ドライバー関数での浮動小数点操作](floating-point-operations-in-graphics-driver-functions.md)します。

 

 






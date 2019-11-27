---
title: メモリ割り当てのサイズおよびピッチの設定
description: メモリ割り当てのサイズおよびピッチの設定
ms.assetid: babd331f-7aec-4aee-aef9-7c10b98f9181
keywords:
- メモリ割り当て WDK ディスプレイ
- メモリの割り当て WDK 表示
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3437ad0257932ac02b7893c19cf14ac0d0e5a46e
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72829495"
---
# <a name="setting-the-size-and-pitch-of-the-memory-allocation"></a>メモリ割り当てのサイズおよびピッチの設定


## <span id="ddk_introduction_to_command_and_dma_buffers_gg"></span><span id="DDK_INTRODUCTION_TO_COMMAND_AND_DMA_BUFFERS_GG"></span>


GDI ハードウェアアクセラレーションをサポートするディスプレイミニポートドライバーは、次の割り当て呼び出しを処理するときに、システムまたはビデオメモリの割り当てのサイズとピッチを設定する必要があります。

<span id="DxgkDdiCreateAllocation"></span><span id="dxgkddicreateallocation"></span><span id="DXGKDDICREATEALLOCATION"></span>[**DxgkDdiCreateAllocation**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_createallocation)  
ドライバーが*DxgkDdiCreateAllocation*の呼び出しを処理するときに、システムまたはビデオメモリの割り当てのサイズをバイト単位で設定する必要があります。 割り当てのサイズは、 [**Pcreateallocation**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/ns-d3dkmddi-_dxgkarg_createallocation) *-&gt;* [](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/ns-d3dkmddi-_dxgk_allocationinfo) 、<em>-&gt;</em> **size**メンバーによって設定されます。 割り当てが CPU に表示される場合、サイズには、余白を含む、画面の幅であるピッチ値 (バイト単位) を含める必要があります。

[**PgetstandardpCreateGdiSurfaceData Driverdata**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/ns-d3dkmddi-_dxgkarg_getstandardallocationdriverdata) *-* &gt;[](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmdt/ns-d3dkmdt-_d3dkmdt_gdisurfacedata) <em>-&gt;</em> **Type**メンバーが D3DKMDT に設定されている場合は、割り当てが CPU から表示されます。 D3DKMDT は、gdisurface\_ステージング\_cpu VISIBLE または\_gdisurface\_EXISTINGSYSMEM に設定されます。\_ これらのサーフェスの種類のプロパティについては、 [**D3DKMDT\_GDISURFACETYPE**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmdt/ne-d3dkmdt-_d3dkmdt_gdisurfacetype)の説明を参照してください。

<span id="DxgkDdiGetStandardAllocationDriverData"></span><span id="dxgkddigetstandardallocationdriverdata"></span><span id="DXGKDDIGETSTANDARDALLOCATIONDRIVERDATA"></span>[**DxgkDdiGetStandardAllocationDriverData**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_getstandardallocationdriverdata)  
ドライバーが、CPU から参照できる割り当てに対して*DxgkDdiGetStandardAllocationDriverData*の呼び出しを処理する場合、次のことを行う必要があります。

1.  [**Pgetstandardallocation Driverdata**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/ns-d3dkmddi-_dxgkarg_getstandardallocationdriverdata) *-* &gt;[**STANDARDの種類**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmdt/ne-d3dkmdt-_d3dkmdt_standardallocation_type)のメンバーを D3DKMDT\_standardallocation\_gdisurface に設定します。

2.  GDI ハードウェアアクセラレータとデスクトップ Windows マネージャー (DWM) によるリダイレクトに使用できるサーフェイスの説明を設定します。これには、 [**PgetstandardGDISURFACEDATA D3DKMDT データ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/ns-d3dkmddi-_dxgkarg_getstandardallocationdriverdata) *-* &gt;**pCreateGdiSurfaceData**メンバーによってポイントされている[ **\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmdt/ns-d3dkmdt-_d3dkmdt_gdisurfacedata)構造体が使用されます。 たとえば、D3DKMDT\_GDISURFACEDATA の**ピッチ**メンバーを通じて、割り当てのピッチを設定します。

 

 






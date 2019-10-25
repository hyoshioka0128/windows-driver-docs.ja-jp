---
title: 遅延コンテキストの DDI 関数の除外
description: 遅延コンテキストの DDI 関数の除外
ms.assetid: f6e7898a-7fb8-4a70-ab2e-3372a28db6f4
keywords:
- Direct3D バージョン 11 WDK Windows 7 の表示、遅延コンテキスト、DDI 関数を除く
- Direct3D バージョン 11 WDK Windows Server 2008 R2 の表示、遅延コンテキスト、DDI 関数の除外
- 遅延コンテキスト WDK Windows 7 ディスプレイ (DDI 関数を除く)
- 遅延コンテキスト WDK Windows Server 2008 R2 表示 (DDI 関数を除く)
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3f572f85efdad974bbb20415498a31c688d59ad5
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72839701"
---
# <a name="excluding-ddi-functions-for-deferred-contexts"></a>遅延コンテキストの DDI 関数の除外


このセクションは、windows 7 以降、および windows Server 2008 R2 以降のバージョンの Windows オペレーティングシステムにのみ適用されます。

Microsoft Direct3D ランタイムが、遅延コンテキストを作成するためにユーザーモードの表示ドライバーの[**CreateDeferredContext**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d11ddi_createdeferredcontext)関数を呼び出すと、その遅延コンテキストに対してランタイムが呼び出すことができる関数がドライバーによって提供されます。 このドライバーは、 [**D3D11DDIARG\_CREATEDEFERREDCONTEXT**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/ns-d3d10umddi-d3d11ddiarg_createdeferredcontext)構造体の**p11ContextFuncs**メンバーが指す[**D3D11DDI\_devicefuncs**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/ns-d3d10umddi-d3d11ddi_devicefuncs)構造体のメンバーになります。 ドライバーは、ドライバーが直接コンテキストを処理するので、遅延コンテキストに対して関数のサブセットのみを提供します。

ドライバーは、 [**D3D11DDI\_devicefuncs**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/ns-d3d10umddi-d3d11ddi_devicefuncs)または[**D3D11\_1ddi\_devicefuncs**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/ns-d3d10umddi-d3d11_1ddi_devicefuncs)の次のメンバーを**NULL**に設定することによって、遅延コンテキスト用の多くの関数を除外します。

```cpp
typedef struct D3D11DDI_DEVICEFUNCS {
...
  PFND3D10DDI_RESOURCEMAP  pfnStagingResourceMap;
  PFND3D10DDI_RESOURCEUNMAP  pfnStagingResourceUnmap;
  PFND3D10DDI_QUERYGETDATA  pfnQueryGetData;
  PFND3D10DDI_FLUSH  pfnFlush;
  PFND3D10DDI_RESOURCEMAP  pfnResourceMap;
  PFND3D10DDI_RESOURCEUNMAP  pfnResourceUnmap;
  PFND3D10DDI_RESOURCEISSTAGINGBUSY  pfnResourceIsStagingBusy;
  PFND3D11DDI_CALCPRIVATERESOURCESIZE  pfnCalcPrivateResourceSize;
  PFND3D10DDI_CALCPRIVATEOPENEDRESOURCESIZE  pfnCalcPrivateOpenedResourceSize;
  PFND3D10DDI_OPENRESOURCE  fnOpenResource;
  PFND3D11DDI_CALCPRIVATESHADERRESOURCEVIEWSIZE  pfnCalcPrivateShaderResourceViewSize;
  PFND3D10DDI_CALCPRIVATERENDERTARGETVIEWSIZE  pfnCalcPrivateRenderTargetViewSize;
  PFND3D11DDI_CALCPRIVATEDEPTHSTENCILVIEWSIZE  pfnCalcPrivateDepthStencilViewSize;
  PFND3D10DDI_CALCPRIVATEELEMENTLAYOUTSIZE  pfnCalcPrivateElementLayoutSize;
  PFND3D10_1DDI_CALCPRIVATEBLENDSTATESIZE  pfnCalcPrivateBlendStateSize;
  PFND3D10DDI_CALCPRIVATEDEPTHSTENCILSTATESIZE  pfnCalcPrivateDepthStencilStateSize;
  PFND3D10DDI_CALCPRIVATERASTERIZERSTATESIZE  pfnCalcPrivateRasterizerStateSize;
  PFND3D10DDI_CALCPRIVATESHADERSIZE  pfnCalcPrivateShaderSize;
  PFND3D11DDI_CALCPRIVATEGEOMETRYSHADERWITHSTREAMOUTPUT  pfnCalcPrivateGeometryShaderWithStreamOutput;
  PFND3D10DDI_CALCPRIVATESAMPLERSIZE  pfnCalcPrivateSamplerSize;
  PFND3D10DDI_CALCPRIVATEQUERYSIZE  pfnCalcPrivateQuerySize;
  PFND3D10DDI_CHECKFORMATSUPPORT  pfnCheckFormatSupport;
  PFND3D10DDI_CHECKMULTISAMPLEQUALITYLEVELS  pfnCheckMultisampleQualityLevels;
  PFND3D10DDI_CHECKCOUNTERINFO  pfnCheckCounterInfo;
  PFND3D10DDI_CHECKCOUNTER  pfnCheckCounter;
  PFND3D11DDI_CHECKDEFERREDCONTEXTHANDLESIZES  pfnCheckDeferredContextHandleSizes;
  PFND3D11DDI_CALCDEFERREDCONTEXTHANDLESIZE  pfnCalcDeferredContextHandleSize;
  PFND3D11DDI_CALCPRIVATEDEFERREDCONTEXTSIZE  pfnCalcPrivateDeferredContextSize;
  PFND3D11DDI_CREATEDEFERREDCONTEXT  pfnCreateDeferredContext;
  PFND3D11DDI_CALCPRIVATECOMMANDLISTSIZE  pfnCalcPrivateCommandListSize;
  PFND3D11DDI_CALCPRIVATETESSELLATIONSHADERSIZE  pfnCalcPrivateTessellationShaderSize;
  PFND3D11DDI_CALCPRIVATEUNORDEREDACCESSVIEWSIZE  pfnCalcPrivateUnorderedAccessViewSize;
  PFND3D11DDI_SETRESOURCEMINLOD  pfnSetResourceMinLOD;
} D3D11DDI_DEVICEFUNCS;
```

```cpp
typedef struct D3D11_1DDI_DEVICEFUNCS {
...
  PFND3D10DDI_RESOURCEMAP  pfnStagingResourceMap;
  PFND3D10DDI_RESOURCEUNMAP  pfnStagingResourceUnmap;
  PFND3D10DDI_QUERYGETDATA  pfnQueryGetData;
  PFND3D11_1DDI_FLUSH  pfnFlush;
  PFND3D10DDI_RESOURCEMAP  pfnResourceMap;
  PFND3D10DDI_RESOURCEUNMAP  pfnResourceUnmap;
  PFND3D10DDI_RESOURCEISSTAGINGBUSY  pfnResourceIsStagingBusy;
  PFND3D11DDI_CALCPRIVATERESOURCESIZE  pfnCalcPrivateResourceSize;
  PFND3D10DDI_CALCPRIVATEOPENEDRESOURCESIZE  pfnCalcPrivateOpenedResourceSize;
  PFND3D10DDI_OPENRESOURCE  fnOpenResource;
  PFND3D11DDI_CALCPRIVATESHADERRESOURCEVIEWSIZE  pfnCalcPrivateShaderResourceViewSize;
  PFND3D10DDI_CALCPRIVATERENDERTARGETVIEWSIZE  pfnCalcPrivateRenderTargetViewSize;
  PFND3D11DDI_CALCPRIVATEDEPTHSTENCILVIEWSIZE  pfnCalcPrivateDepthStencilViewSize;
  PFND3D10DDI_CALCPRIVATEELEMENTLAYOUTSIZE  pfnCalcPrivateElementLayoutSize;
  PFND3D11_1DDI_CALCPRIVATEBLENDSTATESIZE  pfnCalcPrivateBlendStateSize;
  PFND3D10DDI_CALCPRIVATEDEPTHSTENCILSTATESIZE  pfnCalcPrivateDepthStencilStateSize;
  PFND3D11_1DDI_CALCPRIVATERASTERIZERSTATESIZE  pfnCalcPrivateRasterizerStateSize;
  PFND3D11_1DDI_CALCPRIVATESHADERSIZE  pfnCalcPrivateShaderSize;
  PFND3D11_1DDI_CALCPRIVATEGEOMETRYSHADERWITHSTREAMOUTPUT  pfnCalcPrivateGeometryShaderWithStreamOutput;
  PFND3D10DDI_CALCPRIVATESAMPLERSIZE  pfnCalcPrivateSamplerSize;
  PFND3D10DDI_CALCPRIVATEQUERYSIZE  pfnCalcPrivateQuerySize;
  PFND3D10DDI_CHECKFORMATSUPPORT  pfnCheckFormatSupport;
  PFND3D10DDI_CHECKMULTISAMPLEQUALITYLEVELS  pfnCheckMultisampleQualityLevels;
  PFND3D10DDI_CHECKCOUNTERINFO  pfnCheckCounterInfo;
  PFND3D10DDI_CHECKCOUNTER  pfnCheckCounter;
  PFND3D11DDI_CHECKDEFERREDCONTEXTHANDLESIZES  pfnCheckDeferredContextHandleSizes;
  PFND3D11DDI_CALCDEFERREDCONTEXTHANDLESIZE  pfnCalcDeferredContextHandleSize;
  PFND3D11DDI_CALCPRIVATEDEFERREDCONTEXTSIZE  pfnCalcPrivateDeferredContextSize;
  PFND3D11DDI_CREATEDEFERREDCONTEXT  pfnCreateDeferredContext;
  PFND3D11DDI_CALCPRIVATECOMMANDLISTSIZE  pfnCalcPrivateCommandListSize;
  PFND3D11_1DDI_CALCPRIVATETESSELLATIONSHADERSIZE  pfnCalcPrivateTessellationShaderSize;
  PFND3D11DDI_CALCPRIVATEUNORDEREDACCESSVIEWSIZE  pfnCalcPrivateUnorderedAccessViewSize;
  PFND3D11DDI_SETRESOURCEMINLOD  pfnSetResourceMinLOD;
} D3D11DDI_DEVICEFUNCS;
```

 

 






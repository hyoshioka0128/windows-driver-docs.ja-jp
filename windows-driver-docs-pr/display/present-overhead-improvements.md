---
title: 現在のオーバーヘッドの改善
ms.assetid: 92B282D6-0D04-4352-AE03-E0A7A43711E7
description: GPU 処理の負荷を軽減するための内部スワップバッファーの機能強化
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e158d0fdff1c1a5ab75bca334c4e73b233f3f067
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72829714"
---
# <a name="present-overhead-improvements"></a>現在のオーバーヘッドの改善


Windows 8.1 以降では、Microsoft Direct3D ランタイムが内部スワップバッファーをより効率的に処理し、GPU の処理負荷を軽減します。 このパフォーマンスを向上させるために、Windows Display Driver Model (WDDM) 1.3 以降のドライバーでは、新しい現在の device Driver interface (DDI) と新しいテクスチャ形式を共有サーフェスとしてサポートする必要があります。

## <a name="span-idwddm_13_present_ddispanspan-idwddm_13_present_ddispanwddm-13-present-ddi"></a><span id="wddm_1.3_present_ddi"></span><span id="WDDM_1.3_PRESENT_DDI"></span>WDDM 1.3 present (DDI)


以下の参照トピックでは、ディスプレイミニポートドライバーとユーザーモードの表示ドライバーにこの機能を実装する方法について説明します。

-   [*pfnPresent1 (D3D)* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_present1)
-   [*pfnPresent1 (DXGI)* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/dxgiddi/ns-dxgiddi-dxgi1_3_ddi_base_functions)
-   [**D3DDDIARG\_PRESENT1**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/ns-d3dumddi-_d3dddiarg_present1)
-   [**D3DDDIARG\_の表面**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/ns-d3dumddi-d3dddiarg_presentsurface)
-   [**D3DKMT\_コンポジション\_PRESENTHISTORYTOKEN**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmthk/ns-d3dkmthk-_d3dkmt_composition_presenthistorytoken)
-   [**DXGI\_DDI\_ARG\_PRESENT1**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dxgiddi/ns-dxgiddi-dxgi_ddi_arg_present1)
-   [**DXGI\_DDI\_ARG\_の表面**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dxgiddi/ns-dxgiddi-dxgi_ddi_arg_presentsurface)
-   [**D3DDDI\_devicefuncs**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/ns-d3dumddi-_d3dddi_devicefuncs) (new **pfnPresent1**関数ポインター)
-   [**D3DDDIFORMAT**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dukmdt/ne-d3dukmdt-_d3dddiformat) (new **D3DDDIFMT\_G8R8** and **D3DDDIFMT\_R8**定数値)
-   [**D3DKMT\_存在\_モデル**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmthk/ne-d3dkmthk-_d3dkmt_present_model)(新しい**D3DKMT\_PM\_リダイレクト**された\_コンポジション定数値)
-   [**D3DKMT\_PRESENTHISTORYTOKEN**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmthk/ns-d3dkmthk-_d3dkmt_presenthistorytoken) (新しい**コンポジション**メンバー)
-   [**DXGI\_DDI\_BASE\_ARGS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dxgiddi/ns-dxgiddi-dxgi_ddi_base_args) (new **pDXGIDDIBaseFunctions4** member)
-   [**DXGI1\_3\_DDI\_BASE\_FUNCTIONS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dxgiddi/ns-dxgiddi-dxgi1_3_ddi_base_functions) (new **pfnPresent1**関数ポインター)

## <a name="span-idtexture_format_support_for_shared_surfacesspanspan-idtexture_format_support_for_shared_surfacesspanspan-idtexture_format_support_for_shared_surfacesspantexture-format-support-for-shared-surfaces"></a><span id="Texture_format_support_for_shared_surfaces"></span><span id="texture_format_support_for_shared_surfaces"></span><span id="TEXTURE_FORMAT_SUPPORT_FOR_SHARED_SURFACES"></span>共有サーフェスのテクスチャ形式のサポート


ドライバーは、 [**DXGI\_形式**](https://docs.microsoft.com/windows/desktop/api/dxgiformat/ne-dxgiformat-dxgi_format)の列挙から、これらの追加のテクスチャ形式のリソース共有と共有可能なバックバッファーの両方をサポートする必要があります。

- **DXGI\_形式\_A8\_UNORM**
- **DXGI\_形式\_R8\_UNORM**
- **DXGI\_形式\_R8G8\_UNORM**
- **DXGI\_形式\_BC1\_タイプレス\\** *
- **DXGI\_形式\_BC1\_UNORM**
- **DXGI\_形式\_BC1\_UNORM\_SRGB**
- **DXGI\_形式\_BC2\_タイプレス\\** *
- **DXGI\_形式\_BC2\_UNORM**
- **DXGI\_形式\_BC2\_UNORM\_SRGB**
- **DXGI\_形式\_BC3\_タイプレス\\** *
- **DXGI\_形式\_BC3\_UNORM**
- **DXGI\_形式\_BC3\_UNORM\_SRGB**

さらに、Microsoft Direct3D 11 以降がサポートされている場合は、ドライバーが**DXGI の\_形式\_L8\_UNORM**のプレースホルダー形式をサポートする必要があります。 **DXGI\_形式\_L8\_UNORM**は、機能的には**D3DDDIFMT\_L8**形式と同等です。

ドライバーは、 [**D3DDDIFORMAT**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dukmdt/ne-d3dukmdt-_d3dddiformat)列挙からの追加のテクスチャ形式もサポートする必要があります。

-   **D3DDDIFMT\_G8R8**
-   **D3DDDIFMT\_R8**

 

 






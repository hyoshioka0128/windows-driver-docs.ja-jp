---
title: マルチプレーン オーバーレイ リソースの作成
description: Multiplane オーバーレイを使用している場合は、Microsoft DirectX アプリ内に作成される割り当てにこれらの要件が適用されます。
ms.assetid: B3E9BEF8-5CB8-45A3-9491-19AB1EA3D74F
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0d43313e095836a28dd1a2b36976105ef341e74b
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67372846"
---
# <a name="multiplane-overlay-resource-creation"></a>マルチプレーン オーバーレイ リソースの作成


Multiplane オーバーレイを使用している場合は、Microsoft DirectX アプリ内に作成される割り当てにこれらの要件が適用されます。

## <a name="span-iddirectx11resourcecreationspanspan-iddirectx11resourcecreationspanspan-iddirectx11resourcecreationspandirectx-11-resource-creation"></a><span id="DirectX_11_resource_creation"></span><span id="directx_11_resource_creation"></span><span id="DIRECTX_11_RESOURCE_CREATION"></span>DirectX 11 のリソースの作成


ときに、 [ *CreateResource(D3D11)* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3d10umddi/nc-d3d10umddi-pfnd3d11ddi_createresource)関数が呼び出されます。

-   **D3D10\_DDI\_バインド\_存在**と**D3D10\_DDI\_リソース\_MISC\_SHARED**定数値設定は、 **BindFlags**のメンバー、 [ **D3D11DDIARG\_CREATERESOURCE** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3d10umddi/ns-d3d10umddi-d3d11ddiarg_createresource)構造体であることを示す、割り当てをスキャンできます。
-   可能性のフラグでの他のビット フィールドが**フラグ**は設定することなど。
    -   **D3D10\_DDI\_バインド\_シェーダー\_リソース**
    -   **D3D10\_DDI\_バインド\_レンダリング\_ターゲット**
    -   **D3D11\_DDI\_バインド\_順序なし\_アクセス**
    -   **D3D11\_DDI\_バインド\_デコーダー**
    -   **D3D11\_1DDI\_RESOURCE\_MISC\_RESTRICTED\_CONTENT**
    -   **D3D11\_1DDI\_RESOURCE\_MISC\_RESTRICT\_SHARED\_RESOURCE\_DRIVER**
-   ときに、 [ **DXGI\_DDI\_プライマリ\_DESC** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dxgiddi/ns-dxgiddi-dxgi_ddi_primary_desc)構造体が渡された、 [ *CreateResource(D3D11)* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3d10umddi/nc-d3d10umddi-pfnd3d11ddi_createresource)呼び出し。
    -   [**DXGI\_DDI\_プライマリ\_DESC** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dxgiddi/ns-dxgiddi-dxgi_ddi_primary_desc)の適切な値を持つ、 **VidPnSourceId**メンバー。
    -   [**DXGI\_DDI\_プライマリ\_DESC**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dxgiddi/ns-dxgiddi-dxgi_ddi_primary_desc).**ModeDesc**現在モードと一致します。
    -   Multiplane オーバーレイ リソースでは、ドライバーを設定する必要がありますいない、 **DXGI\_DDI\_プライマリ\_ドライバー\_フラグ\_いいえ\_SCANOUT** 内の値にフラグを設定**DriverFlags**のメンバー [ **DXGI\_DDI\_プライマリ\_DESC**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dxgiddi/ns-dxgiddi-dxgi_ddi_primary_desc)します。

## <a name="span-iddirectx9resourcecreationspanspan-iddirectx9resourcecreationspanspan-iddirectx9resourcecreationspandirectx-9-resource-creation"></a><span id="DirectX_9_resource_creation"></span><span id="directx_9_resource_creation"></span><span id="DIRECTX_9_RESOURCE_CREATION"></span>DirectX 9 リソースの作成


ときに、 [ *CreateResource2* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/nc-d3dumddi-pfnd3dddi_createresource2)関数が呼び出されます。

-   **プライマリ**と**SharedResource**でフラグのビット フィールド、**フラグ**のメンバー、 [ **D3DDDIARG\_CREATERESOURCE2** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dukmdt/ns-d3dukmdt-_d3dddiarg_createresource2)構造体を設定します。
-   可能性のフラグでの他のビット フィールドが**フラグ**は設定することなど。
    -   **レンダリング ターゲット**
    -   **テクスチャ**
    -   **DecodeRenderTarget**
    -   **RestrictedContent**
    -   **RestrictSharedAccess**
-   **VidPnSourceId**のメンバー、 [ **D3DDDIARG\_CREATERESOURCE2** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dukmdt/ns-d3dukmdt-_d3dddiarg_createresource2)構造体を適切に初期化します。
-   **RefreshRate**のメンバー、 [ **D3DDDIARG\_CREATERESOURCE2** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dukmdt/ns-d3dukmdt-_d3dddiarg_createresource2)構造体にゼロが含まれています。

 

 






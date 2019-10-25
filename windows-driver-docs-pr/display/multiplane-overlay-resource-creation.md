---
title: マルチプレーン オーバーレイ リソースの作成
description: Multiplane のオーバーレイを使用する場合、これらの要件は、Microsoft DirectX アプリ内で作成される割り当てに適用されます。
ms.assetid: B3E9BEF8-5CB8-45A3-9491-19AB1EA3D74F
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f16e432683a88e865404aad3e61371a994e71150
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72840543"
---
# <a name="multiplane-overlay-resource-creation"></a>マルチプレーン オーバーレイ リソースの作成


Multiplane のオーバーレイを使用する場合、これらの要件は、Microsoft DirectX アプリ内で作成される割り当てに適用されます。

## <a name="span-iddirectx_11_resource_creationspanspan-iddirectx_11_resource_creationspanspan-iddirectx_11_resource_creationspandirectx-11-resource-creation"></a><span id="DirectX_11_resource_creation"></span><span id="directx_11_resource_creation"></span><span id="DIRECTX_11_RESOURCE_CREATION"></span>DirectX 11 リソースの作成


[*Createresource (D3D11)* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d11ddi_createresource)関数が呼び出されると、次のようになります。

-   **D3D10\_ddi\_バインド\_PRESENT**および**D3D10\_DDI\_リソース\_その他の\_共有**定数値は、D3D11DDIARG の**bindflags**メンバーで設定され[ **\_CREATERESOURCE**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/ns-d3d10umddi-d3d11ddiarg_createresource)構造体。割り当てをスキャンできることを示します。
-   **フラグ**内の他のビットフィールドフラグも設定される可能性があります。次に例を示します。
    -   **D3D10\_DDI\_\_シェーダー\_リソースのバインド**
    -   **D3D10\_DDI\_バインド\_レンダー\_ターゲット**
    -   **D3D11\_DDI\_バインド\_順序付けられていない\_アクセス**
    -   **D3D11\_DDI\_\_デコーダーのバインド**
    -   **D3D11\_1DDI\_リソース\_その他\_制限された\_コンテンツ**
    -   **D3D11\_1DDI\_リソース\_その他の\_\_共有\_リソース\_ドライバを制限する**
-   [**DXGI\_DDI\_プライマリ\_DESC**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dxgiddi/ns-dxgiddi-dxgi_ddi_primary_desc)構造体が[*CREATERESOURCE (D3D11)* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d11ddi_createresource)の呼び出しで渡されると、次のようになります。
    -   [**DXGI\_DDI\_プライマリ\_DESC**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dxgiddi/ns-dxgiddi-dxgi_ddi_primary_desc)には、 **VidPnSourceId**メンバーの適切な値が含まれています。
    -   [**DXGI\_DDI\_プライマリ\_DESC**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dxgiddi/ns-dxgiddi-dxgi_ddi_primary_desc)です。**Modedesc**は現在のモードと一致します。
    -   Multiplane オーバーレイリソースの場合、ドライバーは dxgi **\_ddi\_プライマリ\_ドライバー\_フラグ**を設定しないでください。このフラグは、DXGI\_Ddi の**driverflags**メンバーに\_\_scanout フラグ値を設定しません\_[**プライマリ\_DESC**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dxgiddi/ns-dxgiddi-dxgi_ddi_primary_desc)。

## <a name="span-iddirectx_9_resource_creationspanspan-iddirectx_9_resource_creationspanspan-iddirectx_9_resource_creationspandirectx-9-resource-creation"></a><span id="DirectX_9_resource_creation"></span><span id="directx_9_resource_creation"></span><span id="DIRECTX_9_RESOURCE_CREATION"></span>DirectX 9 リソースの作成


[*CreateResource2*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_createresource2)関数が呼び出されると、次のようになります。

-   [**D3DDDIARG\_CREATERESOURCE2**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dukmdt/ns-d3dukmdt-_d3dddiarg_createresource2)構造体の**Flags**メンバーの**Primary**および**sharedresource**ビットフィールドフラグが設定されます。
-   **フラグ**内の他のビットフィールドフラグも設定される可能性があります。次に例を示します。
    -   **作り**
    -   **テクスチャ**
    -   **DecodeRenderTarget**
    -   **RestrictedContent**
    -   **RestrictSharedAccess**
-   [**D3DDDIARG\_CREATERESOURCE2**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dukmdt/ns-d3dukmdt-_d3dddiarg_createresource2)構造体の**VidPnSourceId**メンバーが適切に初期化されています。
-   [**D3DDDIARG\_CREATERESOURCE2**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dukmdt/ns-d3dukmdt-_d3dddiarg_createresource2)構造体の**RefreshRate**メンバーに0が含まれています。

 

 






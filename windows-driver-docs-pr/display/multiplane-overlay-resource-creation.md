---
title: Multiplane オーバーレイ リソースの作成
description: Multiplane オーバーレイを使用している場合は、Microsoft DirectX アプリ内に作成される割り当てにこれらの要件が適用されます。
ms.assetid: B3E9BEF8-5CB8-45A3-9491-19AB1EA3D74F
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5ac2cf5a648d676dc1580ad18ef2e77bfe6926c3
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56552126"
---
# <a name="multiplane-overlay-resource-creation"></a>Multiplane オーバーレイ リソースの作成


Multiplane オーバーレイを使用している場合は、Microsoft DirectX アプリ内に作成される割り当てにこれらの要件が適用されます。

## <a name="span-iddirectx11resourcecreationspanspan-iddirectx11resourcecreationspanspan-iddirectx11resourcecreationspandirectx-11-resource-creation"></a><span id="DirectX_11_resource_creation"></span><span id="directx_11_resource_creation"></span><span id="DIRECTX_11_RESOURCE_CREATION"></span>DirectX 11 のリソースの作成


ときに、 [ *CreateResource(D3D11)* ](https://msdn.microsoft.com/library/windows/hardware/ff540694)関数が呼び出されます。

-   **D3D10\_DDI\_バインド\_存在**と**D3D10\_DDI\_リソース\_MISC\_SHARED**定数値設定は、 **BindFlags**のメンバー、 [ **D3D11DDIARG\_CREATERESOURCE** ](https://msdn.microsoft.com/library/windows/hardware/ff542062)構造体であることを示す、割り当てをスキャンできます。
-   可能性のフラグでの他のビット フィールドが**フラグ**は設定することなど。
    -   **D3D10\_DDI\_バインド\_シェーダー\_リソース**
    -   **D3D10\_DDI\_バインド\_レンダリング\_ターゲット**
    -   **D3D11\_DDI\_バインド\_順序なし\_アクセス**
    -   **D3D11\_DDI\_バインド\_デコーダー**
    -   **D3D11\_1DDI\_RESOURCE\_MISC\_RESTRICTED\_CONTENT**
    -   **D3D11\_1DDI\_RESOURCE\_MISC\_RESTRICT\_SHARED\_RESOURCE\_DRIVER**
-   ときに、 [ **DXGI\_DDI\_プライマリ\_DESC** ](https://msdn.microsoft.com/library/windows/hardware/ff557511)構造体が渡された、 [ *CreateResource(D3D11)*](https://msdn.microsoft.com/library/windows/hardware/ff540694)呼び出し。
    -   [**DXGI\_DDI\_プライマリ\_DESC** ](https://msdn.microsoft.com/library/windows/hardware/ff557511)の適切な値を持つ、 **VidPnSourceId**メンバー。
    -   [**DXGI\_DDI\_プライマリ\_DESC**](https://msdn.microsoft.com/library/windows/hardware/ff557511).**ModeDesc**現在モードと一致します。
    -   Multiplane オーバーレイ リソースでは、ドライバーを設定する必要がありますいない、 **DXGI\_DDI\_プライマリ\_ドライバー\_フラグ\_いいえ\_SCANOUT** 内の値にフラグを設定**DriverFlags**のメンバー [ **DXGI\_DDI\_プライマリ\_DESC**](https://msdn.microsoft.com/library/windows/hardware/ff557511)します。

## <a name="span-iddirectx9resourcecreationspanspan-iddirectx9resourcecreationspanspan-iddirectx9resourcecreationspandirectx-9-resource-creation"></a><span id="DirectX_9_resource_creation"></span><span id="directx_9_resource_creation"></span><span id="DIRECTX_9_RESOURCE_CREATION"></span>DirectX 9 リソースの作成


ときに、 [ *CreateResource2* ](https://msdn.microsoft.com/library/windows/hardware/hh406287)関数が呼び出されます。

-   **プライマリ**と**SharedResource**でフラグのビット フィールド、**フラグ**のメンバー、 [ **D3DDDIARG\_CREATERESOURCE2** ](https://msdn.microsoft.com/library/windows/hardware/hh451074)構造体を設定します。
-   可能性のフラグでの他のビット フィールドが**フラグ**は設定することなど。
    -   **レンダリング ターゲット**
    -   **テクスチャ**
    -   **DecodeRenderTarget**
    -   **RestrictedContent**
    -   **RestrictSharedAccess**
-   **VidPnSourceId**のメンバー、 [ **D3DDDIARG\_CREATERESOURCE2** ](https://msdn.microsoft.com/library/windows/hardware/hh451074)構造体を適切に初期化します。
-   **RefreshRate**のメンバー、 [ **D3DDDIARG\_CREATERESOURCE2** ](https://msdn.microsoft.com/library/windows/hardware/hh451074)構造体にゼロが含まれています。

 

 






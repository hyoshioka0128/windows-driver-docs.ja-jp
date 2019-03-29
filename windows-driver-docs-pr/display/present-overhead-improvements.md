---
title: 存在するオーバーヘッドの機能強化
ms.assetid: 92B282D6-0D04-4352-AE03-E0A7A43711E7
description: GPU の処理の負荷を削減するバッファーを内部のスワップの機能強化
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 64bff6e8c3e9b7187e3ebf9daa0fe395b855533c
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56570406"
---
# <a name="present-overhead-improvements"></a>存在するオーバーヘッドの機能強化


Windows 8.1 以降、マイクロソフトの Direct3D ランタイム ハンドル スワップの内部バッファー詳細については、効率的に、GPU の処理負荷を削減します。 このパフォーマンスの向上をサポートするには、Windows Display Driver Model (WDDM) 1.3 およびそれ以降のドライバーする必要があります新しいの存在するデバイス ドライバー インターフェイス (DDI) 新しいテクスチャ形式としてサポート共有サーフェス。

## <a name="span-idwddm13presentddispanspan-idwddm13presentddispanwddm-13-present-ddi"></a><span id="wddm_1.3_present_ddi"></span><span id="WDDM_1.3_PRESENT_DDI"></span>WDDM 1.3 存在 DDI


これらの参照トピックでは、ディスプレイのミニポート ドライバーとユーザー モードのディスプレイ ドライバーでこの機能を実装する方法について説明します。

-   [*pfnPresent1(D3D)*](https://msdn.microsoft.com/library/windows/hardware/dn458010)
-   [*pfnPresent1(DXGI)*](https://msdn.microsoft.com/library/windows/hardware/dn469267)
-   [**D3DDDIARG\_PRESENT1**](https://msdn.microsoft.com/library/windows/hardware/dn457997)
-   [**D3DDDIARG\_PRESENTSURFACE**](https://msdn.microsoft.com/library/windows/hardware/dn457998)
-   [**D3DKMT\_コンポジション\_PRESENTHISTORYTOKEN**](https://msdn.microsoft.com/library/windows/hardware/dn458001)
-   [**DXGI\_DDI\_ARG\_PRESENT1**](https://msdn.microsoft.com/library/windows/hardware/dn457714)
-   [**DXGI\_DDI\_ARG\_PRESENTSURFACE**](https://msdn.microsoft.com/library/windows/hardware/dn457715)
-   [**D3DDDI\_DEVICEFUNCS** ](https://msdn.microsoft.com/library/windows/hardware/ff544519) (新しい**pfnPresent1**関数ポインター)
-   [**D3DDDIFORMAT** ](https://msdn.microsoft.com/library/windows/hardware/ff544312) (新しい**D3DDDIFMT\_G8R8**と**D3DDDIFMT\_R8**定数値)
-   [**D3DKMT\_存在\_モデル**](https://msdn.microsoft.com/library/windows/hardware/ff548197) (新しい**D3DKMT\_PM\_REDIRECTED\_コンポジション**定数値)
-   [**D3DKMT\_PRESENTHISTORYTOKEN** ](https://msdn.microsoft.com/library/windows/hardware/ff548188) (新しい**コンポジション**メンバー)
-   [**DXGI\_DDI\_ベース\_ARGS** ](https://msdn.microsoft.com/library/windows/hardware/ff557485) (新しい**pDXGIDDIBaseFunctions4**メンバー)
-   [**DXGI1\_3\_DDI\_ベース\_関数**](https://msdn.microsoft.com/library/windows/hardware/dn465883) (新しい**pfnPresent1**関数ポインター)

## <a name="span-idtextureformatsupportforsharedsurfacesspanspan-idtextureformatsupportforsharedsurfacesspanspan-idtextureformatsupportforsharedsurfacesspantexture-format-support-for-shared-surfaces"></a><span id="Texture_format_support_for_shared_surfaces"></span><span id="texture_format_support_for_shared_surfaces"></span><span id="TEXTURE_FORMAT_SUPPORT_FOR_SHARED_SURFACES"></span>共有サーフェスのテクスチャ形式のサポート


ドライバーは、両方をサポートする必要があります共有リソースとこれらの追加のテクスチャ形式からの共有可能なバックバッファーに対して、 [ **DXGI\_形式**](https://msdn.microsoft.com/library/windows/desktop/bb173059)列挙体。

- **DXGI\_形式\_A8\_UNORM**
- **DXGI\_形式\_R8\_UNORM**
- **DXGI\_形式\_R8G8\_UNORM**
- **DXGI\_形式\_BC1\_TYPELESS\\***
- **DXGI\_FORMAT\_BC1\_UNORM**
- **DXGI\_FORMAT\_BC1\_UNORM\_SRGB**
- **DXGI\_形式\_BC2\_TYPELESS\\***
- **DXGI\_FORMAT\_BC2\_UNORM**
- **DXGI\_FORMAT\_BC2\_UNORM\_SRGB**
- **DXGI\_形式\_BC3\_TYPELESS\\***
- **DXGI\_形式\_BC3\_UNORM**
- **DXGI\_FORMAT\_BC3\_UNORM\_SRGB**

さらに、ドライバーがサポートする必要があります、 **DXGI\_形式\_L8\_UNORM** Microsoft direct3d11 と Direct3D 機能レベル 9 のハードウェアの後でサポートされている場合のプレース ホルダーの書式設定します。 **DXGI\_形式\_L8\_UNORM**は機能的に等価、 **D3DDDIFMT\_L8**形式。

ドライバーから追加のテクスチャ形式もサポートする必要があります、 [ **D3DDDIFORMAT** ](https://msdn.microsoft.com/library/windows/hardware/ff544312)列挙体。

-   **D3DDDIFMT\_G8R8**
-   **D3DDDIFMT\_R8**

 

 






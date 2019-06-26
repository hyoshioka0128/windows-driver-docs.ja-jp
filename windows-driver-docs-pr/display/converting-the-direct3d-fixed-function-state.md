---
title: Direct3D の固定機能状態の変換
description: Direct3D の固定機能状態の変換
ms.assetid: bc93d65e-ac16-470d-8c52-db8b1cc74456
keywords:
- ユーザー モード ドライバー WDK Windows Vista の表示、Direct3D 固定機能の状態の変換
- 状態の固定関数変換 WDK を表示します。
- Direct3D の固定機能の状態に変換します。
- Windows Vista Direct3D の WDK のコンバーター
- ピクセル シェーダー コンバーター WDK を表示します。
- 頂点シェーダー コンバーター WDK を表示します。
- シェーダー コンバーター WDK を表示します。
- ステージの状態のテクスチャの WDK 表示
- WDK の表示状態を表示します。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e81ee6c1e2015712bd0eec43d254db60d7373f0b
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67370296"
---
# <a name="converting-the-direct3d-fixed-function-state"></a>Direct3D の固定機能状態の変換


マイクロソフトの Direct3D ランタイムでは、ユーザー モードのディスプレイ ドライバーは、各シェーダーの種類のバージョン 2.0 以降をサポートしている場合に、頂点またはピクセル シェーダーのバージョン 2.0 に Direct3D 固定機能の状態を変換します。 ただし、ランタイムでは、シェーダーのバージョンは変換されません。 たとえば、アプリケーションでは、頂点またはピクセル シェーダーのバージョン 1.1 を使用する場合、バージョン 1.1 に渡されます未変換ドライバーがシェーダーのバージョン 2.0 以降をサポートするかどうかに関係なく、ユーザー モードのディスプレイ ドライバー。 柔軟な頂点の形式 (FVF) コードは、固定機能の処理に使用されます。

### <a name="span-idconverterfeaturesfordirectxversionsspanspan-idconverterfeaturesfordirectxversionsspanconverter-features-for-directx-versions"></a><span id="converter_features_for_directx_versions"></span><span id="CONVERTER_FEATURES_FOR_DIRECTX_VERSIONS"></span>DirectX のバージョンのコンバーター機能

固定関数頂点とピクセル シェーダーのコンバーターのしくみは、使用する Microsoft DirectX のバージョンによって異なります。

-   DirectX 9.0

    固定機能の頂点とピクセル シェーダーのコンバーターは、Windows Vista のディスプレイ ドライバー モデルを操作できます。

    コンバーターは既定で有効にします。

    固定機能の頂点またはピクセル シェーダーのコンバーターを使用すると、純粋なデバイスは無効になります。 アプリケーションが、純粋なデバイスを要求すると、Direct3D ランタイムは、HAL のデバイスを作成します。

    ランタイムは、混合頂点処理をサポートします。

    ソフトウェアの頂点処理常に固定関数頂点シェーダーのコンバーターを使用します。

    ハードウェアの頂点の処理は、ドライバーには、頂点シェーダーのバージョン 2.0 以降がサポートされている場合、固定関数頂点シェーダーのコンバーターを使用します。

    ハードウェアの頂点の処理は、ドライバーには、ピクセル シェーダーのバージョン 2.0 以降がサポートされている場合、固定関数ピクセル シェーダーのコンバーターを使用します。

    混合の頂点の処理モードでハードウェアには、固定関数頂点シェーダーのコンバーターが有効になっているときに浮動小数点定数の数が、ハードウェアでサポートできるに設定されます。

-   DirectX 8.0 以降

    固定機能の頂点とピクセル シェーダーのコンバーターは、Windows Vista display driver モデルのみを操作できます。

    コンバーターは既定で有効にします。

    ソフトウェアの頂点の処理では、固定関数頂点シェーダーのコンバーターがサポートされていません。

    ハードウェアの頂点の処理は、ドライバーには、頂点シェーダーのバージョン 2.0 以降がサポートされている場合、固定関数頂点シェーダーのコンバーターを使用します。

    ハードウェアの頂点の処理は、ドライバーには、ピクセル シェーダーのバージョン 2.0 以降がサポートされている場合、固定関数ピクセル シェーダーのコンバーターを使用します。

    **注**  で DirectX 8.0 より前の DirectX のバージョンは、シェーダーのマッピング コードを fixed 関数が実装されている*Ddraw.dll*します。

     

### <a name="span-idunusedusermodedisplaydriverfunctionsspanspan-idunusedusermodedisplaydriverfunctionsspanunused-user-mode-display-driver-functions"></a><span id="unused_user_mode_display_driver_functions"></span><span id="UNUSED_USER_MODE_DISPLAY_DRIVER_FUNCTIONS"></span>未使用のユーザー モードのディスプレイ ドライバー関数

次[ユーザー モードのディスプレイ ドライバー関数](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/index)固定関数頂点シェーダーのコンバーターが有効にすると、Direct3D ランタイムでは呼び出されません。

-   [**MultiplyTransform**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/nc-d3dumddi-pfnd3dddi_multiplytransform)

-   [**SetTransform**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/nc-d3dumddi-pfnd3dddi_settransform)

-   [**SetMaterial**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/nc-d3dumddi-pfnd3dddi_setmaterial)

-   [**SetLight**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/nc-d3dumddi-pfnd3dddi_setlight)

-   [**CreateLight**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/nc-d3dumddi-pfnd3dddi_createlight)

-   [**DestroyLight**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/nc-d3dumddi-pfnd3dddi_destroylight)

### <a name="span-idunusedrenderstatesspanspan-idunusedrenderstatesspanunused-render-states"></a><span id="unused_render_states"></span><span id="UNUSED_RENDER_STATES"></span>未使用の描画状態

次の描画状態が Direct3D ランタイムによって渡されないと (または、ドライバーによって、誤って渡される場合は無視できます)、固定関数頂点シェーダーのコンバーターが有効な場合。

-   D3DRS\_VERTEXBLEND

-   D3DRS\_INDEXEDVERTEXBLENDENABLE

-   D3DRS\_TWEENFACTOR

-   D3DRS\_FOGVERTEXMODE

-   D3DRS\_照明

-   D3DRS\_アンビエント

-   D3DRS\_カラー頂点

-   D3DRS\_LOCALVIEWER

-   D3DRS\_DIFFUSEMATERIALSOURCE

-   D3DRS\_SPECULARMATERIALSOURCE

-   D3DRS\_AMBIENTMATERIALSOURCE

-   D3DRS\_EMISSIVEMATERIALSOURCE

-   D3DRS\_POINTSCALEENABLE

-   D3DRS\_POINTSCALE\_A

-   D3DRS\_POINTSCALE\_B

-   D3DRS\_POINTSCALE\_C

-   D3DRS\_NORMALIZENORMALS

### <a name="span-idignoredtexturestagestatesspanspan-idignoredtexturestagestatesspanignored-texture-stage-states"></a><span id="ignored_texture_stage_states"></span><span id="IGNORED_TEXTURE_STAGE_STATES"></span>無視されたテクスチャ ステージの状態

Direct3D ランタイムは、ドライバーをステージ状態のすべてのテクスチャを渡します。 ドライバーでは、固定関数ピクセル シェーダーのコンバーターが有効にすると、次のテクスチャのステージの状態を無視します。

-   D3DTSS\_COLOROP

-   D3DTSS\_COLORARG1

-   D3DTSS\_COLORARG2

-   D3DTSS\_ALPHAOP

-   D3DTSS\_ALPHAARG1

-   D3DTSS\_ALPHAARG2

-   D3DTSS\_BUMPENVMAT00

-   D3DTSS\_BUMPENVMAT01

-   D3DTSS\_BUMPENVMAT10

-   D3DTSS\_BUMPENVMAT11

-   D3DTSS\_BUMPENVLSCALE

-   D3DTSS\_BUMPENVLOFFSET

-   D3DTSS\_COLORARG0

-   D3DTSS\_ALPHAARG0

-   D3DTSS\_RESULTARG

-   D3DTSS\_定数

 

 






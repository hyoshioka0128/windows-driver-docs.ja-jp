---
title: Direct3D の固定機能状態の変換
description: Direct3D の固定機能状態の変換
ms.assetid: bc93d65e-ac16-470d-8c52-db8b1cc74456
keywords:
- ユーザーモードディスプレイドライバー WDK Windows Vista、Direct3D 固定関数の状態の変換
- 固定機能の状態変換 WDK の表示
- 変換 (Direct3D の固定関数の状態を)
- コンバーター WDK Windows Vista Direct3D
- ピクセルシェーダーコンバーターの WDK ディスプレイ
- 頂点シェーダーコンバーターの WDK ディスプレイ
- シェーダーコンバーター WDK ディスプレイ
- テクスチャステージの状態 WDK ディスプレイ
- 表示状態 WDK 表示
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7378da680c6ec175886db74c2833668b3adb17f2
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72839789"
---
# <a name="converting-the-direct3d-fixed-function-state"></a>Direct3D の固定機能状態の変換


ユーザーモードの表示ドライバーがシェーダーの種類ごとにバージョン2.0 以降をサポートしている場合、Microsoft Direct3D ランタイムは、Direct3D の固定関数の状態を頂点またはピクセルシェーダーバージョン2.0 に変換します。 ただし、ランタイムではシェーダーのバージョンが変換されません。 たとえば、アプリケーションで頂点シェーダーバージョン1.1 を使用している場合、ドライバーでシェーダーバージョン2.0 以降がサポートされているかどうかに関係なく、バージョン1.1 は、ユーザーモードの表示ドライバーに変換されずに渡されます。 フレキシブル頂点フォーマット (FVF) コードは、固定関数処理で使用されます。

### <a name="span-idconverter_features_for_directx_versionsspanspan-idconverter_features_for_directx_versionsspanconverter-features-for-directx-versions"></a><span id="converter_features_for_directx_versions"></span><span id="CONVERTER_FEATURES_FOR_DIRECTX_VERSIONS"></span>DirectX バージョンのコンバーター機能

固定関数の頂点とピクセルシェーダーのコンバーターの動作は、使用されている Microsoft DirectX のバージョンによって異なります。

-   DirectX 9.0

    固定関数の頂点とピクセルシェーダーのコンバーターは、Windows Vista display driver モデルで動作します。

    コンバーターは既定で有効になっています。

    固定関数の頂点またはピクセルシェーダーコンバーターが使用されている場合、純粋なデバイスは無効になります。 アプリケーションが純粋なデバイスを要求すると、Direct3D ランタイムによって HAL デバイスが作成されます。

    ランタイムは、混合頂点処理をサポートしています。

    ソフトウェアの頂点処理では、常に固定関数の頂点シェーダーコンバーターが使用されます。

    ハードウェアの頂点処理では、ドライバーが頂点シェーダーバージョン2.0 以降をサポートする場合に、固定関数の頂点シェーダーコンバーターを使用します。

    ハードウェアの頂点処理では、ドライバーでピクセルシェーダーバージョン2.0 以降がサポートされている場合に、固定関数ピクセルシェーダーコンバーターが使用されます。

    混合頂点処理モードでは、固定関数の頂点シェーダーコンバーターがハードウェアに対して有効になっている場合、float 定数の数はハードウェアがサポートできるものに設定されます。

-   DirectX 8.0 以前

    固定関数の頂点とピクセルシェーダーのコンバーターは、Windows Vista display driver model でのみ動作します。

    コンバーターは既定で有効になっています。

    固定関数の頂点シェーダーコンバーターは、ソフトウェアの頂点処理ではサポートされていません。

    ハードウェアの頂点処理では、ドライバーが頂点シェーダーバージョン2.0 以降をサポートする場合に、固定関数の頂点シェーダーコンバーターを使用します。

    ハードウェアの頂点処理では、ドライバーでピクセルシェーダーバージョン2.0 以降がサポートされている場合に、固定関数ピクセルシェーダーコンバーターが使用されます。

    **注**   directx 8.0 より前のバージョンの directx では、シェーダーマッピングコードに対する固定関数が*Ddraw*に実装されています。

     

### <a name="span-idunused_user_mode_display_driver_functionsspanspan-idunused_user_mode_display_driver_functionsspanunused-user-mode-display-driver-functions"></a><span id="unused_user_mode_display_driver_functions"></span><span id="UNUSED_USER_MODE_DISPLAY_DRIVER_FUNCTIONS"></span>未使用のユーザーモード表示ドライバー関数

次の[ユーザーモード表示ドライバー関数](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)は、固定関数の頂点シェーダーコンバーターが有効になっている場合、Direct3D ランタイムによって呼び出されません。

-   [**乗数 Ytransform**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_multiplytransform)

-   [**SetTransform**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_settransform)

-   [**SetMaterial**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_setmaterial)

-   [**SetLight**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_setlight)

-   [**CreateLight**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_createlight)

-   [**DestroyLight**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_destroylight)

### <a name="span-idunused_render_statesspanspan-idunused_render_statesspanunused-render-states"></a><span id="unused_render_states"></span><span id="UNUSED_RENDER_STATES"></span>未使用のレンダリング状態

次のレンダリング状態は、固定関数の頂点シェーダーコンバーターが有効になっている場合、Direct3D ランタイムによって渡されません (または、間違って渡された場合、ドライバーによって無視される可能性があります)。

-   D3DRS\_VERTEXBLEND

-   D3DRS\_INDEXEDVERTEXBLENDENABLE

-   D3DRS\_TWEENFACTOR

-   D3DRS\_のモード

-   D3DRS\_照明

-   D3DRS\_アンビエント

-   D3DRS\_COLORVERTEX

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

### <a name="span-idignored_texture_stage_statesspanspan-idignored_texture_stage_statesspanignored-texture-stage-states"></a><span id="ignored_texture_stage_states"></span><span id="IGNORED_TEXTURE_STAGE_STATES"></span>無視されたテクスチャステージの状態

Direct3D ランタイムは、すべてのテクスチャステージの状態をドライバーに渡します。 固定機能ピクセルシェーダーコンバーターが有効になっている場合、ドライバーは次のテクスチャステージの状態を無視する必要があります。

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

 

 






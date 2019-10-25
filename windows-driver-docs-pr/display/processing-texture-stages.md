---
title: テクスチャ ステージの処理
description: テクスチャ ステージの処理
ms.assetid: e22f5e2f-f17c-4a84-941b-c38e14b28550
keywords:
- 複数のテクスチャ WDK Direct3D、テクスチャステージ
- テクスチャステージ WDK Direct3D
- D3DDP2OP_TEXTURESTAGESTATE
- D3DHAL_DP2TEXTURESTAGESTATE
- テクスチャ管理 WDK Direct3D、ステージ
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 03ff3d64f62f635257131e949c6e90de9006c175
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72826051"
---
# <a name="processing-texture-stages"></a>テクスチャ ステージの処理


## <span id="ddk_processing_texture_stages_gg"></span><span id="DDK_PROCESSING_TEXTURE_STAGES_GG"></span>


ドライバーは、コマンドストリームで後に続く D3DDP2OP\_TEXTURESTAGESTATE operation コードと[**D3DHAL\_DP2TEXTURESTAGESTATE**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dhal/ns-d3dhal-_d3dhal_dp2texturestagestate)構造体を使用して、テクスチャステージの状態への変更を処理します。 ドライバーが操作コードを処理する方法の詳細については、「[コマンドストリーム](command-stream.md)」を参照してください。

たとえば、操作コードが D3DDP2OP\_TEXTURESTAGESTATE で、 [**D3DHAL\_DP2COMMAND**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dhal/ns-d3dhal-_d3dhal_dp2command)構造体の**wstatecount**メンバーの値が7の場合、7 D3DHAL\_DP2TEXTURESTAGESTATE 構造体次の D3DHAL\_DP2COMMAND 命令に到達する前にフォローします。 各 D3DHAL\_DP2TEXTURESTAGESTATE 構造体には、テクスチャ描画パイプラインのどのステージにテクスチャ状態を変更する必要があるかを指定する**Dwstage**メンバーが含まれています。 同じ構造体の**Tsstate**メンバーは、設定する D3DTEXTURESTAGESTATETYPE 列挙型の状態を指定します。また、\_D3DHAL の DP2TEXTURESTAGESTATE 構造体の**dwValue**メンバーには、指定したの値が含まれます。状態を設定する必要があります。

このプロセスは、すべてのレンダリング状態、または他の種類の命令で同じです。 [**D3DHAL\_DP2COMMAND**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dhal/ns-d3dhal-_d3dhal_dp2command)構造体の**BCOMMAND**メンバーが D3DDP2OP\_renderstate の場合、従う構造は[**D3DHAL\_DP2RENDERSTATE**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dhal/ns-d3dhal-_d3dhal_dp2renderstate)構造体であり、その構造体の情報を使用してを設定します。それに応じたレンダリング状態。

個々のブール値のレンダリング状態を使用して座標を制御するのではなく、各レンダリング状態の値は、D3DWRAP\_で構成される一連のフラグ ( *d3dtypes*で定義されている)\_V フラグで構成されます。 この変更は、より高い次元のテクスチャとの互換性のために行われました。

複数のテクスチャの実装に関するその他の有用な情報については、DirectX SDK ドキュメントの「blend の式」、「テクスチャごとの状態のセマンティクス」、「カラー演算」、「アルファ演算」を参照してください。 DirectX 6.0 以降のバージョンで有効になっているテクスチャステージの状態の種類の詳細については、「D3DTEXTUREOP and D3DTEXTUREFILTERTYPE 列挙型」を参照してください。

**   DirectX** 9.0 以降のアプリケーションでは、D3DSAMPLERSTATETYPE 列挙体の値を使用して、サンプラーテクスチャ関連のレンダリング状態の特性を制御できます。 DirectX 8.0 以前では、これらのサンプラーの状態は D3DTEXTURESTAGESTATETYPE 列挙体に含まれていました。 ランタイムは、ユーザーモードサンプラーの状態 (D3DSAMP\_*Xxx*) をカーネルモードの D3DTSS\_*xxx*値にマップして、ドライバーがユーザーモードのサンプラー状態を処理する必要がないようにします。 D3DSAMPLERSTATETYPE の詳細については、最新の DirectX SDK のドキュメントを参照してください。

 

 

 






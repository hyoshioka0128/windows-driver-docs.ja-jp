---
title: テクスチャ ステージの処理
description: テクスチャ ステージの処理
ms.assetid: e22f5e2f-f17c-4a84-941b-c38e14b28550
keywords:
- 複数のテクスチャ WDK Direct3D テクスチャ ステージ
- WDK Direct3D のテクスチャ
- D3DDP2OP_TEXTURESTAGESTATE
- D3DHAL_DP2TEXTURESTAGESTATE
- テクスチャ管理 WDK Direct3D、ステージ
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c1b6309f904eaee91365970b993a67de5053c985
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67383908"
---
# <a name="processing-texture-stages"></a>テクスチャ ステージの処理


## <span id="ddk_processing_texture_stages_gg"></span><span id="DDK_PROCESSING_TEXTURE_STAGES_GG"></span>


ドライバーの使用、D3DDP2OP\_TEXTURESTAGESTATE 操作コードと[ **D3DHAL\_DP2TEXTURESTAGESTATE** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dhal/ns-d3dhal-_d3dhal_dp2texturestagestate)変更を処理するコマンド ストリーム内で次の構造テクスチャ ステージの状態にします。 ドライバー操作のコードを処理する方法については、次を参照してください。[コマンド Stream](command-stream.md)します。

たとえば、操作コードが D3DDP2OP が場合\_TEXTURESTAGESTATE の値、 **wStateCount**のメンバー、 [ **D3DHAL\_DP2COMMAND** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dhal/ns-d3dhal-_d3dhal_dp2command)構造体は、7、7 つ D3DHAL\_DP2TEXTURESTAGESTATE 構造が [次へ] D3DHAL 前に済まして\_DP2COMMAND 命令に到達します。 各 D3DHAL\_DP2TEXTURESTAGESTATE 構造に含まれる、 **dwStage**テクスチャのブレンド パイプラインのステージは、テクスチャ状態の変更する必要がありますを指定するメンバー。 **TSState**同じ構造体のメンバーを設定する D3DTEXTURESTAGESTATETYPE 列挙型の状態を指定して、 **dwValue** 、D3DHAL のメンバー\_DP2TEXTURESTAGESTATE構造体には、指定した状態を設定する必要があります、値が含まれています。

プロセスは、すべての描画状態、または他の種類の命令も同じです。 場合、 **bCommand**のメンバー、 [ **D3DHAL\_DP2COMMAND** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dhal/ns-d3dhal-_d3dhal_dp2command)構造体が D3DDP2OP\_RENDERSTATE、その構造に従うは、 [**D3DHAL\_DP2RENDERSTATE** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dhal/ns-d3dhal-_d3dhal_dp2renderstate)構造とその構造体の情報は、レンダリング状態を適宜設定に使用されます。

レンダリングの各状態値は、D3DWRAP と共に構成フラグのセットを座標を制御するブール値の個別の描画状態を使用してではなく\_して D3DWRAP\_V フラグ (で定義されている*d3dtypes.h*)。 高次元テクスチャの互換性のため、この変更が加えられました。

Blend 式、テクスチャごとの状態、色の操作、およびアルファの操作のセマンティクスをカバーするセクションで DirectX SDK ドキュメントでは、テクスチャの複数の実装に関連するその他の有用な情報を検出できます。 DirectX 6.0 と以降のバージョンを参照してください、D3DTEXTUREOP D3DTEXTUREFILTERTYPE 列挙型の有効なテクスチャ ステージ状態の種類の詳細についてはします。

**注**   DirectX 9.0 と以降のアプリケーションで値を使用 D3DSAMPLERSTATETYPE 列挙サンプラーのレンダリングのテクスチャに関連する状態の特性を制御します。 DirectX 8.0 以降では、これらのサンプラーの状態が D3DTEXTURESTAGESTATETYPE 列挙に含まれます。 ランタイムは、ユーザー モード サンプラーの状態をマップ (D3DSAMP\_*Xxx*) には、カーネル モード D3DTSS\_*Xxx*値ドライバーがユーザー モード サンプラーの状態を処理する必要はありません。 D3DSAMPLERSTATETYPE の詳細については、DirectX SDK の最新のドキュメントを参照してください。

 

 

 






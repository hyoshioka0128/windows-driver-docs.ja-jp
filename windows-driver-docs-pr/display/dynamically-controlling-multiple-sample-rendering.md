---
title: 複数サンプル レンダリングの動的制御
description: 複数サンプル レンダリングの動的制御
ms.assetid: cd0bea22-29e8-40f7-987b-5c36765e5677
keywords:
- 複数の標本レンダリング WDK DirectX 9.0、ダイナミック コントロール
- multisamples WDK DirectX 9.0、ダイナミック コントロールのレンダリング
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 913def1d2ce1981a8d695e7e9d508d199a9c83da
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67383103"
---
# <a name="dynamically-controlling-multiple-sample-rendering"></a>複数サンプル レンダリングの動的制御


## <span id="ddk_dynamically_controlling_multiple_sample_rendering_gg"></span><span id="DDK_DYNAMICALLY_CONTROLLING_MULTIPLE_SAMPLE_RENDERING_GG"></span>


DirectX 9.0 バージョンのドライバーでは、または有効にして、プリミティブのレンダリングの間でのマルチ サンプル表示を無効にするの機能をサポートできます。 ドライバーのデバイスは、この機能をサポートしています、ドライバー、D3DPRASTERCAPS を設定することを報告する\_マルチ サンプリング\_内のビットを切り替え機能、 **RasterCaps** D3DCAPS9 構造体のメンバー。 ドライバーへの応答で D3DCAPS9 構造体を返す、 **GetDriverInfo2** 」の説明に従って D3DCAPS8 構造体を返すにする方法と同様にクエリ[DirectX 8.0 スタイル Direct3D の機能を Reporting](reporting-directx-8-0-style-direct3d-capabilities.md)します。 このクエリのサポートについては、「[サポート GetDriverInfo2](supporting-getdriverinfo2.md)します。

切り替える複数サンプル レンダリング オンとオフを複数のシーンが開始および終了シーンの状態の間、ドライバーの受信、D3DDP2OP\_RENDERSTATE 操作のコードで、[コマンド ストリーム](command-stream.md)の[ **D3dDrawPrimitives2** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dhal/nc-d3dhal-lpd3dhal_drawprimitives2cb)関数。 ドライバーの処理、D3DRS\_MULTISAMPLEANTIALIAS から状態を表示する、 **RenderState**のメンバー、 [ **D3DHAL\_DP2RENDERSTATE** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dhal/ns-d3dhal-_d3dhal_dp2renderstate)このオペレーション コードに関連付けられている構造体。 ドライバーを決定するブール値から複数サンプル レンダリングを有効にするかどうか、 **dwState** D3DHAL のメンバー\_DP2RENDERSTATE します。 値**TRUE**を有効にすることを意味し、 **FALSE**を無効にすることを意味します。

場合、D3DPRASTERCAPS\_マルチ サンプリング\_切り替え機能のビットが設定されて、ドライバーは、D3DRS を受信できる\_MULTISAMPLEANTIALIAS D3DRENDERSTATE 間の状態を表示する\_SCENECAPTURE 指定状態を表示します。**TRUE**開始シーンについてと**FALSE**エンド シーンについて。

 

 






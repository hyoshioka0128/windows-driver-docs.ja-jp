---
title: 複数のサンプルレンダリングを動的に制御する
description: 複数のサンプルレンダリングを動的に制御する
ms.assetid: cd0bea22-29e8-40f7-987b-5c36765e5677
keywords:
- 複数サンプル表示 WDK DirectX 9.0、ダイナミックコントロール
- multisamples のレンダリング WDK DirectX 9.0、ダイナミックコントロール
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7513bd1e01dc6f5599a13319264550f65ca430d5
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72839709"
---
# <a name="dynamically-controlling-multiple-sample-rendering"></a>複数のサンプルレンダリングを動的に制御する


## <span id="ddk_dynamically_controlling_multiple_sample_rendering_gg"></span><span id="DDK_DYNAMICALLY_CONTROLLING_MULTIPLE_SAMPLE_RENDERING_GG"></span>


DirectX 9.0 バージョンドライバーでは、プリミティブのレンダリング間で複数のサンプルレンダリングをさらに有効または無効にする機能をサポートできます。 ドライバーのデバイスがこの機能をサポートしていることを報告するために、ドライバーは、D3DCAPS9 構造体の**RasterCaps**メンバーの D3DPRASTERCAPS\_マルチサンプリング\_トグル機能ビットを設定します。 このドライバーは、 **GetDriverInfo2**クエリに対する応答として、D3DCAPS9 構造体を返します。「 [DirectX 8.0 スタイルの Direct3D 機能の報告](reporting-directx-8-0-style-direct3d-capabilities.md)」で説明されているように、D3DCAPS8 構造体を返す方法と似ています。 このクエリのサポートについては、「 [GetDriverInfo2](supporting-getdriverinfo2.md)のサポート」を参照してください。

開始シーンと終了シーンの状態の間で複数のサンプルレンダリングをオンまたはオフに切り替えるには、ドライバーは[**D3dDrawPrimitives2**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dhal/nc-d3dhal-lpd3dhal_drawprimitives2cb)関数の[コマンドストリーム](command-stream.md)で D3DDP2OP\_renderstate 操作コードを受け取ります。 ドライバーは、この操作コードに関連付けられている[**D3DHAL\_DP2RENDERSTATE**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dhal/ns-d3dhal-_d3dhal_dp2renderstate)構造体の**renderstate**メンバーから D3DRS\_multisampleantialias エイリアシングレンダー状態を処理します。 ドライバーは、D3DHAL\_DP2RENDERSTATE の**Dwstate**メンバーのブール値から複数サンプルの表示を有効または無効にするかどうかを決定します。 値**TRUE**は、を有効にし、 **FALSE**を無効にすることを意味します。

D3DPRASTERCAPS\_マルチサンプリング\_トグル機能ビットが設定されている場合、ドライバーは、 **TRUE**を指定した D3DRENDERSTATE\_SCENECAPTURE render 状態間で、D3DRS\_MULTISAMPLEANTIALIAS エイリアシングレンダリング状態を受け取ることができます。開始-シーン情報。エンドシーン情報の場合は**FALSE** 。

 

 






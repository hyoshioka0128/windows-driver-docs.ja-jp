---
title: 単一ピクセル幅のアンチエイリアシング線のサポート
description: 単一ピクセル幅のアンチエイリアシング線のサポート
ms.assetid: f1e0df18-25d8-4ebd-b920-5cfbe5acf096
keywords:
- 1ピクセルワイド行 WDK DirectX 9.0
- エイリアス1ピクセル全体の行 WDK DirectX 9.0
- アンチエイリアシング1ピクセルワイド行 WDK DirectX 9.0
- ラインアンチエイリアシング WDK DirectX 9.0
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 11570ccc8f296be57ca8efe8575fef44f11329b5
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72825599"
---
# <a name="supporting-single-pixel-wide-antialiased-lines"></a>単一ピクセル幅のアンチエイリアシング線のサポート


## <span id="ddk_supporting_single_pixel_wide_antialiased_lines_gg"></span><span id="DDK_SUPPORTING_SINGLE_PIXEL_WIDE_ANTIALIASED_LINES_GG"></span>


DirectX 9.0 バージョンのドライバーでは、エイリアスまたはアンチエイリアシングの1ピクセル幅の線をサポートできます。 このドライバーは、D3DCAPS9 構造体の**LineCaps**メンバーで D3DLINECAPS\_アンチエイリアシング機能ビットを設定することによって、アンチエイリアシングのサポートを示します。 このドライバーは、 **GetDriverInfo2**クエリに対する応答として、D3DCAPS9 構造体を返します。「 [DirectX 8.0 スタイルの Direct3D 機能の報告](reporting-directx-8-0-style-direct3d-capabilities.md)」で説明されているように、D3DCAPS8 構造体を返す方法と似ています。 このクエリのサポートについては、「 [GetDriverInfo2](supporting-getdriverinfo2.md)のサポート」を参照してください。

行のアンチエイリアシングを有効にするために、ドライバーは[**D3dDrawPrimitives2**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dhal/nc-d3dhal-lpd3dhal_drawprimitives2cb)関数の[コマンドストリーム](command-stream.md)で D3DDP2OP\_renderstate 操作コードを受け取ります。 ドライバーは、この操作コードに関連付けられている[**D3DHAL\_DP2RENDERSTATE**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dhal/ns-d3dhal-_d3dhal_dp2renderstate)構造体の**renderstate**メンバーから、D3DRS\_アンチパターンの有効化のレンダリング状態を処理します。 ドライバーは、D3DHAL\_DP2RENDERSTATE の**Dwstate**メンバーのブール値に対して、行のアンチエイリアシングを有効または無効にするかどうかを決定します。 値**TRUE**は、を有効にし、 **FALSE**を無効にすることを意味します。 既定では、このレンダー状態の値は**FALSE**に設定されています。

D3DRS\_アンチパターン有効化のレンダリング状態は、ワイヤフレームモードで描画された三角形および線描画プリミティブ型に適用されます。

複数のサンプルのレンダーターゲットにレンダリングする場合、ドライバーは、行のアンチエイリアシングを有効にし、すべての行を別名で表示する要求を無視する必要があります。

 

 






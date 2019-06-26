---
title: 単一ピクセル幅のアンチエイリアシング線のサポート
description: 単一ピクセル幅のアンチエイリアシング線のサポート
ms.assetid: f1e0df18-25d8-4ebd-b920-5cfbe5acf096
keywords:
- ピクセル幅の単一行の WDK DirectX 9.0
- エイリアス シングル ピクセル幅行 WDK DirectX 9.0
- アンチエイリアシング単一のピクセル幅行 WDK DirectX 9.0
- 行のアンチエイリアシング WDK DirectX 9.0
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0519b825c24134f49a3f910cd9ac0a99bc987329
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67361238"
---
# <a name="supporting-single-pixel-wide-antialiased-lines"></a>単一ピクセル幅のアンチエイリアシング線のサポート


## <span id="ddk_supporting_single_pixel_wide_antialiased_lines_gg"></span><span id="DDK_SUPPORTING_SINGLE_PIXEL_WIDE_ANTIALIASED_LINES_GG"></span>


DirectX 9.0 バージョンのドライバーでは、別名またはアンチ エイリアスのいずれかであるピクセル幅の単一行をサポートできます。 ドライバーでは、アンチエイリアシングのサポートを示す、D3DLINECAPS を設定して\_アンチエイリアシング機能ビット、 **LineCaps** D3DCAPS9 構造体のメンバー。 ドライバーへの応答で D3DCAPS9 構造体を返す、 **GetDriverInfo2** 」の説明に従って D3DCAPS8 構造体を返すにする方法と同様にクエリ[DirectX 8.0 スタイル Direct3D の機能を Reporting](reporting-directx-8-0-style-direct3d-capabilities.md)します。 このクエリのサポートについては、「[サポート GetDriverInfo2](supporting-getdriverinfo2.md)します。

行のアンチエイリアシングを有効にする受信、D3DDP2OP\_RENDERSTATE 操作のコードで、[コマンド ストリーム](command-stream.md)の[ **D3dDrawPrimitives2** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dhal/nc-d3dhal-lpd3dhal_drawprimitives2cb)関数。 ドライバーの処理、D3DRS\_ANTIALIASEDLINEENABLE から状態を表示する、 **RenderState**のメンバー、 [ **D3DHAL\_DP2RENDERSTATE** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dhal/ns-d3dhal-_d3dhal_dp2renderstate)このオペレーション コードに関連付けられている構造体。 ドライバーが有効にまたは行のブール値から無効にするかどうかを決定します、 **dwState** D3DHAL のメンバー\_DP2RENDERSTATE します。 値**TRUE**を有効にすることを意味し、 **FALSE**を無効にすることを意味します。 このレンダリング状態の値の設定既定では、 **FALSE**します。

D3DRS\_ANTIALIASEDLINEENABLE レンダリング状態線の描画プリミティブ型と同じように、ワイヤ フレーム モードで描画される三角形に適用されます。

複数サンプルへのレンダリングでは、ターゲットをレンダリングするときに、ドライバーは、行アンチエイリアシングが有効にして、すべての行のエイリアスを表示する要求を無視する必要があります。

 

 






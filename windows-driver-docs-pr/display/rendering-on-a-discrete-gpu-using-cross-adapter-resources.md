---
title: クロス アダプター リソースを使用した個別の GPU でのレンダリング
description: Windows 8.1 以降では、不連続 GPU は、ビットブロック転送 (bitblt) または現在の操作の宛先としてクロスアダプタリソースを使用しますが、ストレッチやカラー変換は使用しません。オペレーティングシステムが、bitblt または現在の操作を実行するためにユーザーモード表示ドライバーに要求するリソース。統合 GPU では、デスクトップウィンドウマネージャー (DWM) による構成中に、クロスアダプターリソースをテクスチャとして使用します。GDI ハードウェアアクセラレータのレンダーターゲット。ディスプレイのプライマリ。3-d 操作のレンダーターゲットとしてではありません。
ms.assetid: 88CE2D2F-BBD8-4CE4-9183-BBFB0659990E
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a6fac0db449be83fe2bf7fe0fc8094278e23d2eb
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72829623"
---
# <a name="span-iddisplayrendering_on_a_discrete_gpu_using_cross-adapter_resourcesspanrendering-on-a-discrete-gpu-using-cross-adapter-resources"></a><span id="display.rendering_on_a_discrete_gpu_using_cross-adapter_resources"></span>クロスアダプターリソースを使用した個別の GPU でのレンダリング


Windows 8.1 以降では、[個別の GPU](using-cross-adapter-resources-in-a-hybrid-system.md)では次のように[クロスアダプターリソース](using-cross-adapter-resources-in-a-hybrid-system.md)が使用されるようになります。

-   ビットブロック転送 (bitblt) または現在の操作を対象としますが、拡大またはカラー変換は必要ありません。
-   Bitblt または現在の操作を実行するユーザーモード表示ドライバーをオペレーティングシステムが要求するリソース。

[統合 GPU](using-cross-adapter-resources-in-a-hybrid-system.md)では、[クロスアダプターリソース](using-cross-adapter-resources-in-a-hybrid-system.md)が次のように使用されます。

-   デスクトップウィンドウマネージャー (DWM) による合成中のテクスチャ。
-   [GDI ハードウェアアクセラレータ](gdi-hardware-acceleration.md)のレンダーターゲット。
-   ディスプレイのプライマリ。
-   3-d 操作のレンダーターゲットとしてではありません。

次のセクションでは、ハイブリッドシステム内の個別の GPU でアプリケーションがレンダリングされる3つのシナリオに関連するアーキテクチャとプロセスについて説明します。

## <a name="span-idredirected_bitblt_modelspanspan-idredirected_bitblt_modelspanredirected-bitblt-presentation-model"></a><span id="redirected_bitblt_model"></span><span id="REDIRECTED_BITBLT_MODEL"></span>表示された bitblt プレゼンテーションモデルのリダイレクト


![個別の gpu にレンダリングするためにアプリによって使用される、ハイブリッドグラフィックスリダイレクトされた bitblt モデル。](images/hybrid-graphics-arch-blit.png)

1.  トップレベルウィンドウのアダプター間リソースは、統合 GPU で標準の割り当てとしてカーネルモードで作成されます。
2.  このリソースが個別の GPU で開かれると、Microsoft DirectX graphics kernel subsystem (Dxgkrnl) は[*DxgkDdiGetStandardAllocationDriverData*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_getstandardallocationdriverdata)関数を呼び出し、同じバッキングストアを使用して、個別の gpu に新しいリソースを作成します ((大容量記憶装置) は、統合 GPU 用です。
3.  Microsoft Direct3D ランタイムは、独立した GPU のユーザーモード表示ドライバーに対して、プライベートドライバーデータを使用してクロスアダプターリソースを開くように指示します。
4.  DirectX アプリケーションは、バックバッファーリソースに対して個別の GPU でレンダリングします。 図の「Render」操作を参照してください。
5.  DirectX アプリケーションが**現在**のメソッドを呼び出すと、Direct3D ランタイムは個別の GPU のユーザーモードドライバーの[*present*](https://docs.microsoft.com/windows-hardware/drivers/ddi/dxgiddi/ns-dxgiddi-dxgi_ddi_base_functions) (または*pfnPresent*) 関数を呼び出して、バックバッファーをクロスアダプターリソースにコピーします。 図の "Present" 操作を参照してください。
6.  Windows グラフィックスデバイスインターフェイス (GDI) アプリケーションが最上位のウィンドウに表示されるときに、DirectX Graphics カーネルサブシステムは、統合 GPU のディスプレイミニポートドライバーの[*DxgkDdiRenderKm*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_renderkm)関数を呼び出し、クロスアダプターを示します。リソースはレンダーターゲットです。 図の GDI アプリケーションとクロスアダプターの画面の間の接続を確認します。
7.  DWM プロセスでは、統合 GPU 内のクロスアダプタリソースが開かれ、ソーステクスチャとしてコンポジション中に使用されます。 図の「合成」操作を参照してください。

## <a name="span-iddirect_flip_modelspanspan-iddirect_flip_modelspandirect-flip-presentation-model"></a><span id="direct_flip_model"></span><span id="DIRECT_FLIP_MODEL"></span>Direct フリッププレゼンテーションモデル


![個別の gpu にレンダリングするためにアプリによって使用されるハイブリッドグラフィックス direct フリップモデル。](images/hybrid-graphics-arch-flip.png)

1.  Direct3D ランタイムは、個々の GPU のユーザーモード表示ドライバーに対して、各スワップチェーン画面のクロスアダプタリソースを作成するように指示します。
2.  個別の GPU では、直接フリップモードが使用可能な場合、Direct3D ランタイムは[**D3DDDI\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dukmdt/ns-d3dukmdt-_d3dddi_allocationinfo)の割り当て情報構造の**Primary**メンバーと**VidPnSourceId**メンバーを設定することがあります。 これらのメンバー値は、 [*Pfnallocatecb*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_allocatecb)関数が呼び出されたときに渡される必要があります。
3.  Direct3D ランタイムは、統合 GPU のユーザーモード表示ドライバーに対して、DWM によって管理されるクロスアダプターリソースを開くように指示します。
4.  アプリケーションは、レンダリングターゲットテクスチャをターゲットとして使用して、個別の GPU にレンダリングします。 図の「Render」操作を参照してください。
5.  アプリケーションが**現在**のメソッドを呼び出すと、Direct3D ランタイムは、個別の GPU のユーザーモードドライバーの[*bltdxgi*](https://docs.microsoft.com/windows-hardware/drivers/ddi/dxgiddi/ns-dxgiddi-dxgi_ddi_base_functions) (または*pfnblt*) 関数を呼び出して、クロスアダプターリソースへのコピーを実行します。 次に、ランタイムは、独立した GPU のユーザーモードドライバーの使用中の[*dxgi*](https://docs.microsoft.com/windows-hardware/drivers/ddi/dxgiddi/ns-dxgiddi-dxgi_ddi_base_functions) (または*pfnPresent*) 関数を呼び出します。このとき、ソースはクロスアダプターリソースに設定され、ターゲット割り当ては**NULL**に設定されます。 図の「コピー」操作を参照してください。
6.  DWM は、統合 GPU のリソースを使用して合成を実行します。 直接フリップ操作が必要な場合は ([**DXGK\_SEGMENTFLAGS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/ns-d3dkmddi-_dxgk_segmentflags)。**DirectFlip**が設定されている場合) DWM は、統合された GPU のディスプレイミニポートドライバーに対して、1つのアダプターから別の割り当てへの反転操作を実行するように指示します。 図の「DWM フリップ」操作を参照してください。

## <a name="span-idfullscreen_modelspanspan-idfullscreen_modelspanfull-screen-model"></a><span id="fullscreen_model"></span><span id="FULLSCREEN_MODEL"></span>全画面モデル


1.  Direct3D ランタイムは、統合 GPU のユーザーモード表示ドライバーに対して、各スワップチェーン画面に対してクロスアダプタ共有プライマリ割り当てを作成するように指示します。
2.  Direct3D ランタイムは、クロスアダプターリソースを開くために、個別の GPU のユーザーモード表示ドライバーに指示します。
3.  アプリケーションは、レンダリングターゲットテクスチャをターゲットとして使用して、個別の GPU にレンダリングします。
4.  アプリケーションが**現在**のメソッドを呼び出すと、Direct3D ランタイムは、クロスアダプターリソースへのコピーを実行するように、個別の GPU のユーザーモード表示ドライバーに指示します。
5.  統合 GPU のユーザーモード表示ドライバーと表示ミニポートドライバーは、このクロスアダプターリソースに切り替えるように指示されます。

 

 






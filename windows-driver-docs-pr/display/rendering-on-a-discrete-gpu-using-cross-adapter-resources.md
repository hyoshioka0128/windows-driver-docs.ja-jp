---
title: クロス アダプターのリソースを使用して、独立した GPU でのレンダリング
description: Windows 8.1 以降、独立した GPU リソースを使用クロス アダプターを送信先としてビット ブロック転送 (bitblt) または現在の操作が拡大または色変換せずします。オペレーティング システムがユーザー モードを要求するリソースは、bitblt 関数に存在する操作を実行するドライバーを表示し、from.integrated GPU は、デスクトップ ウィンドウ マネージャー (DWM) での構成時にテクスチャとしてアダプター間のリソースを使用します。GDI ハードウェア アクセラレータのレンダー ターゲット。プライマリ ディスプレイ。3-D の操作のレンダー ターゲットとしてではなく。
ms.assetid: 88CE2D2F-BBD8-4CE4-9183-BBFB0659990E
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 91990d20e5d0f1b8781285a50ca026416f0da7b4
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56528787"
---
# <a name="span-iddisplayrenderingonadiscretegpuusingcross-adapterresourcesspanrendering-on-a-discrete-gpu-using-cross-adapter-resources"></a><span id="display.rendering_on_a_discrete_gpu_using_cross-adapter_resources"></span>クロス アダプターのリソースを使用して、独立した GPU でのレンダリング


以降では、Windows 8.1、[独立した GPU](using-cross-adapter-resources-in-a-hybrid-system.md)を使用して、[クロス アダプター リソース](using-cross-adapter-resources-in-a-hybrid-system.md)として。

-   ビット ブロック転送 (bitblt) または存在する操作が拡大または色の変換先。
-   オペレーティング システムがユーザー モードを要求するリソースは、bitblt 関数またはとの間に存在する操作を実行するドライバーを表示します。

[統合 GPU](using-cross-adapter-resources-in-a-hybrid-system.md)を使用して、[クロス アダプター リソース](using-cross-adapter-resources-in-a-hybrid-system.md)として。

-   デスクトップ ウィンドウ マネージャー (DWM) での構成時にテクスチャです。
-   レンダー ターゲットを[ハードウェア アクセラレータの GDI](gdi-hardware-acceleration.md)します。
-   プライマリ ディスプレイ。
-   3-D の操作のレンダー ターゲットとしてではなく。

以下のセクションでは、ハイブリッド システム内の個別の GPU 上でアーキテクチャとアプリケーションが表示される 3 つのシナリオに関連するプロセスについて説明します。

## <a name="span-idredirectedbitbltmodelspanspan-idredirectedbitbltmodelspanredirected-bitblt-presentation-model"></a><span id="redirected_bitblt_model"></span><span id="REDIRECTED_BITBLT_MODEL"></span>リダイレクトされた bitblt プレゼンテーション モデル


![ハイブリッドのグラフィックスには、不連続の gpu 上で表示するために、アプリによって使用される bitblt モデルがリダイレクトされます。](images/hybrid-graphics-arch-blit.png)

1.  最上位レベルのウィンドウのクロス アダプター リソースは、カーネル モードで統合された GPU 上で標準的な割り当てとして作成されます。
2.  このリソースが個別の GPU 上で開かれると、Microsoft DirectX グラフィックスのカーネル サブシステム (Dxgkrnl.sys) を呼び出す、 [ *DxgkDdiGetStandardAllocationDriverData* ](https://msdn.microsoft.com/library/windows/hardware/ff559673)関数を新たに作成します統合された GPU の場合と同じバッキング ストア (大容量記憶装置デバイス) を使用して個別の GPU 上でのリソースです。
3.  マイクロソフトの Direct3D ランタイムでは、独立した GPU のユーザー モードのディスプレイ ドライバーをプライベートのドライバーのデータを使用して、クロス アダプター リソースを開くように指示します。
4.  DirectX アプリケーションは、バック バッファー リソースを個別の GPU でレンダリングします。 図の「表示」操作を参照してください。
5.  DirectX アプリケーションを呼び出すと、**存在**メソッドは、Direct3D のランタイム呼び出し、 [ *PresentDXGI* ](https://msdn.microsoft.com/library/windows/hardware/ff569179) (または*pfnPresent*) の関数アダプターが複数のリソースにバック バッファーをコピーする独立した GPU のユーザー モード ドライバーです。 図に、"present が"操作を参照してください。
6.  DirectX グラフィックスのカーネルのサブシステムを呼び出す Windows グラフィックス デバイス インターフェイス (GDI) アプリケーションは、最上位ウィンドウにレンダリングするとき、 [ *DxgkDdiRenderKm* ](https://msdn.microsoft.com/library/windows/hardware/ff559800)関数の統合、GPU の表示ミニポート ドライバーとアダプター間のリソースがレンダー ターゲットであることを示します。 GDI のアプリケーションとの図に、クロス アダプター画面間の接続を参照してください。
7.  DWM プロセスでは、統合された GPU でクロス アダプター リソースを開くし、ソース テクスチャとしてコンポジション中に使用します。 図の「合成」操作を参照してください。

## <a name="span-iddirectflipmodelspanspan-iddirectflipmodelspandirect-flip-presentation-model"></a><span id="direct_flip_model"></span><span id="DIRECT_FLIP_MODEL"></span>直接フリップ プレゼンテーション モデル


![不連続の gpu 上で表示するために、アプリで使用される、フリップ モデルをハイブリッド グラフィックに指示します。](images/hybrid-graphics-arch-flip.png)

1.  Direct3D のランタイムでは、独立した GPU のユーザー モードのディスプレイ ドライバー各スワップ チェーン サーフェスのアダプターが複数のリソースを作成するように指示します。
2.  不連続の GPU 上で Direct3D ランタイム設定、**プライマリ**と**VidPnSourceId**のメンバー、 [ **D3DDDI\_ALLOCATIONINFO**](https://msdn.microsoft.com/library/windows/hardware/ff544364)直接反転モードが使用可能な場合に構造体します。 ときにこれらのメンバー値を渡す必要があります、 [ *pfnAllocateCb* ](https://msdn.microsoft.com/library/windows/hardware/ff568893)関数が呼び出されます。
3.  Direct3D のランタイムでは、統合された GPU のユーザー モードのディスプレイ ドライバーが DWM によって管理されるアダプター間のリソースを開くに指示します。
4.  アプリケーションは、変換先としてレンダー ターゲットのテクスチャを使用して個別の GPU 上でレンダリングします。 図の「表示」操作を参照してください。
5.  アプリケーションを呼び出すと、**存在**メソッドは、Direct3D のランタイム呼び出し、 [ *BltDXGI* ](https://msdn.microsoft.com/library/windows/hardware/ff538252) (または*pfnBlt*)、個別の関数アダプターが複数のリソースへのコピーを実行する GPU のユーザー モード ドライバーです。 ランタイムを呼び出して、 [ *PresentDXGI* ](https://msdn.microsoft.com/library/windows/hardware/ff569179) (または*pfnPresent*) 関数の独立した GPU のユーザー モード ドライバーでは、ソースとアダプター間のリソースに設定し、変換先の割り当てに設定**NULL**します。 図に、「コピー」操作を参照してください。
6.  DWM は、統合された GPU からリソースを使用してその構成を実行します。 直接の反転操作が必要な場合 ([**DXGK\_SEGMENTFLAGS**](https://msdn.microsoft.com/library/windows/hardware/ff562039).**DirectFlip**設定されている)、DWM は、統合された GPU の間のクロス アダプターの 1 つの割り当てからフリップ操作を実行するミニポート ドライバーを表示するように指示します。 図に、「DWM フリップ」操作を参照してください。

## <a name="span-idfullscreenmodelspanspan-idfullscreenmodelspanfull-screen-model"></a><span id="fullscreen_model"></span><span id="FULLSCREEN_MODEL"></span>全画面表示のモデル


1.  Direct3D のランタイムでは、統合された GPU のユーザー モードのディスプレイ ドライバー各スワップ チェーン サーフェスのクロス アダプターの共有プライマリ割り当てを作成するように指示します。
2.  Direct3D のランタイムでは、独立した GPU のユーザー モードのディスプレイ ドライバー間アダプター リソースを開くように指示します。
3.  アプリケーションは、レンダー ターゲットのテクスチャを使用して、変換先として、不連続の GPU でレンダリングします。
4.  アプリケーションを呼び出すと、**存在**メソッド、Direct3D ランタイム クロス アダプター リソースへのコピーを実行する独立した GPU のユーザー モードのディスプレイ ドライバーように指示します。
5.  統合された GPU のユーザー モードのディスプレイ ドライバーとディスプレイのミニポート ドライバーは、このアダプターの間のリソースに移動するように指示されます。

 

 






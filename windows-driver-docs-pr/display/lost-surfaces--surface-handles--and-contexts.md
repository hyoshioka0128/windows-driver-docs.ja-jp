---
title: 破棄されたサーフェス、サーフェス ハンドル、およびコンテキスト
description: 破棄されたサーフェス、サーフェス ハンドル、およびコンテキスト
ms.assetid: d2458077-56f8-481b-b612-a706e9560314
keywords:
- コンテキスト WDK Direct3D、D3dCreateSurfaceEx
- D3dCreateSurfaceEx
- surface が WDK Direct3D を処理する
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0ce6de0d5d06ea57a8a683051744182db4d24bd5
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72840596"
---
# <a name="lost-surfaces-surface-handles-and-contexts"></a>破棄されたサーフェス、サーフェス ハンドル、およびコンテキスト


## <span id="ddk_lost_surfaces_surface_handles_and_contexts_gg"></span><span id="DDK_LOST_SURFACES_SURFACE_HANDLES_AND_CONTEXTS_GG"></span>


一部のサーフェイスは、通常、これらのサーフェイスのハンドルをドライバーのコンテキストに格納することによって、コンテキスト (レンダーターゲット、Z バッファー、テクスチャなど) で参照される必要があります。 これらのサーフェイスは、ドライバーに関する限り、失われる可能性があります。 コンテキスト自体は存続する可能性がありますが、失われたサーフェイスに対して古い (無効) ハンドルがある可能性があります。 ランタイムは、この状態のときに、コンテキストにレンダリングコマンドが渡されないことを保証しますが、レンダリングを再び開始する前に、コンテキストを復元されたサーフェイスと再関連付けする方法に問題があります。 ランタイムは、失われたサーフェイスのハンドルが変更されないことを保証します。 これにより、コンテキストがそのサーフェイス (レンダーターゲット、Z、テクスチャ) へのハンドルを保持している場合、このコンテキストでレンダリングを再開する前に、これらのサーフェイスは常に*同じハンドル値を使用して*再作成 (復元) されます。

一部のドライバーの作成者は、すべての[**D3dDrawPrimitives2**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dhal/nc-d3dhal-lpd3dhal_drawprimitives2cb)呼び出しでハンドルを逆参照するのではなく、データをコンテキストに直接格納することによって、コンテキストの状態を最適化することができます。 この逆参照のコストは、 *D3dDrawPrimitives2*トークンのバッチを実行するコストと比較して小さくなる可能性があるため、この最適化は推奨されません。 ただし、ドライバーの作成者が必要とする場合は、復元時にサーフェイスが移動する可能性があることに注意する必要があります。 つまり、ハンドルが同じでも、同じ**Fpvidmem** (その作成時に、 [**DD\_surface\_グローバル**](https://docs.microsoft.com/windows/desktop/api/ddrawint/ns-ddrawint-_dd_surface_global)構造) ポインターのメンバーである場合、そのサーフェイスが復元されるという保証はありません。 このように最適化されたコンテキストは、古いビデオメモリポインターで終了する可能性があり、サーフェイスが移動した情報はありません。 これに対処する1つの方法として、ドライバーがコンテキストに関連付けられている場合 (レンダーターゲット、Z バッファー、またはテクスチャとして)、任意のサーフェイスにタグを付けることができます。 その後、 [**D3dCreateSurfaceEx**](https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_createsurfaceex)時に、このサーフェイスを参照する任意のコンテキストを検索し、そのコンテキストを更新できます。

1つのサーフェイスが複数のコンテキストに関連付けられる可能性があるため、サーフェイスがコンテキストへのポインターを保持することは推奨されません。

*失わ*れたサーフェイスの概念は、DirectDraw SDK ドキュメントで導入されました。 失われたサーフェイスは、DirectX 7.0 DDI モデルに何らかの影響を与えます。 詳細については、「 [DirectDraw サーフェスの紛失と復元](losing-and-restoring-directdraw-surfaces.md)」を参照してください。

 

 






---
title: 破棄されたサーフェス、サーフェス ハンドル、およびコンテキスト
description: 破棄されたサーフェス、サーフェス ハンドル、およびコンテキスト
ms.assetid: d2458077-56f8-481b-b612-a706e9560314
keywords:
- コンテキスト WDK の Direct3D D3dCreateSurfaceEx
- D3dCreateSurfaceEx
- 画面は、WDK Direct3D を処理します。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 80d234676d661bd18b87dd7d1e23f5fa0e3b7f9b
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67384839"
---
# <a name="lost-surfaces-surface-handles-and-contexts"></a>破棄されたサーフェス、サーフェス ハンドル、およびコンテキスト


## <span id="ddk_lost_surfaces_surface_handles_and_contexts_gg"></span><span id="DDK_LOST_SURFACES_SURFACE_HANDLES_AND_CONTEXTS_GG"></span>


サーフェスの一部がで参照されます (レンダー ターゲット、Z バッファー、テクスチャなど)、コンテキストを通常、ドライバーのコンテキストでこれらのサーフェスのハンドルを格納することで。 ドライバーがに関する限り、これらのサーフェスを (破棄) 失わになる可能性があります。 コンテキスト自体は存続可能性がありますが、失われたサーフェスに (無効) ハンドルが古いことがあります。 ランタイムは、ことレンダリング コマンドに渡されないコンテキスト間にこの状態では、レンダリングをもう一度開始前に、復元されたサーフェスとコンテキストを再関連付けする方法の問題が引き続きを保証します。 ランタイムは、失われたサーフェスのハンドルを変更しないことを保証します。 さらにこう場合にそのサーフェス (レンダー ターゲット、Z、およびテクスチャ) し、これらのサーフェスはハンドルが常に再作成されます (復元) コンテキスト*と同じ値を処理する*前に、レンダリングは、このコンテキストで再開できます。

いくつかのドライバー開発者がハンドルを逆参照での作業を行うのではなく、直接コンテキストでは、画面のデータを格納するによって、コンテキストの状態を最適化することができますすべて[ **D3dDrawPrimitives2** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dhal/nc-d3dhal-lpd3dhal_drawprimitives2cb)を呼び出す. この逆参照のコストが小さいする可能性がありますのでがのバッチ実行のコストを比較*D3dDrawPrimitives2*トークンは、この最適化がお勧めできません。 ただし、これを行う場合ドライバー開発者は、し、必要があるサーフェスを移動、復元するときに注意してください。 つまり、ハンドルは同じだがないこと、サーフェイスが同じ復元されていることを保証**fpVidMem** (のメンバー、 [ **DD\_画面\_GLOBAL**](https://docs.microsoft.com/windows/desktop/api/ddrawint/ns-ddrawint-_dd_surface_global)構造) が作成されたポインター。 この方法で最適化されたコンテキストは可能性があります最終的に古いビデオ メモリのポインターをサーフェスが移動される情報はありません。 これに対処する 1 つのメソッドは、(ターゲット、Z バッファー、またはテクスチャのレンダリング) とコンテキストに関連付けられているときに、ドライバーが任意の画面をタグ可能性があります。 [ **D3dCreateSurfaceEx** ](https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_createsurfaceex)時刻では、この画面を参照し、そのコンテキストを更新する任意のコンテキストを検索できます。

1 つの画面が 1 つ以上のコンテキストに関連付けられている可能性があるためサーフェスがコンテキストを指すポインターを維持することがないお勧めします。

概念*失わ*サーフェスは、DirectDraw SDK ドキュメントで導入されました。 失われたサーフェスでは、DirectX 7.0 DDI モデルでいくつかに影響を与えます。 詳細については、次を参照してください。[データが失われると DirectDraw サーフェスの復元](losing-and-restoring-directdraw-surfaces.md)します。

 

 






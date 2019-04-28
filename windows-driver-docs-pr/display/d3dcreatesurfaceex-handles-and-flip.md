---
title: D3dCreateSurfaceEx ハンドルと反転
description: D3dCreateSurfaceEx ハンドルと反転
ms.assetid: b87762fd-444d-437a-b076-189f51cc6dd1
keywords:
- コンテキスト WDK の Direct3D D3dCreateSurfaceEx
- D3dCreateSurfaceEx
- WDK Direct3D の反転
- DdFlip
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2d2fb024d700610bdd7ac6423f41444ac23f53b5
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63371505"
---
# <a name="d3dcreatesurfaceex-handles-and-flip"></a>D3dCreateSurfaceEx ハンドルと反転


## <span id="ddk_d3dcreatesurfaceex_handles_and_flip_gg"></span><span id="DDK_D3DCREATESURFACEEX_HANDLES_AND_FLIP_GG"></span>


DirectDraw surface 構造体は、サーフェスの概念、ビデオ メモリで必ずしも固有ではない場所を表すために設計されています。 この抽象化の主な使用が、アプリケーション オブジェクトを使用して 1 つ定数サーフェス バック バッファーを表す場合でも、移動の結果としてビデオ メモリのバック バッファーがあります、プライマリのフリッピング チェーン内では、 [ *DdFlip* ](https://msdn.microsoft.com/library/windows/hardware/ff549306)関数。

[ *DdFlip* ](https://msdn.microsoft.com/library/windows/hardware/ff549306)関数サーフェスのリングを受け取り、ビデオ メモリのポインターに関するこのリングを順番に再割り当ています。 画面の 2 つのオブジェクトの特定のケースでは、プロセスは、ビデオ メモリのポインターを取引先に縮小されます。 さらに、DirectDraw ランタイム ローテーションも行われます、 [ **D3dCreateSurfaceEx** ](https://msdn.microsoft.com/library/windows/hardware/ff542840)それぞれの面とのドライバーが所有している内容に関連付けられたハンドル、 **dwReserved1**各画面のメンバー。 この動作は、DirectX 7.0 のドライバーとドライバーの表面の構造体の内部 DirectDraw surface 構造へのポインターの埋め込みを規則に効果的にいくつかの興味深い影響です。

2 つ表面のオブジェクト、A と B の H のハンドルに関連付けられている<sub>A</sub>および H<sub>B</sub>、および**fpVidMem** (のメンバー、 [ **DD\_画面\_グローバル**](https://msdn.microsoft.com/library/windows/hardware/ff551726)構造) の F 値<sub>A</sub>と F<sub>B</sub>。 さらに、アプリケーションがフリッピング チェーンのバック バッファーを指す A サーフェスの構造を使用するいるとします。 [ *DdFlip* ](https://msdn.microsoft.com/library/windows/hardware/ff549306)時間やハンドル**fpVidMem**サーフェス A がある H ため、値が交換されます<sub>B</sub>と F<sub>B</sub>、サーフェス B は、H<sub>A</sub>と F<sub>A</sub>します。 バック バッファーに描画、F でのビデオ メモリを表す必要があります A のサーフェスしようとアプリケーションを今すぐ<sub>B</sub> (アプリケーションへの呼び出しを開始するため、 *DdFlip*)。

描画コマンドが、ドライバーは、そのサーフェイスに関連付けられたハンドルに発行された (H を<sub>B</sub>、時間ではなく<sub>A</sub>)。 ドライバーは単なる DirectDraw surface 構造体へのポインターを保存する場合は何が起こるでしょうか。 ドライバーを検索 H<sub>B</sub>、B、画面に格納されているポインターの後に続く、 **fpVidMem** F の値<sub>A</sub>します。 F でのビデオ メモリの描画を開始<sub>A</sub>します。 これではないアプリケーションで想定される内容です。 構造体、し、H の画面、DirectDraw へのポインターを後ではなく一方で、ドライバーは、独自の構造で surface データを保存する場合は、<sub>B</sub> F にまだ解決<sub>B</sub>で描画が発生して、正しい面です。 この後者の場合は、現在 DDI が実装されている方法です。

 

 






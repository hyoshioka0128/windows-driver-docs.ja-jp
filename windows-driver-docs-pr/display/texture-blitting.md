---
title: テクスチャ ビット ブロックの転送
description: テクスチャ ビット ブロックの転送
ms.assetid: 5a2e49c1-e99d-4b0d-a46c-b22b3dcefaf8
keywords:
- blt WDK Direct3D
- テクスチャ管理 WDK Direct3D、中
- WDK Direct3D 中
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6b37648cfed2fee5928f777bd88386f1ac682fd1
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63362619"
---
# <a name="texture-blitting"></a>テクスチャ ビット ブロックの転送


## <span id="ddk_texture_blitting_gg"></span><span id="DDK_TEXTURE_BLITTING_GG"></span>


DirectX の 7.0 で導入された、Direct3D DDI の重要な変更は、テクスチャは、トークン内に埋め込むことによって、ブリットこと、 [ **D3dDrawPrimitives2** ](https://msdn.microsoft.com/library/windows/hardware/ff544704)コマンド ストリーム。 このトークンは D3DDP2OP\_TEXBLT、または、ローカルまたは非ローカルのビデオ メモリにバッキング サーフェスからの転送、テクスチャのあるドライバーを通知します。

従来からのテクスチャの内部ハンドルを作成するために縛られるドライバーの代わりにも、 *D3dTextureCreate*と*D3dTextureDestroy*コールバック、ランタイムは今すぐハンドルを割り当てますDirect3D のコンテキスト内で作成される各 DirectDrawSurface オブジェクトの数。 このハンドルの数について、ドライバーがシグナル状態、 [ **D3dCreateSurfaceEx** ](https://msdn.microsoft.com/library/windows/hardware/ff542840)コールバック。

*D3dCreateSurfaceEx*が呼び出された後、すべてのハードウェア アブストラクション レイヤー (HAL) [ *DdCreateSurface* ](https://msdn.microsoft.com/library/windows/hardware/ff549263)の呼び出しが完了します。 *D3dCreateSurfaceEx*すべて内部のハードウェアのエミュレーション層 (HEL) した後もいいます**CreateSurface**の呼び出しが完了します。 HEL 呼び出しは、通常、バッキング DirectDrawSurface オブジェクトが作成されたときに発生します。 これらの呼び出しは、Direct3D コンテキストが作成された前後に発生する可能性があります[ **D3dContextCreate**](https://msdn.microsoft.com/library/windows/hardware/ff542178)します。

また、アプリケーションが実行されているときに、呼び出しを[ **D3dDestroyDDLocal** ](https://msdn.microsoft.com/library/windows/hardware/ff544685)をクリーンアップして、これらのサーフェスで明示的に作成されたドライバー データを破棄します。 この呼び出しが行われるは、Direct3D コンテキストが作成される前にもします。 これは、クリーンアップされていない任意のコンテキストに関連付けられているダーティ ハンドルがないことを確認します。 これは、予防策を破棄しないように実際に何もコンテキストが正しく使用後にクリーンアップする場合だけです。

 

 






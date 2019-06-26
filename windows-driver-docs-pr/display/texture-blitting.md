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
ms.openlocfilehash: 979ab81556882a84dfa4d65177184444428196e2
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67353434"
---
# <a name="texture-blitting"></a>テクスチャ ビット ブロックの転送


## <span id="ddk_texture_blitting_gg"></span><span id="DDK_TEXTURE_BLITTING_GG"></span>


DirectX の 7.0 で導入された、Direct3D DDI の重要な変更は、テクスチャは、トークン内に埋め込むことによって、ブリットこと、 [ **D3dDrawPrimitives2** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dhal/nc-d3dhal-lpd3dhal_drawprimitives2cb)コマンド ストリーム。 このトークンは D3DDP2OP\_TEXBLT、または、ローカルまたは非ローカルのビデオ メモリにバッキング サーフェスからの転送、テクスチャのあるドライバーを通知します。

従来からのテクスチャの内部ハンドルを作成するために縛られるドライバーの代わりにも、 *D3dTextureCreate*と*D3dTextureDestroy*コールバック、ランタイムは今すぐハンドルを割り当てますDirect3D のコンテキスト内で作成される各 DirectDrawSurface オブジェクトの数。 このハンドルの数について、ドライバーがシグナル状態、 [ **D3dCreateSurfaceEx** ](https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_createsurfaceex)コールバック。

*D3dCreateSurfaceEx*が呼び出された後、すべてのハードウェア アブストラクション レイヤー (HAL) [ *DdCreateSurface* ](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff549263(v=vs.85))の呼び出しが完了します。 *D3dCreateSurfaceEx*すべて内部のハードウェアのエミュレーション層 (HEL) した後もいいます**CreateSurface**の呼び出しが完了します。 HEL 呼び出しは、通常、バッキング DirectDrawSurface オブジェクトが作成されたときに発生します。 これらの呼び出しは、Direct3D コンテキストが作成された前後に発生する可能性があります[ **D3dContextCreate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dhal/nc-d3dhal-lpd3dhal_contextcreatecb)します。

また、アプリケーションが実行されているときに、呼び出しを[ **D3dDestroyDDLocal** ](https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_destroyddlocal)をクリーンアップして、これらのサーフェスで明示的に作成されたドライバー データを破棄します。 この呼び出しが行われるは、Direct3D コンテキストが作成される前にもします。 これは、クリーンアップされていない任意のコンテキストに関連付けられているダーティ ハンドルがないことを確認します。 これは、予防策を破棄しないように実際に何もコンテキストが正しく使用後にクリーンアップする場合だけです。

 

 






---
title: テクスチャ ビット ブロックの転送
description: テクスチャ ビット ブロックの転送
ms.assetid: 5a2e49c1-e99d-4b0d-a46c-b22b3dcefaf8
keywords:
- blt WDK Direct3D
- テクスチャ管理 WDK Direct3D、blitting
- blitting WDK Direct3D
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d6d4b49923cdfc75a2b12c9f3a400db5add5f89d
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72829332"
---
# <a name="texture-blitting"></a>テクスチャ ビット ブロックの転送


## <span id="ddk_texture_blitting_gg"></span><span id="DDK_TEXTURE_BLITTING_GG"></span>


DirectX 7.0 で導入された Direct3D DDI の重要な変更点は、 [**D3dDrawPrimitives2**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dhal/nc-d3dhal-lpd3dhal_drawprimitives2cb)コマンドストリームにトークンを埋め込むことによってテクスチャを blitted することです。 このトークンは D3DDP2OP\_TEXBLT で、テクスチャをバッキングサーフェイスからローカルまたは非ローカルのビデオメモリに転送する必要があることをドライバーに通知します。

また、レガシ*D3dTextureCreate*と*D3dTextureDestroy*コールバックを使用してテクスチャの内部ハンドルを作成するためのドライバーではなく、ランタイムは、次のような各 directdrawsurface オブジェクトにハンドル番号を割り当てます。Direct3D コンテキスト内で作成されます。 ドライバーは、 [**D3dCreateSurfaceEx**](https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_createsurfaceex)コールバックを介して、このハンドル番号について通知されます。

*D3dCreateSurfaceEx*は、すべてのハードウェアアブストラクションレイヤー (HAL) の[*Dd urface*](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff549263(v=vs.85))の呼び出しが完了した後に呼び出されます。 *D3dCreateSurfaceEx*は、内部ハードウェアエミュレーションレイヤー ( **HEL) の**すべての呼び出しが完了した後にも呼び出されます。 HEL 呼び出しは、通常、バッキング DirectDrawSurface オブジェクトが作成されるときに発生します。 これらの呼び出しは、 [**D3dContextCreate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dhal/nc-d3dhal-lpd3dhal_contextcreatecb)で Direct3D コンテキストが作成される前と後に発生する可能性があります。

また、アプリケーションが実行されている場合は、 [**D3dDestroyDDLocal**](https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_destroyddlocal)に対して、これらのサーフェイスに対して明示的に作成されたドライバーデータをクリーンアップおよび破棄するための呼び出しが行われます。 この呼び出しは、Direct3D コンテキストが作成される前にも行われます。 これは、クリーンアップされていないコンテキストに関連付けられているダーティハンドルがないことを確認するために行われます。 これは、コンテキストが使用後に適切にクリーンアップされた場合に、実際には何も破棄しないようにする必要がある単なる予防措置です。

 

 






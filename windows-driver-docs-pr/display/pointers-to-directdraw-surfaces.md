---
title: DirectDraw サーフェスへのポインター
description: DirectDraw サーフェスへのポインター
ms.assetid: 5d7c8b22-d2d3-4e40-b7b2-7277e051812c
keywords:
- コンテキスト WDK Direct3D、DirectDraw surface ポインター
- DirectDraw surface ポインター WDK Direct3D
- DirectDraw WDK Direct3D の surface ポインター
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7200c160ec3a2a8a5fda4b23e953fcc9c07f6cbc
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72829781"
---
# <a name="pointers-to-directdraw-surfaces"></a>DirectDraw サーフェスへのポインター


## <span id="ddk_pointers_to_directdraw_surfaces_gg"></span><span id="DDK_POINTERS_TO_DIRECTDRAW_SURFACES_GG"></span>


ドライバーの作成者は、DirectDrawSurface データ構造体へのポインターを、独自のドライバー側のサーフェイス構造体内に保持しようとしている可能性があります。 ただし、この方法は Microsoft Windows 2000 以降では成功しません。これは、DirectDraw カーネル側のデータ構造へのアクセスが、ユーザーモードとドライバーからこれらの構造を分離する管理スキームによって仲介されるためです。 [**EngLockDirectDrawSurface**](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-englockdirectdrawsurface)は、 [**EngUnlockDirectDrawSurface**](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-engunlockdirectdrawsurface)ルーチンが呼び出されるまで有効な構造体へのポインターを提供します。

このロック/ロック解除のペアの外部では、構造は同じ場所に存在する (存在する) ことは保証されていません。 また、これらのロック/ロック解除の組み合わせによってパフォーマンスが低下します。 ドライバーが surface 構造の独自のコピーを保持している場合、ロックは必要ありません。 ドライバー側の表面構造内のデータの更新は、 [**D3dCreateSurfaceEx**](https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_createsurfaceex)のような低頻度の呼び出し中に行われます。 結果として、 [**D3dDrawPrimitives2**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dhal/nc-d3dhal-lpd3dhal_drawprimitives2cb)のような頻度の高い呼び出しでは、少ないコードを実行する必要があります。

 

 






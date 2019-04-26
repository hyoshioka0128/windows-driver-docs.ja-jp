---
title: DirectDraw サーフェスへのポインター
description: DirectDraw サーフェスへのポインター
ms.assetid: 5d7c8b22-d2d3-4e40-b7b2-7277e051812c
keywords:
- コンテキスト WDK Direct3D、DirectDraw surface ポインター
- DirectDraw surface ポインター WDK Direct3D
- DirectDraw WDK Direct3D のサーフェスのポインター
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8486c612054cf5e7f54bbf659bc173f57f9663e7
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63352214"
---
# <a name="pointers-to-directdraw-surfaces"></a>DirectDraw サーフェスへのポインター


## <span id="ddk_pointers_to_directdraw_surfaces_gg"></span><span id="DDK_POINTERS_TO_DIRECTDRAW_SURFACES_GG"></span>


ドライバーの作成者をプライベート ドライバー側サーフェス構造体内 DirectDrawSurface データ構造体へのポインターを保持してしまう可能性があります。 ただし、この実習は成功しません Microsoft Windows 2000 以降で DirectDraw カーネル側のデータ構造へのアクセスがユーザー モードとドライバーからこれらの構造の影響を受けないようにする管理スキームを通じて仲介ためです。 [**EngLockDirectDrawSurface** ](https://msdn.microsoft.com/library/windows/hardware/ff564966)まで有効な構造体へのポインター、 [ **EngUnlockDirectDrawSurface** ](https://msdn.microsoft.com/library/windows/hardware/ff565042)ルーチンが呼び出されます。

このロック/ロック解除のペアの外部に存在すると、または存在しても、同じ場所に、構造体は保証されません。 さらに、これらのロック/ロック解除のペアによってパフォーマンス低下します。 ドライバーは、独自のサーフェスの構造体のコピーを保持している場合、ロックは必要ありません。 などの低頻度の呼び出し中にドライバー側サーフェス構造内のデータへの更新が行われる[ **D3dCreateSurfaceEx**](https://msdn.microsoft.com/library/windows/hardware/ff542840)します。 結果は、のような頻度の高い呼び出し中に少ないコードを実行する必要がある[ **D3dDrawPrimitives2**](https://msdn.microsoft.com/library/windows/hardware/ff544704)します。

 

 






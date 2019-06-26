---
title: 圧縮された SysMem で作成したテクスチャ サーフェスの処理
description: システム メモリ内で作成された圧縮テクスチャ サーフェスの処理
ms.assetid: 773962ce-f459-4dc5-8311-c43ae33cfb7c
keywords:
- 描画圧縮テクスチャ WDK DirectDraw、システム メモリに関する考慮事項
- DirectDraw 圧縮テクスチャ WDK Windows 2000 を表示、システム メモリに関する考慮事項
- 圧縮されたテクスチャ サーフェス WDK DirectDraw、システム メモリに関する考慮事項
- WDK DirectDraw、圧縮されたテクスチャを表示します。
- 圧縮テクスチャ WDK DirectDraw、
- 描画圧縮テクスチャ WDK DirectDraw、幅
- DirectDraw 圧縮テクスチャ WDK Windows 2000 では、表示幅
- 圧縮されたテクスチャ サーフェス WDK DirectDraw、幅
- 描画圧縮テクスチャ WDK DirectDraw、高さ
- DirectDraw 圧縮テクスチャ WDK Windows 2000 を表示する高さ
- 圧縮されたテクスチャ サーフェス WDK DirectDraw、高さ
ms.date: 12/06/2018
ms.localizationpriority: medium
ms.custom: seodec18
ms.openlocfilehash: 0ffab42f64f4247c745d736b0553d3fca18da742
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67382321"
---
# <a name="handling-compressed-texture-surfaces-created-in-system-memory"></a>システム メモリ内で作成された圧縮テクスチャ サーフェスの処理

**このトピックでは、Windows NT ベースのオペレーティング システムにのみ適用されます。**

システム メモリ内で作成された圧縮テクスチャ サーフェスの高さと幅は、適切なメモリ量を割り当てること、カーネル モードのランタイムを強制的にユーザー モードのランタイムによって変更されます。 ディスプレイ ドライバーは、障害が発生したからこの画面上で実行される後続の操作を回避するには、この変更を取り消す必要があります。 DirectDraw ランタイムが、ドライバーを呼び出すたびに[ **D3dCreateSurfaceEx** ](https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_createsurfaceex)圧縮テクスチャ サーフェスを作成する機能、ドライバーは、幅と、画面の高さを復元する必要があります、変更されていない状態です。

ドライバーの*D3dCreateSurfaceEx*関数は、画面の幅、ピッチ、および高さが次のように変更を受け取ります。

-   幅とピッチ ブロックのサイズを乗算行で 4 x 4 ブロックの数が含まれます。

-   高さには、列内の 4 x 4 ブロックの数が含まれています。

次のコード スニペットでは、計算、ドライバーは、幅と、画面の高さの復元を実行する必要がありますを示しています。

```cpp
RealWidth = (Width / Block size) * 4;
RealHeight = Height * 4;
```

ドライバーは、カーネルの内のメンバーに復元された幅と高さの値を割り当てる必要があります[ **DD\_画面\_GLOBAL** ](https://docs.microsoft.com/windows/desktop/api/ddrawint/ns-ddrawint-_dd_surface_global)構造を表示します。 これにより、DirectDraw を防止 DXT テクスチャを拒否するカーネル モードのランタイムが、幅と高さの値が一致しないために、blt をダウンロードします。 ドライバーのままでサイズ変更された場合、 **wWidth**と**wHeight** DD のメンバー\_画面\_グローバル、DirectDraw カーネル モードのランタイムは、blt からを拒否します幅と高さが変更されていない座標であると、ソースの変更の DD の「外部」ことだと思いますので、ビデオ メモリ画面へのシステム メモリ領域が変更される\_画面\_グローバル サイズ。

 

 






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
ms.openlocfilehash: 31b84bfb1387bc43bb30f260a83a98e86aed126f
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63323793"
---
# <a name="handling-compressed-texture-surfaces-created-in-system-memory"></a>システム メモリ内で作成された圧縮テクスチャ サーフェスの処理

**このトピックでは、Windows NT ベースのオペレーティング システムにのみ適用されます。**

システム メモリ内で作成された圧縮テクスチャ サーフェスの高さと幅は、適切なメモリ量を割り当てること、カーネル モードのランタイムを強制的にユーザー モードのランタイムによって変更されます。 ディスプレイ ドライバーは、障害が発生したからこの画面上で実行される後続の操作を回避するには、この変更を取り消す必要があります。 DirectDraw ランタイムが、ドライバーを呼び出すたびに[ **D3dCreateSurfaceEx** ](https://msdn.microsoft.com/library/windows/hardware/ff542840)圧縮テクスチャ サーフェスを作成する機能、ドライバーは、幅と、画面の高さを復元する必要があります、変更されていない状態です。

ドライバーの*D3dCreateSurfaceEx*関数は、画面の幅、ピッチ、および高さが次のように変更を受け取ります。

-   幅とピッチ ブロックのサイズを乗算行で 4 x 4 ブロックの数が含まれます。

-   高さには、列内の 4 x 4 ブロックの数が含まれています。

次のコード スニペットでは、計算、ドライバーは、幅と、画面の高さの復元を実行する必要がありますを示しています。

```cpp
RealWidth = (Width / Block size) * 4;
RealHeight = Height * 4;
```

ドライバーは、カーネルの内のメンバーに復元された幅と高さの値を割り当てる必要があります[ **DD\_画面\_GLOBAL** ](https://msdn.microsoft.com/library/windows/hardware/ff551726)構造を表示します。 これにより、DirectDraw を防止 DXT テクスチャを拒否するカーネル モードのランタイムが、幅と高さの値が一致しないために、blt をダウンロードします。 ドライバーのままでサイズ変更された場合、 **wWidth**と**wHeight** DD のメンバー\_画面\_グローバル、DirectDraw カーネル モードのランタイムは、blt からを拒否します幅と高さが変更されていない座標であると、ソースの変更の DD の「外部」ことだと思いますので、ビデオ メモリ画面へのシステム メモリ領域が変更される\_画面\_グローバル サイズ。

 

 






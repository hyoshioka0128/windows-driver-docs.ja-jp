---
title: 表示メモリ
description: 表示メモリ
ms.assetid: 92092bf2-dc31-4781-82c6-3365df77af99
keywords:
- 表示メモリに関するメモリ WDK DirectDraw、表示します。
- 表示メモリに関するメモリ WDK DirectDraw、描画
- メモリに関する、DirectDraw メモリ WDK Windows 2000 の表示します。
- メモリに関するメモリ WDK DirectDraw、
- 描画メモリ WDK DirectDraw
- DirectDraw メモリ WDK Windows 2000 の表示
- メモリ WDK DirectDraw
- メモリ WDK DirectDraw を表示します。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8540a92be9ef8a32bc98da934c9424fe07b3068f
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56582090"
---
# <a name="display-memory"></a>表示メモリ


## <span id="ddk_display_memory_gg"></span><span id="DDK_DISPLAY_MEMORY_GG"></span>


一般に、DirectDraw をできる限り表示メモリがはるかに割り当てること表示パフォーマンスが向上し、ゲームや高速より優れた品質の視覚的イメージに実行するには、その他の DirectDraw アプリケーションを使用します。

通常、ピッチを右側にメモリを消費しないように、ディスプレイの幅に設定のあるディスプレイ カード (概念的には) フロント バッファーの。 これにより、その他のサーフェスを使用できる概念下部にある 1 つのスクラッチ領域が残ります。 メモリ アクセスには 1 つのポインターが表示アクセス可能なメモリの領域全体を参照できるため、ここでは非常に簡単です。

ピッチがプライマリの画面の幅よりも大きい場合は、フロント バッファーの概念の右側にメモリが無駄になります。 これは、カード上のメモリが直線または四角形がかどうかに関係なく、独立した四角形のヒープとして再利用します。 (場合でも、メモリは、線形、いくつか表示ドライバーの修正プログラム、ブリット機能を高速化、声の高さ。 はなく、ドライバーを書き換えるより、メモリだけ再利用できます独立したヒープとして。)

 

 






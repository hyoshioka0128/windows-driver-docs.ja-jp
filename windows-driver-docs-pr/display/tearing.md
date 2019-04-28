---
title: テアリング
description: テアリング
ms.assetid: b4c21592-cbdf-4dd6-9457-71d53b9f7b32
keywords:
- WDK DirectDraw を破棄します。
- ページ フリップ WDK DirectDraw を描画、解除を行う
- DirectDraw WDK Windows 2000 の表示を切り替える、解除を行う
- WDK DirectDraw を反転の解除を行うページ
- WDK DirectDraw を反転、解除を行う
- WDK の DirectDraw を画面の回転
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3108ef2a8f3125ed4faf83f41fbefc56c7cf114f
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63362720"
---
# <a name="tearing"></a>テアリング


## <span id="ddk_tearing_gg"></span><span id="DDK_TEARING_GG"></span>


説明したように、 [Flipping](flipping.md)セクション、フリップは、表示メモリの新しいリージョンを指すように基本的にメモリのポインターを変更 (permedia2 チップのサンプル コードを参照してください)。 画面から離れる反転されている必要があります終了処理を可能性があります (次の図に示すように)、またはアプリケーションが、blt をロックします。 または、そのメモリを変更する前に表示されているが完了しました。

![図の解除を行う方法を示すおよびなしの解除を行う](images/ddfig8.png)

終了処理に反転される画面の反転の中に書き込まれたデータがある場合にも発生します。 分裂はユニバーサルおよびが行われるときに毎回イメージが描画され、同時に表示されています。 高速なフレーム レートは、この問題を解決できません。 プライマリ サーフェス、オーバーレイ、およびテクスチャはすべて DirectDraw サーフェスであるため、ことができます反転同様に、解除を行うようにします。

終了処理が発生するは、ページ フリップまたは blt が不適切なタイミングで行われます。 たとえば、モニターのスキャン ラインは、上記の図の破線で表される、サーフェイスの表示の途中では、ページが反転、終了処理が発生します。 (例のように、下の図の) 全体の画面が表示された後にのみ発生するページ フリップのタイミングで、終了処理を回避できます。 終了処理は、表示されているプロセスでは、画面に中ときも発生します。

 

 






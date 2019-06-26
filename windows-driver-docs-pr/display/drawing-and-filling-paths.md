---
title: パスの描画と塗りつぶし
description: パスの描画と塗りつぶし
ms.assetid: bc31aeba-d1f1-4e38-a8df-19e8d7e178c7
keywords:
- GDI WDK Windows 2000 の表示パス
- グラフィックス ドライバー WDK Windows 2000 の表示、パス
- WDK の GDI やパスの描画
- WDK GDI のパスを入力
- WDK GDI のパス
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3ec62cd3663ca2c3fe534d62eac8daa2aba75bd3
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67365728"
---
# <a name="drawing-and-filling-paths"></a>パスの描画と塗りつぶし


## <span id="ddk_drawing_and_filling_paths_gg"></span><span id="DDK_DRAWING_AND_FILLING_PATHS_GG"></span>


グラフィック ドライバーは、線、またはパスのオブジェクトによって定義された曲線のシーケンスへのパスを考慮 ([**PATHOBJ** ](https://docs.microsoft.com/windows/desktop/api/winddi/ns-winddi-_pathobj)構造)。 閉じたパスの入力を処理するには、ドライバーは、関数をサポートしています。 [ **DrvFillPath**](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvfillpath)します。

GDI を呼び出すことができます[ **DrvFillPath** ](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvfillpath)デバイス管理の画面上のパスを入力します。 GDI の塗りつぶしの要件を比較し、 [ **DEVINFO** ](https://docs.microsoft.com/windows/desktop/api/winddi/ns-winddi-tagdevinfo)構造体のフラグ GCAPS\_ベジエ曲線、GCAPS\_ALTERNATEFILL、および GCAPS\_WINDINGFILL をドライバーを呼び出すかどうかを決定します。 GDI は、ドライバーを呼び出す場合、ドライバーか、操作または戻り値は、要求されたパスまたはクリッピングは複雑すぎるため、デバイスによって処理されるは GDI の通知が実行します。 後者の場合は、GDI は、要求をいくつかの簡単操作に分割します。

ドライバーは、省略可能なサポートも[ **DrvStrokeAndFillPath** ](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvstrokeandfillpath)パスの入力を要求する関数。 この関数は、入力し、同時に、パスの輪郭を描きます。 多くの GDI プリミティブでは、この機能が必要です。 太線は、線の描画に使用する場合は、境界のパスの増大幅を補正するために、塗りつぶされた領域を減らす必要があります。

ドライバーが返されるときに**FALSE**いずれかから、 [ **DrvFillPath** ](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvfillpath)または[ **DrvStrokeAndFillPath** ](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvstrokeandfillpath)関数、GDI がより単純な操作のセットにパスの塗りつぶしの要求を変換し、再度ドライバー関数の呼び出しを実行します。 デバイスを返す場合**FALSE** 2 番目の呼び出しで再度**DrvFillPath**、GDI パス クリップ オブジェクトに変換しを呼び出して[ **EngFillPath** ](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-engfillpath). **FALSE**場合に返す**DrvStrokeAndFillPath**が再現されている呼び出しをキューに個別の呼び出しに変換できるの GDI [ **DrvStrokePath** ](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvstrokepath)**DrvFillPath**します。

 

 






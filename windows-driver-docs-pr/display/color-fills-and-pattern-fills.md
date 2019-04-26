---
title: 色による塗りつぶしとパターンの塗りつぶし
description: 色による塗りつぶしとパターンの塗りつぶし
ms.assetid: 6e597405-e40f-4cb8-b177-896681745e00
keywords:
- 描画 blt WDK DirectDraw、色を設定します。
- DirectDraw 中 WDK Windows 2000 の表示色で塗りつぶさ
- 中 WDK DirectDraw、色で塗りつぶさ
- blt WDK DirectDraw、色を設定します。
- サーフェス WDK DirectDraw、中
- 描画 blt WDK DirectDraw、パターンの塗りつぶし
- DirectDraw 中 WDK Windows 2000 の表示、パターンの塗りつぶし
- 中 WDK DirectDraw、パターンの塗りつぶし
- blt WDK DirectDraw、パターンの塗りつぶし
- 色で塗りつぶさ WDK DirectDraw
- WDK DirectDraw パターンの塗りつぶし
- 塗りつぶしの色 WDK DirectDraw
- 塗りつぶしのパターン WDK DirectDraw
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: cd9893a8932f712f26b16960bdc1540949c25c39
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63354236"
---
# <a name="color-fills-and-pattern-fills"></a>色による塗りつぶしとパターンの塗りつぶし


## <span id="ddk_color_fills_and_pattern_fills_gg"></span><span id="DDK_COLOR_FILLS_AND_PATTERN_FILLS_GG"></span>


色の塗りつぶしを四角形による記述では、特定の色で画面の領域を塗りつぶします。 ほとんどのカードの表示のメモリ アドレスのみで、四角形と色のディメンションが必要です。 一部のカードには、先頭および末尾の座標 X と Y 座標が必要です。 Windows がこれらの座標の最後の行を自動的に削除することに注意してください。 たとえば、640 する 0 から番号が、Windows は 640 の行を削除します。

一部のカードは、色の塗りつぶしと同じものを実現することができます、パターンの塗りつぶしを使用します。 ピクセル (パターン)、8 x 8 リージョンは、目的の色おり、そのパターンが指定された領域の塗りつぶしに使用します。 パターンは、必要なプロパティと同じ色で塗りつぶすに入力色と同じに設定されています。 パターン塗りはブレンドことが必要な命令の数を減らす 4 つの別の色を受け取ります。

 

 






---
title: 描画の直線と曲線
description: 描画の直線と曲線
ms.assetid: 0816fb69-7811-4319-b050-00ded21a10d4
keywords:
- WDK GDI の行
- GDI WDK Windows 2000 の表示、行
- グラフィックス ドライバー WDK Windows 2000 の表示、行
- WDK の GDI や線の描画
- GDI WDK Windows 2000 の表示、曲線
- グラフィックス ドライバー WDK Windows 2000 の表示、曲線
- WDK GDI、曲線の描画
- WDK GDI ブラシします。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 085512c36bfec63b9fa0eb16fab025108d42f1d6
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56556563"
---
# <a name="drawing-lines-and-curves"></a>描画の直線と曲線


## <span id="ddk_drawing_lines_and_curves_gg"></span><span id="DDK_DRAWING_LINES_AND_CURVES_GG"></span>


直線と曲線のグラフィック出力に含まれる型は[幾何学的行](geometric-wide-lines.md)、[表面的な行](cosmetic-lines.md)、および[ベジエ曲線](bezier-curves.md)します。

直線と曲線の出力のドライバーがサポートできる、 [ **DrvStrokePath**](https://msdn.microsoft.com/library/windows/hardware/ff556316)、 [ **DrvFillPath**](https://msdn.microsoft.com/library/windows/hardware/ff556220)、および[ **DrvStrokeAndFillPath** ](https://msdn.microsoft.com/library/windows/hardware/ff556311)関数。 ドライバーをサポートする必要があります**DrvStrokePath**デバイス管理が、画面の線を描画する場合は、ドライバーが曲線をサポートする必要はありません。

GDI は、行または任意の属性のセットで曲線を描画、GDI を呼び出して[ **DrvStrokePath**](https://msdn.microsoft.com/library/windows/hardware/ff556316)します。 少なくとも、 **DrvStrokePath**関数は、単色ブラシで solid とスタイルの表面的な線の描画と任意のクリッピングをサポートする必要があります。 GDI PATHOBJ\_*Xxx*と CLIPOBJ\_*Xxx*サービス機能これを可能に事前計算済みのクリッピングとワイドの行の 1 ピクセルのセットに行を分割します。 **DrvStrokePath** 、ポインターを提供**plineattrs**を[ **LINEATTRS** ](https://msdn.microsoft.com/library/windows/hardware/ff568195)さまざまな属性を定義する構造体。

ドライバーできますコールバック GDI を呼び出すことによって後回しパスまたはクリッピングが複雑すぎるため、ドライバーで、デバイスで処理するとき、 [ **EngStrokePath** ](https://msdn.microsoft.com/library/windows/hardware/ff565033)関数。 この場合、GDI を中断できます、 [ **DrvStrokePath** ](https://msdn.microsoft.com/library/windows/hardware/ff556316)呼び出しを一連の行 1 ピクセルに事前計算済みのクリッピングとなります。

呼び出して、CLIPOBJ\_*Xxx* GDI からサービス、ドライバーは GDI パス内のすべての行を列挙し、すべての行のクリッピング計算の実行を持つことができます。 ドライバーが、PATHOBJ を使用してさらに、\_*Xxx*、CLIPOBJ\_*Xxx*、または XFORMOBJ\_*Xxx*簡略化するサービス、グラフィックスの操作です。 たとえば、ドライバーを使用**CLIPOBJ\_cEnumStart**プリンター、まで、このリージョンを送信およびにクリップします。 ドライバーを使用できますも[ **PATHOBJ\_vEnumStart** ](https://msdn.microsoft.com/library/windows/hardware/ff568856)と[ **PATHOBJ\_bEnum** ](https://msdn.microsoft.com/library/windows/hardware/ff568851)行を列挙するために、またはパス内の曲線。 パスをデバイスに送信し、およびそのストロークを描画できます。

 

 






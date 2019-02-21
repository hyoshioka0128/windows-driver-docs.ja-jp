---
title: 表面的な行のスタイル
description: 表面的な行のスタイル
ms.assetid: 07e72190-7c8e-471e-9851-ccc037312c5c
keywords:
- WDK の GDI の行に表面的なスタイル
- GDI WDK Windows 2000 の表示、線は表面的なスタイル
- グラフィック ドライバー WDK Windows 2000 の表示、線、外観のスタイル
- 表面的な WDK GDI、線の描画スタイル
- WDK GDI の表面的な行のスタイル
- WDK の GDI の表面的な行のスタイル
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ff6006683ce59cfb0f38598a6fe3f0d9984fd20b
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56558896"
---
# <a name="styled-cosmetic-lines"></a>表面的な行のスタイル


## <span id="ddk_styled_cosmetic_lines_gg"></span><span id="DDK_STYLED_COSMETIC_LINES_GG"></span>


[ **DrvStrokePath** ](https://msdn.microsoft.com/library/windows/hardware/ff556316)関数は、単色のブラシを使用して任意のクリッピングと表面的な線の描画をサポートする必要があります。 ドライバーは、GDI サービスへの呼び出しを行うことができます[ **PATHOBJ\_vEnumStartClipLines** ](https://msdn.microsoft.com/library/windows/hardware/ff568857)領域 precompute にします。

表面的な行のスタイルは、繰り返し配列によって指定されているため、ジオメトリの太線に似ています。 表面的な行のスタイルを適用した場合は、配列エントリは、スタイルの手順で長さを含む LONG 値です。 によってスタイル手順とピクセルの間のリレーションシップが定義されている、 **xStyleStep**、 **yStyleStep**、および**denStyleStep**フィールド、 [ **GDIINFO** ](https://msdn.microsoft.com/library/windows/hardware/ff566484)によって返される構造体、 [ **DrvEnablePDEV** ](https://msdn.microsoft.com/library/windows/hardware/ff556211)関数。

ドライバーを呼び出すと[ **PATHOBJ\_bEnumClipLines**](https://msdn.microsoft.com/library/windows/hardware/ff568852)、複雑なクリッピングを表面的な行のスタイル処理するために、GDI の値を変更する、 [ **CLIPLINE** ](https://msdn.microsoft.com/library/windows/hardware/ff539416)構造体の**iStyleState**スタイルの状態を表すメンバー。 スタイルの状態が線のセグメントの最初のピクセルにオフセット行はクリップされませんがある場合に表示が最初のピクセルは、します。 スタイルの状態は、2 つの 16 ビット値がまとめられて ULONG 値で構成されます。 高値と安値の場合は、上位と下位 16 ビット スタイルの状態のスタイルの位置と呼ばれる、スタイルの状態の小数部のバージョンとして計算することができます。

`
    style position = HIGH + LOW/denStyleStep
`

たとえば場合、内の値**iStyleState**は 1 および 2、および**denStyleStep** 3 は、スタイルの位置が 5/3。 スタイルの描画のスタイルの配列の開始位置だけを判断するには、製品を実行します。

`
    style position * denStyleStep
`

この例での**denStyleStep**値最初の 5 つを除外する第 3 の描画位置が計算されます (5/3 \* 3) スタイルの配列 (ピクセル)。 つまり、このクリップされた行のスタイルの配列の 6 番目のピクセルの描画を開始します。

表面的な行の y スタイルと表面的な行の x スタイルがあります。 行は、dx y 方向の x 方向および dy 単位でのデバイス単位を拡張する場合、行が y スタイル、次の条件が true の場合。

`
    (dy * yStyleStep)  >=  (dx * xStyleStep)
`

によってスタイルの位置がここでは、高度な**yStyleStep**/**denStyleStep** y 方向の高度なピクセルごとにします。

逆に、行が x スタイルし、スタイルの位置が高度な**xStyleStep**/**denStyleStep**次が true の場合は、x 方向に高度なピクセルごとに。

`
    (dx * xStyleStep)  >  (dy * yStyleStep)
`

スタイルの位置は、新しい整数進めます、スタイルの手順はスタイルの配列で 1 つの単位を進めます。

次の図は、さまざまな傾斜を持つ複数の表面的なスタイル設定された行を示します。

![表面的な行のスタイルを示す図](images/102-02.png)

この図では、表示されるピクセル グリッドは、正方形ではありませんが、する 4 つのピクセルの x 方向の y 方向の 3 つのピクセルと同じ距離を表す、EGA ディスプレイのあるように表示されます。 手順をスタイル、 [ **GDIINFO** ](https://msdn.microsoft.com/library/windows/hardware/ff566484)構造体は、ディスプレイのピクセルは正方形で任意の傾きで同じスタイル設定された行が表示されることを確認します。 この図では、スタイルの配列で (によって定義された、 **pstyle**のメンバー、 [ **LINEATTRS** ](https://msdn.microsoft.com/library/windows/hardware/ff568195)構造) は{1,1}を破損した行が同じサイズにはドットとの矛盾点です。 ドライバーの値の**xStyleStep**が 3、 **yStyleStep**は 4、および**denStyleStep** 12。

さらに示すために、ドット マトリックス プリンターが 144 dpi の水平方向の解像度と、72 dpi 垂直方向の解像度とします。 さらに、最小のドットのドットの長さは 1/24 インチとします。 このプリンターをサポートするには、最小の番号を選択します**xStyleStep**と**yStyleStep** 1 などのプリンターの縦横比を補うことができます**xStyleStep**と。2 (144/72 インチ) の**yStyleStep**から 6 (144/24) の**denStyleStep**します。

場合、LA\_のフラグで代替のビットが設定されて、 [ **LINEATTRS** ](https://msdn.microsoft.com/library/windows/hardware/ff568195)表面的な行の構造、特殊なスタイルを使用します。 ここでは、他のすべてのピクセルは方向や縦横比に関係なく、です。 スタイルの配列の場合と、スタイルの状態が返される{1,1}と**xStyleStep**、 **yStyleStep**、および**denStyleStep**はすべて 1 つ。 つまり場合、 **lStyleState** 0 の場合は、上の最初のピクセルが場合**lStyleState**は 1 つは、最初のピクセルはオフです。

場合、LA\_STARTGAP ビットが LINEATTRS フラグの設定、スタイルの配列内の要素の意味を反転します。 2 番目のエントリなど、最初のダッシュの長さを指定する、配列の最初のエントリが最初の空白の長さを指定します。

 

 






---
title: ユーザー定義の用紙サイズをサポートする
description: ユーザー定義の用紙サイズをサポートする
ms.assetid: f9c0b759-687e-4d92-80ce-330e30cbc41c
keywords:
- ユーザー定義用紙サイズを WDK Unidrv
- WDK Unidrv のカスタマイズされた用紙サイズします。
- 最大の用紙サイズ WDK Unidrv
- WDK の余白の用紙サイズ
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1dfbd1d19ac42c46391f0a36aadb5a2bd93fd0ac
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63365328"
---
# <a name="supporting-user-defined-paper-sizes"></a>ユーザー定義の用紙サイズをサポートする





ユーザー定義用紙サイズは 1 つのプリント サーバーを特定できるし、特定のアプリケーション用にカスタマイズされた通常。 そのためのカスタマイズされた用紙サイズに、呼び出されます多くの場合。 システム管理者は、印刷のフォルダーを使用して、カスタマイズされた用紙サイズを定義します。 プリンターには、カスタマイズされた用紙サイズが処理される場合、ベンダーは、サイズの許容範囲を指定するプリンターの GPD ファイルを使用する必要があります。

カスタマイズされた用紙のサイズが許容範囲を記述するは、2 つの方法が用意されています。

-   サイズの範囲を明示的に指定することができます。

-   プリンターの最大の用紙サイズを基準とサイズの範囲を指定することができます。

### <a name="specifying-paper-size-ranges-explicitly"></a>用紙サイズの範囲を明示的に指定します。

このメソッドを使用して、GPD ファイルの用紙サイズの機能を含める必要があります、 \*CUSTOMSIZE 引数を持つエントリをオプションします。 このエントリは、次のオプション属性を含める必要があります。

\*MinSize \*MaxSize \*MaxPrintableWidth \*MinLeftMargin \*TopMargin \*BottomMargin \*CenterPrintable でしょうか。
\*CursorOrigin \*GPD エントリを使用コマンドするには、次の特性を持つプリンターに対してのみカスタム用紙サイズの説明を作成します。

-   プリンターでは、コマンドを明示的にカスタマイズされた用紙サイズを選択します (通常はカーソルの原点を移動する) をサポートしています。

-   カーソルの配信元は固定、用紙のすべてのカスタマイズされた用紙サイズの左上隅に対して相対的です。 (これは通常ありません横向きモードの印刷、または center フィードや右 hand-給紙されるプリンターの場合は true。)

-   上部と下部の余白、用紙サイズに依存しません。

-   用紙の幅が指定した値の合計より小さい場合\* **MinLeftMargin**と\* **MaxPrintableWidth**、右側の余白はありません。 これは、プリンターが印刷できる用紙の右端。

コマンドのパラメーター (で指定されている\***コマンド**エントリ) 場合、印刷時に計算できます[標準変数式](standard-variable-expressions.md)が使用すると、通常、PhysPaperLength を含むとPhysPaperWidth 変数。 これらの変数は、アプリケーションで指定したとおり、印刷ジョブに対して要求された実際の用紙サイズを表します。

### <a name="specifying-paper-size-ranges-relative-to-the-printers-largest-paper-size"></a>プリンターの最大サイズを基準に用紙サイズの範囲を指定します。

カスタマイズされた用紙サイズの範囲を明示的に指定するために必要な特性をサポートしていないプリンター、別の方法が提供、プリンターの最大の用紙サイズを基準と用紙のサイズを指定するされます。

このメソッドを使用して、GPD ファイルの用紙サイズの機能を含める必要があります、 \*CUSTOMSIZE 引数を持つエントリをオプションします。 このエントリは、次のオプション属性を含める必要があります。

\*MinSize \*MaxSize \*MaxPrintableWidth \*CustCursorOriginX \*CustCursorOriginX \*CustPrintableOriginX \*CustPrintableOriginY \*CustPrintableSizeX \*CustPrintableSizeY\*コマンド、プリンターの最大の用紙サイズを基準としたサイズの範囲を指定する場合は、次の配置ルールを使用します。

-   左側のフィードのプリンターのすべての用紙サイズ上および左の余白をアラインする必要があります。

-   右フィードのプリンターのすべての用紙サイズ上および右の余白を固定する必要があります。

-   センター フィードのプリンターの上余白および用紙サイズのすべての最上位の中心点をアラインする必要があります。

次の手順が含まれます。

1.  プリンターの最大サイズは、次の情報を確認します。
    -   最大の用紙サイズを選択するために必要なコマンドです。
    -   最大の用紙サイズに使用される値\*PageDimensions、 \*CursorOrigin、 \*PrintableOrigin、および\*PrintableArea GPD エントリ、GPD ファイルに含まれる予定があるかのようです。 ただし、いない実際に配置するこれらのエントリ ファイル。

2.  指定またはプリンターの最大の用紙サイズを基準と、カスタマイズされた用紙のサイズごとに、次の情報を計算する数式を作成します。
    -   配信元と各紙の印刷可能領域のサイズ。
    -   各用紙のカーソルの原点。

手順 2 の数式である必要があります[CUSTOMSIZE パラメーター式](option-attributes-for-the-papersize-feature.md#ddk-customsize-parameter-expressions-gg)、次の GPD エントリの値として指定されます。

\*CustCursorOriginX \*CustCursorOriginX \*CustPrintableOriginX \*CustPrintableOriginY \*CustPrintableSizeX \*CustPrintableSizeY、CUSTOMSIZE オプションには、おく必要があります。\*プリンターの最大サイズを選択するコマンドを指定するコマンドの入力。 このコマンドは、場所、プリンター用紙に印刷、実際、任意のサイズのすべてのカスタム用紙サイズ、および印刷可能領域と配信元のコントロールをカーソルに指定された式に送信されます。

### <a name="sample-calculations"></a>計算のサンプル

単純な例として、プリンターには、最大の用紙サイズの余白として同じサイズの余白を取得するカスタマイズされた用紙サイズがサポートされていると仮定します。 必要な手順は次のとおりです。

最大の用紙サイズの値を決定\* **PageDimensions**、 \* **CursorOrigin**、 \* **PrintableOrigin**と\* **PrintableArea**エントリ。 (に配置しないこれらのエントリ GPD ファイルです。)

Pseudoexpressions を次に示すように、これらの値の観点から最大の用紙サイズの余白のそれぞれの幅を決定します。

LeftMarginWidth =\***PrintableOrigin**.x

RightMarginWidth =\***PageDimensions**.x -\***PrintableArea**.x LeftMarginWidthTopMarginWidth =\***PrintableOrigin**例えば BottomMarginWidth =\***PageDimensions**例えば -\***PrintableArea**例えば-**TopMarginWidth**

これらの pseudoexpressions .x と例えば表しますの各エントリの水平および垂直方向コンポーネント[ペア](pairs.md)値。 ランドス ケープの印刷用のランドス ケープの値を使用して、 \* **PrintableArea**と\* **PrintableOrigin**します。

Pseudoexpressions を指定または非標準の用紙に印刷可能領域の計算を作成します。

\*CustPrintableOriginX: %d {LeftMarginWidth}

\*CustPrintableOriginY: %d {TopMarginWidth}

\*CustPrintableSizeX: %d {PhysPaperWidth LeftMarginWidth RightMarginWidth}

\*CustPrintableSizeY: %d {PhysPaperLength TopMarginWidth BottomMarginWidth}

PhysPaperWidth と PhysPaperLength の 2 つの標準的な変数の使用に注意してください。 実行時に、これらの変数には、長さと、アプリケーションによって要求された実際の用紙サイズの幅が含まれます。

これらの pseudoexpressions が有効である、ホワイト ペーパーは、左が取り込まれる、右が取り込まれる、または center が取り込まれるかどうかに注意してください。

GPD エントリを作成するこれらの式に、手順 1. で特定の実際の値を挿入します。 例は次のようになります。
```cpp
*CustPrintableOriginX:  %d{300}
*CustPrintableOriginY:  %d{300}
*CustPrintableSizeX:   %d{PhysPaperWidth-600}
*CustPrintableSizeY:  %d{PhysPaperLength-600}
```

カーソルの配信元のインデックスを計算する pseudoexpressions を作成します。 次の pseudoexpressions で\*CursorOrigin.x と\*CursorOrigin.y の水平および垂直方向のコンポーネントのプレース ホルダーは、[ペア](pairs.md)用紙サイズの最大のカーソルの配信元の値。

左側が取り込まれるプリンター。

\*CustCursorOriginX: %d {\*CursorOrigin.x} \*CustCursorOriginY: %d {\*CursorOrigin.y} の右側が取り込まれるプリンター。

\*CustCursorOriginX: %d {\*CursorOrigin.x+PhysPaperWidth -\*PageDimensions.x} \*CustCursorOriginY: %d {\*CursorOrigin.y} center 給紙プリンター。

\*CustCursorOriginX: %d {\*CursorOrigin.x+(PhysPaperWidth-PageDimensions.x)/2} \*CustCursorOriginY: %d {\*CursorOrigin.y} GPD エントリを作成するこれらの式に、手順 1. で特定の実際の値を挿入. (Center 送り用紙) の例があります。
```cpp
*CustCursorOriginX:  %d{((PhysPaperWidth-14040)/2)+300}
*CustCursorOriginY:   %d{180}
```

残りの 3 つ GPD エントリ - の値を指定\*MinSize、 \*MaxSize、および\*MaxPrintableWidth します。 指定された値\*MaxPrintableWidth は、実際には、このメソッドは使用されませんが、その値を 1 に設定できるように、パーサーは、エントリが存在する必要があります。

### <a name="a-real-example"></a>実際の例

次の例の GPD ファイル セグメントには、center 給紙プリンターの使用可能なカスタマイズされた用紙サイズがについて説明します。 縦モードの場合は、すべてのカスタム用紙サイズのすべての余白は、サイズの 300 マスター単位 (1/4 インチ) です。 横モードの場合、上下の余白は左の中にマスター 240 の単位と左右の余白が 200 のマスター ユニット。

```cpp
*Option: CUSTOMSIZE
{
  *rcNameID: =USER_DEFINED_SIZE_DISPLAY
  *MinSize: PAIR(4200,9000)
  *MaxSize: PAIR(14040, 21240)
  *MaxPrintableWidth: 14040
  *MinLeftMargin: 100
  *CenterPrintable?: FALSE
  *PageProtectMem: 1692
  *InsertBlock: =PaperConstraints
  *switch: Orientation
  {
    *case: PORTRAIT
    {
       *CustCursorOriginX:  %d{((PhysPaperWidth-14040)/2)+300}
       *CustCursorOriginY:   %d{180}
       *CustPrintableOriginX:  %d{300}
       *CustPrintableOriginY:  %d{300}
       *CustPrintableSizeX:   %d{PhysPaperWidth-600}
       *CustPrintableSizeY:  %d{PhysPaperLength-600}
       *Command: CmdSelect
       {
         *Order: DOC_SETUP.13
 *Cmd: "<1B>&l101a8c1e99F<1B>*p0x0Y<1B>*c0t8064x12528Y"
 }
    }
    *case: LANDSCAPE_CC90
    {
      *switch:  Option20
      {
      *% The 8100 rotates the landscape job 180 degrees if a stapler
      *% is attached, so the staple can be placed in the top left
      *% corner of the document. The printer always rotates the
      *% landscape job, even if stapling is not selected.
        *case: 3KStapler
        {
          *CustCursorOriginX:  %d{((PhysPaperWidth-14040)/2)+200}
          *CustCursorOriginY:   %d{PhysPaperLength}
          *CustPrintableOriginX:  %d{200}
          *CustPrintableOriginY:  %d{240}
          *CustPrintableSizeX:   %d{PhysPaperWidth-400}
          *CustPrintableSizeY:  %d{PhysPaperLength-480}
          *Command: CmdSelect
          {
            *Order: DOC_SETUP.13
            *Cmd: "<1B>&l101a8c1e63F<1B>*p0x0Y<1B>*c0t12456x8184Y"
          }
        }
        *case: MBM5S
        {
          *CustCursorOriginX:  %d{((PhysPaperWidth-14040)/2)+200}
          *CustCursorOriginY:   %d{PhysPaperLength}
          *CustPrintableOriginX:  %d{200}
          *CustPrintableOriginY:  %d{240}
          *CustPrintableSizeX:   %d{PhysPaperWidth-400}
          *CustPrintableSizeY:  %d{PhysPaperLength-480}
          *Command: CmdSelect
          {
            *Order: DOC_SETUP.13
            *Cmd: "<1B>&l101a8c1e63F<1B>*p0x0Y<1B>*c0t12456x8184Y"
          }
        }
        *default
        {
          *CustCursorOriginX:  %d{((PhysPaperWidth-14040)/2)+200}
          *CustCursorOriginY:   %d{21000}
          *CustPrintableOriginX:  %d{200}
          *CustPrintableOriginY:  %d{240}
          *CustPrintableSizeX:   %d{PhysPaperWidth-400}
          *CustPrintableSizeY:  %d{PhysPaperLength-480}
          *Command: CmdSelect
          {
            *Order: DOC_SETUP.13
 *Cmd: "<1B>&l101a8c1e63F<1B>*p0x0Y<1B>*c0t12456x8184Y"
 }
        }
      } *% switch Option20
    } *% case LANDSCAPE_CC90
  } *% switch Orientation
}
```

 

 





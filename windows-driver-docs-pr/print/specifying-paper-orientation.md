---
title: 用紙の向きの指定
description: 用紙の向きの指定
ms.assetid: 2d62e1ff-965b-4fd7-922c-319ec1bc39a5
keywords:
- Unidrv、用紙の向き
- 用紙の向き WDK Unidrv
- 縦向き WDK Unidrv
- LANDSCAPE_CC90 方向 WDK Unidrv
- LANDSCAPE_CC270 方向 WDK Unidrv
- 横モード WDK Unidrv
- 縦モード WDK Unidrv
- Unidrv WDK 印刷
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 37a3898d4ca7022c15765025dfcbf8bad60c1c60
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72840407"
---
# <a name="specifying-paper-orientation"></a>用紙の向きの指定





向きの[標準機能](standard-features.md)には、縦、横\_CC90、横\_CC270 の3つの[標準オプション](standard-options.md)が関連付けられています。 特に指定しない限り、既定の向きは [縦] です。 このオプションの使用は簡単です。このトピックでは説明しません。 このトピックのバランスは、2つの横向きオプションに関係しています。

### <a href="" id="landscape-cc90-and-landscape-cc270"></a>横\_CC90 と横向き\_CC270

横向き機能の横\_CC90 および横向き\_CC270 オプションは、縦モードのテキストおよびグラフィックスに適用される回転の量を示し、横モードに変換します。 横\_CC90 オプションは、テキストとグラフィックスを反時計回りに90°回転します。 横\_CC270 オプションは、テキストとグラフィックスを反時計回りに270°回転します。これは、時計回りに90度回転した場合と同じです。 どちらのオプションでも、Unidrv はテキストを回転し、指定された量をグラフィック表示し、新しい向きに合わせてそれらを移動するタスクを処理します。

多くのプリンターでは縦モードと横モードの両方がサポートされていますが、残りのプリンターでは、通常は縦モードのみがサポートされています。 各モードには独自の座標系があります。縦モードでは、原点が左上隅にあり (x が右に増加し、y が下方向に増加します)。横モードでは、原点は左下隅 (x 増加と y が右に増加) になります。

横モードをサポートしていないプリンターでも、この向きでドキュメントを印刷できます。 この種類のプリンターでは、プリンターの GPD ファイルの横\_CC270 オプションを指定する必要があります。 (これらのプリンターに対して [横\_CC90] オプションを指定した場合、テキストとグラフィックスは印刷時に正しく表示されません。)このオプションの下で、Unidrv は、プリンターの左上隅の原点を基準とした座標で、変換されたテキストとグラフィックスをプリンターに提示します。

横モードと縦モードをサポートするプリンターの場合は、GPD ファイルの横\_CC90 オプションを指定する必要があります。 このオプションでは、プリンターに対して横コマンド文字列を発行するように Unidrv を指定する必要があります。これにより、縦モードの座標系から横モード座標系 (左下隅の原点) に切り替わります。 Unidrv は、プリンターの左下隅の原点を基準として、変換されたテキストとグラフィックスをプリンターに提示します。

ただし、横モードをサポートするプリンター (ランドスケープ\_CC90 オプションが通常使用されます) は、横\_CC270 オプションを使用して操作できます。 このオプションの下で、Unidrv は、縦モードのみをサポートしているかのようにプリンターを処理するように指示されています (つまり、原点が左上隅にある、1つの座標系のみでサポートされています)。 そのため、Unidrv は、座標系を変更するコマンドを発行するように指示する必要がありません。 Unidrv は、変換されたテキストとグラフィックスを、この左上隅の原点を基準とした座標でプリンターに提示します。 Unidrv は元の場所を想定しているので、ユーザーがプリンターのプロパティページで横向きの向きを選択した場合でも、このようなプリンターは横モードのコマンド文字列を発行してはなりません。 次の GPD ファイルの例では、\*オプション: 横向き\_CC270 セクションに、プリンターを縦モードにするコマンドが含まれていることに注意してください (横\_縦向き\_CMD)、横モードに配置することはできません。

```cpp
*Feature: Orientation
{
  *rcNameID: =ORIENTATION_DISPLAY
  *DefaultOption: PORTRAIT
  *Option: PORTRAIT
  {
    *rcNameID: =PORTRAIT_DISPLAY
    *Command: CmdSelect
    {
      *Order: DOC_SETUP.60
      *Cmd: =ORIENT_PORTRAIT_CMD
    }
  }
  *Option: LANDSCAPE_CC270
   {
     *rcNameID: =LANDSCAPE_DISPLAY
     *Command: CmdSelect
     {
       *Order: DOC_SETUP.60
       *Cmd: =ORIENT_PORTRAIT_CMD
     }
  }
}
```

**注**   Windows 7 では、 **Mxdcgetpdevadjustment**関数に、横方向の回転用の新しいパラメーターがあります。 詳細については、「 [**MxdcXDCGetPDEVAdjustment**](https://docs.microsoft.com/windows-hardware/drivers/ddi/mxdc/nf-mxdc-mxdcgetpdevadjustment)」を参照してください。

 

 

 





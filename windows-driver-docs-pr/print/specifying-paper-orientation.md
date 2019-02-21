---
title: 用紙の向きを指定します。
description: 用紙の向きを指定します。
ms.assetid: 2d62e1ff-965b-4fd7-922c-319ec1bc39a5
keywords:
- Unidrv、用紙の向き
- 用紙の向き WDK Unidrv
- 縦向き WDK Unidrv
- LANDSCAPE_CC90 向き WDK Unidrv
- LANDSCAPE_CC270 向き WDK Unidrv
- 横モード WDK Unidrv
- 縦モード WDK Unidrv
- Unidrv WDK の印刷
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 428bfa4c9bd84cd2981e09362e813df5dbb78c99
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56551796"
---
# <a name="specifying-paper-orientation"></a>用紙の向きを指定します。





3 つ[標準オプション](standard-options.md)向きに関連付けられている[の標準機能](standard-features.md):PORTRAIT、LANDSCAPE\_CC90 とランドス ケープ\_CC270 します。 指定しない場合、既定の方向は縦にします。 このオプションの使用は簡単ですが、およびさらには説明しませんこのトピックの「します。 このトピックでの分散では、2 つの横のオプション。

### <a href="" id="landscape-cc90-and-landscape-cc270"></a>ランドス ケープ\_CC90 とランドス ケープ\_CC270

ランドス ケープ\_CC90 とランドス ケープ\_方向機能の CC270 オプションがテキストとグラフィックスで縦モードの横長表示モードに変換する場合に適用する回転の量を示します。 ランドス ケープ\_CC90 オプションが、反時計回りに 90 度のテキストとグラフィックスを回転します。 ランドス ケープ\_CC270 オプション テキストとグラフィックス 270 度回転反時計回りを時計回りに 90 度回転すると同じです。 どちらのオプションは、Unidrv はテキストとグラフィックス指定の量を回転して、新しい向きに応じて移動のタスクを処理します。

多くのプリンターでは、縦向きモードのみをサポートする機能を減らすには、通常、残りのプリンター縦モードと横モードの場合の両方をサポートします。 各モードが、独自の座標系: 縦モードでは、配信元 (右側の増加と y が増える下) x 左上隅には横モードでは、原点は、(x 上の増加と、右側に y 増加) 左上隅にあります。

横モードをサポートしていないプリンターはこの方向でドキュメントを印刷するかけられます。 この種類のプリンターでは、ランドス ケープを指定する必要があります\_プリンターの GPD ファイル CC270 オプション。 (ランドス ケープを指定する場合\_印刷されたときに、これらのプリンター、テキストおよびグラフィックス用 CC90 オプションが文字が正しく表示します)。このオプションは、Unidrv 原点プリンターの上限左座標を使用して、変換されたテキストとグラフィックスをプリンターに表示されます。

横モードと縦向きモードをサポートしているプリンター、ランドス ケープを指定する必要があります\_GPD ファイル CC90 オプション。 このオプションは、Unidrv 指定する必要がランドス ケープ コマンド文字列をプリンターを発行する縦モードの座標系から (左上隅にある origin) で横モードの座標システムへの切り替えにすることです。 Unidrv では、プリンターの下の左上の隅の原点の座標を使用して、変換されたテキストとグラフィックスをプリンターがし表示します。

ただし、サポートしているプリンターは横長表示モード (対象のランドス ケープ\_CC90 オプション通常使用される)、ランドス ケープで動作可能\_CC270 オプション。 縦モードのみがサポートされているかのように、プリンターを処理するこのオプションは、Unidrv が送られます (つまり、1 つの座標システムで、左上隅を原点と)。 その結果、Unidrv は座標系を変更するコマンドを発行する送信されませんする必要があります。 Unidrv では、この上限左端の原点の座標を使用して、変換されたテキストとグラフィックスをプリンターに表示します。 Unidrv には、この場所の原点の前提としています、ため、このようなプリンターする必要がありますは発行されません横モードのコマンド文字列では、ユーザーがプリンターのプロパティ ページの横の向きを選択した場合でも。 次の GPD ファイルの例でわかるように、\*オプション。ランドス ケープ\_CC270 セクションには、プリンターを縦向きモードに配置するためのコマンドが含まれています (回転\_縦\_CMD)、横モードに配置しない 1 つ。

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

**注**   For Windows 7、 **MxdcGetPDEVAdjustment**関数には、横置きに回転の新しいパラメーター。 詳細については、次を参照してください。 [ **MxdcXDCGetPDEVAdjustment**](https://msdn.microsoft.com/library/windows/hardware/ff557558)します。

 

 

 





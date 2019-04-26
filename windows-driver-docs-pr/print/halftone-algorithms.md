---
title: ハーフトーン アルゴリズム
description: ハーフトーン アルゴリズム
ms.assetid: 1831f952-4c83-4dfa-87e7-1c755f143227
keywords:
- HP-GL/2 モノクロ WDK Unidrv、ハーフトーン アルゴリズム
- PCL 5e WDK Unidrv、ハーフトーン アルゴリズム
- ハーフトーン WDK Unidrv
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 34703f5a3b5fc1bdbc8181c0c0ea413ede686d6b
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63341310"
---
# <a name="halftone-algorithms"></a>ハーフトーン アルゴリズム





一部のプリンターのベンダーは、テキスト、ベクトル オブジェクト、およびビットマップなどのオブジェクトのさまざまな種類の印刷中にさまざまなハーフトーン アルゴリズムを使用できます。 次の 3 つの例では、それぞれのオブジェクトの種類を印刷する GPD にどのような追加するかを表示します。

最初の例では、ハーフトーン印刷テキスト レンダリングを組み込む方法を示します。

```cpp
*Ifdef: WINNT_51
*Feature: TEXTHALFTONE
{
  *rcNameID: =TEXTHALFTONE_DISPLAY
  *DefaultOption: DETAIL
  *Option: DETAIL
   {
     *rcNameID: =DETAIL_HT_DISPLAY
     *Command: CmdSetTextHTAlgo { *Cmd : "<1B>*t0J" }
   }
  *Option: SMOOTH
   {
     *rcNameID: =SMOOTH_HT_DISPLAY
     *Name: "Smooth"
     *Command: CmdSetTextHTAlgo { *Cmd : "<1B>*t15J" }
   }
  *Option: BASIC
   {
     *rcNameID: =BASIC_HT_DISPLAY
     *Command: CmdSetTextHTAlgo { *Cmd : "<1B>*t18J" }
   }
}
*Endif:
```

2 番目の例には、ベクター グラフィックスの印刷中にハーフトーン レンダリング用のコマンドが含まれます。

```cpp
*Ifdef:  WINNT_51
*Feature: GRAPHICSHALFTONE
{
  *rcNameID: =GRAPHICSHALFTONE_DISPLAY
  *DefaultOption: SMOOTH
  *Option: DETAIL
   {
     *rcNameID: =DETAIL_HT_DISPLAY
     *Command: CmdSetGraphicsHTAlgo { *Cmd : "<1B>*t15J" }
   }
  *Option: SMOOTH
   {
     *rcNameID: =SMOOTH_HT_DISPLAY
     *Command: CmdSetGraphicsHTAlgo { *Cmd : "<1B>*t18J" }
   }
  *Option: BASIC
   {
     *rcNameID: =BASIC_HT_DISPLAY
     *Command: CmdSetGraphicsHTAlgo { *Cmd : "<1B>*t18J" }
   }
}
*Endif:
```

3 番目の例には、ハーフトーン印刷ビットマップ レンダリング用のコマンドが含まれます。

```cpp
*Ifdef: WINNT_51
*Feature: PHOTOHALFTONE
{
  *rcNameID: =PHOTOHALFTONE_DISPLAY
  *DefaultOption: SMOOTH
  *Option: DETAIL
   {
     *rcNameID: =DETAIL_HT_DISPLAY
     *Command: CmdSetPhotoHTAlgo { *Cmd : "<1B>*t15J" }
   }
  *Option: SMOOTH
   {
     *rcNameID: =SMOOTH_HT_DISPLAY
     *Command: CmdSetPhotoHTAlgo { *Cmd : "<1B>*t7J" }
   }
  *Option: BASIC
   {
     *rcNameID: =BASIC_HT_DISPLAY
     *Command: CmdSetPhotoHTAlgo { *Cmd : "<1B>*t3J" }
   }
}
*Endif:
```

 

 





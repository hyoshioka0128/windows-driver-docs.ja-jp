---
title: ミニドライバーで指定されるハーフトーン
description: ミニドライバーで指定されるハーフトーン
ms.assetid: 15af499a-c541-4d61-ace3-5a211574674c
keywords:
- ミニドライバーが指定したハーフトーン WDK Unidrv
- カスタマイズされたハーフトーン WDK Unidrv
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 280fd2a3e7e7440e9e4c86b9aec7ab05a3dd95ee
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67382047"
---
# <a name="minidriver-supplied-halftoning"></a>ミニドライバーで指定されるハーフトーン





かどうか、指定した色形式は 1 ピクセルあたりのビット数が、イメージの描画に使用されているいずれか (\*DrvBPP) が、プリンターでサポートされるピクセルあたりのビットを超える (\*DevBPP を乗算して\*DevNumOfPlanes)、その後カスタマイズされたハーフトーン機能を提供する必要があります。

カスタマイズされたハーフトーン機能を提供するには、次の操作を行う必要があります。

-   提供、[プラグインでレンダリング](rendering-plug-ins.md)を実装する、 [ **IPrintOemUni::ImageProcessing** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/prcomoem/nf-prcomoem-iprintoemuni-imageprocessing)メソッド。

-   ハーフトーンを含める\*GPD ファイルと、各機能のエントリは、ハーフトーン メソッドをカスタマイズ、インクルード、\*ハーフトーン メソッドを記述するオプションのエントリ。 (いずれにも使用しないでください、[ハーフトーン機能の属性をオプション](option-attributes-for-the-halftone-feature.md))。

-   含めるを返さ\*GPD ファイルのエントリに機能します。 色の書式設定オプションを指定された各にする必要があります、 \*IPCallbackID 属性の場合は、 **IPrintOemUni::ImageProcessing**その色形式のハーフトーン処理するメソッド。

次の例では、2 つの色形式と 4 つのハーフトーン メソッドを定義します。 この例では[制約オプション](option-constraints.md)ハーフトーン メソッド Unidrv は、ユーザーは、各色形式を選択を許可する必要がありますを指定します。

```cpp
*Feature: ColorMode
{
    *Option: ColorFormat1
    {
        *Name: "Color Format 1"
        *DevBPP: 1
        *DevNumofPlanes: 4
        *ColorPlaneOrder: LIST (CYAN, MAGENTA, YELLOW, BLACK)
        *DrvBPP: 4
        *Constraints: LIST (Halftone.CustomHalftoneMethod1,
+                           Halftone.CustomHalftoneMethod2)
    }
    *Option: ColorFormat2
    {
        *Name: "Color Format 2"
        *DevBPP: 24
        *DevNumofPlanes: 1
        *DrvBPP: 8
        *IPCallbackID: 100
        *Constraints: LIST (Halftone.StandardHalftoneMethod1,
+                           Halftone.StandardHalftoneMethod2)
    }
}
*Feature: Halftone
{
    *Option: StandardHalftoneMethod1
    {
        *Name: "Standard Halftone Method 1"
    }
    *Option: StandardHalftoneMethod2
    {
        *Name: "Standard Halftone Method 2"
    }
    *Option: CustomHalftoneMethod1
    {
        *Name: "Custom Halftone Method 1"
    }
    *Option: CustomHalftoneMethod2
    {
        *Name: "Custom Halftone Method 2"
    }
}
```

説明したように例では、ColorFormat1 と ColorFormat2 返さの両方のオプションが Unidrv を処理できる、色の形式を表す[色形式の処理](handling-color-formats.md)します。 ColorFormat2、用、 \* **IPCallbackID**属性が指定されています。 Unidrv にプリンターの呼び出し、プリンターのユーザーは、色の書式として ColorFormat2 を選択した場合[ **IPrintOemUni::ImageProcessing** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/prcomoem/nf-prcomoem-iprintoemuni-imageprocessing)ハーフトーン処理するために COM メソッド。 メソッドのパラメーターの 1 つは、現在選択されているハーフトーン メソッドを表す文字列名へのポインターです。

ハーフトーンの詳細については、次を参照してください。[カスタマイズ ハーフトーン](customized-halftoning.md)します。

 

 





---
title: ミニドライバーで指定されるハーフトーン
description: ミニドライバーで指定されるハーフトーン
ms.assetid: 15af499a-c541-4d61-ace3-5a211574674c
keywords:
- ミニドライバーが提供するハーフトーン WDK Unidrv
- カスタマイズされたハーフトーン WDK Unidrv
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1fc1828e70d99dba4bd7a077798e4963e32c7051
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72824267"
---
# <a name="minidriver-supplied-halftoning"></a>ミニドライバーで指定されるハーフトーン





指定された色の形式が、イメージのレンダリングに使用されるピクセルあたりのビット数 (\*DrvBPP) が、プリンターでサポートされているピクセルあたりのビット数 (\*DevBPP に \*DevNumOfPlanes を掛けた値) より大きい場合は、次のように指定する必要があります。カスタマイズされたハーフトーン機能。

カスタマイズされたハーフトーン機能を提供するには、次の操作を行う必要があります。

-   [**Iprintoemuni:: ImageProcessing**](https://docs.microsoft.com/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemuni-imageprocessing)メソッドを実装する[レンダリングプラグイン](rendering-plug-ins.md)を提供します。

-   GPD ファイルにハーフトーン\*機能のエントリを含め、カスタマイズされた各ハーフトーン方式には、ハーフトーン方式を説明する \*オプションのエントリを含めます。 ([ハーフトーン機能に](option-attributes-for-the-halftone-feature.md)は、いずれのオプション属性も使用しないでください)。

-   ColorMode \*機能のエントリを GPD ファイルに含めます。 指定された各色書式設定オプションについて、 **Iprintoemuni:: ImageProcessing**メソッドでその色の形式のハーフトーンを処理する場合は、\*IPCallbackID 属性を含める必要があります。

次の例では、2つのカラー形式と4つのハーフトーンメソッドを定義します。 この例では、[オプション制約](option-constraints.md)を使用して、どのハーフトーン方式を使用してユーザーが各カラー形式に対して選択できるようにするかを指定します。

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

この例では、ColorFormat1 オプションと ColorFormat2 ColorMode オプションの両方が、[色の書式の処理](handling-color-formats.md)に関する説明に従って、Unidrv が処理できるカラー形式を表しています。 ColorFormat2 では、\***Ip id**属性が指定されています。 プリンターユーザーがカラー形式として ColorFormat2 を選択した場合、Unidrv は、プリンターの[**Iprintoemuni:: ImageProcessing**](https://docs.microsoft.com/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemuni-imageprocessing) COM メソッドを呼び出して、ハーフトーンを処理します。 メソッドのパラメーターの1つは、現在選択されているハーフトーンメソッドを表す文字列名へのポインターです。

ハーフトーンの詳細については、「カスタマイズされた[ハーフトーン](customized-halftoning.md)」を参照してください。

 

 





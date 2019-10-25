---
title: 行パターン繰り返しの数の設定
description: 行パターン繰り返しの数の設定
ms.assetid: 090b823a-59d0-40e1-8feb-0b03b7f08fee
keywords:
- ラインパターンの繰り返し WDK Direct3D
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8baddb7079866688acfb3f8a7be1a8492bc9b7c4
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72825814"
---
# <a name="setting-the-number-of-line-pattern-repetitions"></a>行パターン繰り返しの数の設定


## <span id="ddk_setting_the_number_of_line_pattern_repetitions_gg"></span><span id="DDK_SETTING_THE_NUMBER_OF_LINE_PATTERN_REPETITIONS_GG"></span>


アプリケーションでは、ソリッドまたはパターン線を使用してプリミティブをレンダリングするように Direct3D デバイスに指示できます。 デバイスでパターンの繰り返しがサポートされている場合は、アプリケーションで特定の行パターンを拡張することもできます。 デバイスのドライバーは、デバイスが特定の行パターンの繰り返しをサポートしていることを示すために、D3DPMISCCAPS\_LINEPATTERN REP フラグを設定する必要があります。 このフラグがどのように設定されるかは、DirectX のバージョンによって異なります。

-   DirectX 7.0 以前の場合は、 [**D3DPRIMCAPS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dcaps/ns-d3dcaps-_d3dprimcaps)構造体の**Dw誤 ccaps**メンバーでこのフラグを設定します。

-   DirectX 8.0 以降では、D3DCAPS*xx*構造体の**PrimitiveMiscCaps**メンバーにこのフラグを設定します。ここで、 *Xx*は directx のバージョンを示します (たとえば、バージョン8の場合は D3DCAPS8、バージョン9の場合は D3DCAPS9)。 D3DCAPS8 と D3DCAPS9 については、それぞれのバージョンの DirectX SDK ドキュメントで説明されています。

アプリケーションで、D3DRENDERSTATE\_LINEPATTERN (または D3DRS\_LINEPATTERN) のレンダー状態のレンダー状態の値を設定するときに、の**Wrepeatfactor**メンバーを設定することによって、行パターンを繰り返す回数を指定できます。D3DLINEPATTERN 構造体。 アプリケーションでは、このメンバーに最大値 65535 (16 ビット値) を設定できます。 ただし、ハードウェアでサポートされるのは最大 255 (8 ビット値) のみです。 そのため、表示ドライバーは、無効な要求として、255より大きい値に対して、行パターンの繰り返し数を設定しようとする要求を失敗させる必要があります。 D3DLINEPATTERN については、DirectX SDK のドキュメントを参照してください。

 

 






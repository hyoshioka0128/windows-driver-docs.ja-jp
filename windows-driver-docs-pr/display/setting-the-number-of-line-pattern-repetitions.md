---
title: 行パターン繰り返しの数の設定
description: 行パターン繰り返しの数の設定
ms.assetid: 090b823a-59d0-40e1-8feb-0b03b7f08fee
keywords:
- 行パターンの繰り返し WDK Direct3D
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5e613c3ac27101017036c2842fbd42cff1d2c548
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67365551"
---
# <a name="setting-the-number-of-line-pattern-repetitions"></a>行パターン繰り返しの数の設定


## <span id="ddk_setting_the_number_of_line_pattern_repetitions_gg"></span><span id="DDK_SETTING_THE_NUMBER_OF_LINE_PATTERN_REPETITIONS_GG"></span>


アプリケーションは、solid またはパターンの行を使用するプリミティブを表示するために、Direct3D デバイスを直接送信できます。 アプリケーションは、デバイスは、繰り返しパターンをサポートしている場合、特定の行のパターンを拡張もできます。 デバイスのドライバーが、D3DPMISCCAPS を設定する必要があります\_LINEPATTERNREP デバイスが、パターンを特定の行を繰り返しをサポートしていることを示すフラグ。 このフラグを設定する方法は、DirectX のバージョンによって異なります。

-   DirectX 7.0 以降このフラグを設定、 **dwMiscCaps**のメンバー、 [ **D3DPRIMCAPS** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dcaps/ns-d3dcaps-_d3dprimcaps)構造体。

-   DirectX 8.0 以降では、このフラグを設定、 **PrimitiveMiscCaps** 、D3DCAPS のメンバー*Xx*構造、場所*Xx* DirectX のバージョン (たとえば、D3DCAPS8 を示しますバージョン 8 とバージョン 9 D3DCAPS9)。 DirectX SDK ドキュメントのそれぞれのバージョンでは、D3DCAPS8 と D3DCAPS9 が説明します。

アプリケーションが、D3DRENDERSTATE のレンダリング状態の値を設定すると\_LINEPATTERN (または D3DRS\_LINEPATTERN) の状態の表示を設定して行パターンを繰り返す回数を指定できます、 **wRepeatFactor** D3DLINEPATTERN 構造体のメンバー。 アプリケーションでは、65535 (16 ビット値) の最大値をこのメンバーを設定できます。 ただし、ハードウェアは、最大 255 (8 ビット値) のみをサポートします。 したがって、ディスプレイ ドライバーとして無効な要求に、値に行の繰り返しパターンの数を 255 より大きい設定しようとする要求を失敗する必要があります。 D3DLINEPATTERN は DirectX SDK のドキュメントについて説明します。

 

 






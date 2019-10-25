---
title: ガンマ変換と線形変換の形式のマークキング
description: ガンマ変換と線形変換の形式のマークキング
ms.assetid: 1285b04e-b67a-46d2-82b2-3cde433bf578
keywords:
- ガンマ補正 WDK DirectX 9.0、ガンマ変換のためのマーク付け形式
- 変換のための形式のマーク付け WDK DirectX 9.0
- 線形変換 WDK DirectX 9.0
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8d77fd3ff8003466cfaf8165b07694e14c305953
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72840574"
---
# <a name="marking-formats-for-gamma-and-linear-conversion"></a>ガンマ変換と線形変換の形式のマークキング


## <span id="ddk_marking_formats_for_gamma_and_linear_conversion_gg"></span><span id="DDK_MARKING_FORMATS_FOR_GAMMA_AND_LINEAR_CONVERSION_GG"></span>


DirectX 9.0 バージョンドライバーは、線形またはガンマ変換のテクスチャ形式をマークします。これにより、これらの形式のテクスチャを正確に処理またはレンダリングするために変換するかどうかを判断できます。

通常、テクスチャコンテンツは sRGB 形式で格納され、ガンマは修正されます。 ただし、ピクセルパイプラインで、sRGB 形式のテクスチャに対して正確なブレンド操作を実行するには、ドライバーから読み取る前に、これらのテクスチャを線形形式に変換する必要があります。 ピクセルパイプラインがレンダリングターゲットにテクスチャを書き込む準備ができたら、ドライバーはこれらのテクスチャを sRGB 形式に変換する必要があります。 このようにして、ピクセルパイプラインはすべての操作を線形空間で実行します。

ドライバーは、変換用の形式をマークするために、 [**ddの Ddピクセル形式**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-_ddpixelformat)構造の**dwoperations**メンバーで、次のフラグを指定します。

-   D3DFORMAT\_OP\_SRGBREAD を使用して、テクスチャがガンマ 2.2 (sRGB または not) であるかどうかを示します。また、参照時のブレンド操作またはサンプラーのためにドライバーによって線形形式に変換される必要があるかどうかを示します。

-   D3DFORMAT\_OP\_SRGBWRITE は、レンダーターゲットへの書き込み時にピクセルパイプラインが sRGB 領域に正確に戻す必要があるかどうかを示します。

 

 






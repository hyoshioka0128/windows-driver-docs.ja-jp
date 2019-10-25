---
title: グラフィックス DDI の使用
description: グラフィックス DDI の使用
ms.assetid: e48d117b-8c1c-4617-84f8-b0b489b1083a
keywords:
- WDK GDI、DDI の描画
- GDI WDK Windows 2000 display、DDI
- グラフィックスドライバー WDK Windows 2000 display、DDI
- DDI WDK グラフィックス
- GDI WDK Windows 2000 display、functions
- グラフィックスドライバー WDK Windows 2000 display、functions
- functions WDK グラフィックス
- WDK GDI、functions の描画
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c025e698b78d7e6c4d854d99121654ed3e3dc237
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72825390"
---
# <a name="using-the-graphics-ddi"></a>グラフィックス DDI の使用


## <span id="ddk_using_the_graphics_ddi_gg"></span><span id="DDK_USING_THE_GRAPHICS_DDI_GG"></span>


グラフィックスデバイスインターフェイス (GDI) を介してルーティングされるデバイスに依存しないアプリケーション呼び出しに応答して、グラフィックスドライバーは、グラフィックスデバイスが必要な出力を生成することを確認する必要があります。 グラフィックスドライバーは、必要なだけのグラフィックスデバイスドライバーインターフェイス (DDI) を実装することによって、グラフィックス出力を制御します。

グラフィック DDI 関数の名前は、 *DrvXxx*の形式になっています。 GDI は、これらの*DrvXxx*関数を呼び出して、データをドライバーに渡します。 アプリケーションが GDI の要求を行うと、そのドライバーが関連する機能をサポートしていることが GDI によって判断されます。 関数を提供し、関数の完了時に GDI に戻るのは、ドライバーの役割です。

ここでは、表示のライターとプリンタードライバーが認識する必要があるグラフィックス DDI 関数について説明します。 グラフィックス DDI 関数の宣言、構造体の定義、および定数は、 *winddi*にあります。 グラフィックス DDI 関数の詳細については、「[プリンターとディスプレイドライバーによって実装される GDI 関数](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)」を参照してください。

このセクションに含まれるトピックは次のとおりです。

[グラフィックスドライバーの機能](graphics-driver-functions.md)

[初期化関数と終了関数のサポート](supporting-initialization-and-termination-functions.md)

[グラフィックスドライバー関数における浮動小数点演算](floating-point-operations-in-graphics-driver-functions.md)

[デバイスに依存するビットマップの作成](creating-device-dependent-bitmaps.md)

[グラフィックス出力のサポート](supporting-graphics-output.md)

[グラフィックス DDI の色およびパターン関数のサポート](supporting-graphics-ddi-color-and-pattern-functions.md)

[グラフィックス DDI のフォントおよびテキスト関数のサポート](supporting-graphics-ddi-font-and-text-functions.md)

[DEVMODEW 構造体](the-devmodew-structure.md)

 

 






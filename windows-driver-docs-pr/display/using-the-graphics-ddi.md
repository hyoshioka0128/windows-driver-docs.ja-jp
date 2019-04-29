---
title: グラフィックス DDI の使用
description: グラフィックス DDI の使用
ms.assetid: e48d117b-8c1c-4617-84f8-b0b489b1083a
keywords:
- WDK の GDI 描画 DDI
- GDI WDK Windows 2000 の表示、DDI
- グラフィックス ドライバー WDK Windows 2000 の表示、DDI
- DDI WDK グラフィック
- GDI WDK Windows 2000 の表示、関数
- グラフィックス ドライバー WDK Windows 2000 の表示、関数
- WDK グラフィックス関数
- 描画 WDK GDI や関数
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f7c1c3ea3fc87aa17227417af5ae5349a3485d1c
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63388983"
---
# <a name="using-the-graphics-ddi"></a>グラフィックス DDI の使用


## <span id="ddk_using_the_graphics_ddi_gg"></span><span id="DDK_USING_THE_GRAPHICS_DDI_GG"></span>


グラフィックス デバイス インターフェイス (GDI) 経由のルーティング デバイスに依存しないアプリケーションの呼び出しに応答して、グラフィックス ドライバーはする必要があります、グラフィックス デバイスが必要な出力を生成することを確認します。 グラフィック ドライバーは、グラフィックス デバイス ドライバー インターフェイス (DDI) は、必要な限り実装することによってグラフィックスの出力を制御します。

グラフィックス DDI 関数名は、 *DrvXxx*フォーム。 GDI を呼び出す*DrvXxx*ドライバーにデータを渡す関数。 ときに、アプリケーションには、GDI および GDI の要求には、ドライバーは、関連する関数をサポートしています、GDI がその関数を呼び出すことが決定します。 関数を提供し、関数の完了時に、GDI に戻り、ドライバーの役目です。

このセクションでは、グラフィックス ディスプレイおよびプリンター ドライバーのライターが認識する必要がある DDI 関数について説明します。 グラフィックス DDI 関数に対する宣言、構造体の定義、および定数が記載*winddi.h*します。 グラフィックス DDI 関数の詳細については、次を参照してください。 [GDI 関数は、プリンターやディスプレイ ドライバーによって実装される](https://msdn.microsoft.com/library/windows/hardware/ff566549)します。

このセクションのトピックは次のとおりです。

[グラフィックス ドライバー関数](graphics-driver-functions.md)

[初期化と終了関数をサポートしています。](supporting-initialization-and-termination-functions.md)

[浮動小数点演算でグラフィックス ドライバー関数](floating-point-operations-in-graphics-driver-functions.md)

[デバイス依存ビットマップを作成します。](creating-device-dependent-bitmaps.md)

[グラフィックスの出力をサポートしています。](supporting-graphics-output.md)

[グラフィックス DDI 色およびパターンの機能をサポート](supporting-graphics-ddi-color-and-pattern-functions.md)

[グラフィックス DDI フォントおよびテキストの機能をサポート](supporting-graphics-ddi-font-and-text-functions.md)

[DEVMODEW 構造体](the-devmodew-structure.md)

 

 






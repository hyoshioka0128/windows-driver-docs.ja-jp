---
title: GDI サポートサービス
description: GDI サポートサービス
ms.assetid: a5521f9f-ddf6-4892-bf6d-aebb7936df11
keywords:
- GDI WDK Windows 2000 display、service ルーチン
- グラフィックスドライバー WDK Windows 2000 display、service ルーチン
- WDK GDI、サービスルーチンの描画
- サービスルーチン WDK GDI
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1a78c6bccb13496fde5af186a9772d977246ff90
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72839678"
---
# <a name="gdi-support-services"></a>GDI サポートサービス


## <span id="ddk_gdi_support_services_gg"></span><span id="DDK_GDI_SUPPORT_SERVICES_GG"></span>


*GDI*は、ドライバーの設計を簡素化する多くのサービスルーチンをエクスポートします。 ドライバーは、これらのルーチンを直接呼び出すことができます。 名前が**Eng**で始まる一般的なグラフィックスエンジンサービスであるルーチンの名前。 特定のオブジェクトに関連するサービスルーチンは、常にオブジェクトの名前で始まります。たとえば、 [**CLIPOBJ\_cEnumStart**](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-clipobj_cenumstart)は[**CLIPOBJ**](https://docs.microsoft.com/windows/desktop/api/winddi/ns-winddi-_clipobj)サービスです。

1番目の引数がユーザーオブジェクトへのポインターであるサービスルーチンは、そのユーザーオブジェクトのメソッドであり、通常C++の規則を使用して呼び出される   ます。 そのため、でC++記述されたドライバーは、メソッドとしてサービスルーチンにアクセスできます。

 

これらのサービスルーチンは、次のカテゴリに分類されます。

[Surface management](gdi-support-for-surfaces.md)

[パレットサービス](gdi-support-for-palettes.md)

[パスサービス](gdi-services-for-paths.md)

[ウィンドウサービス](gdi-support-for-window-objects.md)

[レンダリングサービス](gdi-drawing-and-related-services.md)

[フォントとテキストサービス](gdi-font-and-text-services.md)

[メモリサービス](gdi-memory-services.md)

[イベントサービス](gdi-event-services.md)

[ファイル、モジュール、およびプロセスサービス](gdi-file--module--and-process-services.md)

[セマフォサービス](gdi-semaphore-services.md)

[プリンターサービス](gdi-printer-services.md)

[ドライバー関連のサービス](gdi-driver-related-services.md)

[インフォメーションサービス](gdi-information-services.md)

[ユーティリティサービス](gdi-utility-services.md)

[浮動小数点サービス](gdi-floating-point-services.md)

[ハーフトーンサービス](gdi-halftone-services.md)

グラフィックス[Ddi を使用](using-the-graphics-ddi.md)すると、グラフィックス ddi のエントリポイントについて説明します。また、これらのサービスルーチンの多くを使用して、ドライバーがエントリポイントを実装できるようにする方法についても説明します。 各サービス関数の詳細な説明については、「[プリンターとディスプレイドライバーによって呼び出される GDI 関数](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)」を参照してください。

 

 






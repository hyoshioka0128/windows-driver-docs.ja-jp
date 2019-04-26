---
title: GDI サポート サービス
description: GDI サポート サービス
ms.assetid: a5521f9f-ddf6-4892-bf6d-aebb7936df11
keywords:
- GDI WDK Windows 2000 の表示、サービス ルーチン
- グラフィックス ドライバー WDK Windows 2000 の表示、サービス ルーチン
- 描画 WDK GDI やサービス ルーチン
- サービス ルーチン WDK GDI
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ca220ac893d235b99633179f7c4618a3ca9712bf
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63357900"
---
# <a name="gdi-support-services"></a>GDI サポート サービス


## <span id="ddk_gdi_support_services_gg"></span><span id="DDK_GDI_SUPPORT_SERVICES_GG"></span>


*GDI*ドライバーの設計を簡略化できる多くのサービス ルーチンをエクスポートします。 ドライバーは、これらのルーチンを直接呼び出すことができます。 一般的なグラフィックスのルーチンの名前エンジン サービスの名前が始まる**への Eng**します。 オブジェクトの名前を持つ常に、特定のオブジェクトに関連するサービス ルーチンを開始します。たとえば、 [ **CLIPOBJ\_cEnumStart** ](https://msdn.microsoft.com/library/windows/hardware/ff539421)は、 [ **CLIPOBJ** ](https://msdn.microsoft.com/library/windows/hardware/ff539417)サービス。

**注**  を最初の引数は、ユーザー オブジェクトへのポインター サービス ルーチンは、そのユーザー オブジェクトのメソッドし、通常の C++ 規則を使用すると呼ばれます。 そのため、C++ で記述されたドライバーの方法としてサービス ルーチンにアクセスできます。

 

これらのサービス ルーチンは、次のカテゴリに分類されます。

[サーフェスの管理](gdi-support-for-surfaces.md)

[パレット サービス](gdi-support-for-palettes.md)

[パス サービス](gdi-services-for-paths.md)

[ウィンドウ サービス](gdi-support-for-window-objects.md)

[サービスの表示](gdi-drawing-and-related-services.md)

[フォントとテキスト サービス](gdi-font-and-text-services.md)

[メモリのサービス](gdi-memory-services.md)

[イベント サービス](gdi-event-services.md)

[ファイル、モジュール、および処理サービス](gdi-file--module--and-process-services.md)

[セマフォのサービス](gdi-semaphore-services.md)

[プリンターのサービス](gdi-printer-services.md)

[ドライバー関連のサービス](gdi-driver-related-services.md)

[インフォメーション サービス](gdi-information-services.md)

[ユーティリティ サービス](gdi-utility-services.md)

[浮動小数点のサービス](gdi-floating-point-services.md)

[ハーフトーン サービス](gdi-halftone-services.md)

[グラフィックス DDI を使用して](using-the-graphics-ddi.md)グラフィックス DDI のエントリ ポイントを説明し、これらのサービス ルーチンの多くを使用して、ドライバーのエントリ ポイントを実装する場所についても説明します。 各サービスの機能の詳細な説明については、次を参照してください。 [GDI 関数は、プリンターおよびディスプレイ ドライバーによって呼び出されます](https://msdn.microsoft.com/library/windows/hardware/ff566544)します。

 

 






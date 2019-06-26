---
title: グラフィックス ドライバー関数
description: グラフィックス ドライバー関数
ms.assetid: 2e8725a1-2d98-472d-b8ec-8f451272fe77
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c5cbce883565fa91a1dab5d41ca8e4f1240b15a7
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67379936"
---
# <a name="graphics-driver-functions"></a>グラフィックス ドライバー関数


## <span id="ddk_graphics_driver_functions_gg"></span><span id="DDK_GRAPHICS_DRIVER_FUNCTIONS_GG"></span>


以下のトピックでは、分類に必要な特定の状況で必須およびオプションとして、driver エントリ ポイント関数について説明します。

[必要なグラフィック ドライバー関数](required-graphics-driver-functions.md)

[条件付きで必須のグラフィックス ドライバー関数](conditionally-required-graphics-driver-functions.md)

[省略可能なグラフィックス ドライバー関数](optional-graphics-driver-functions.md)

GDI を呼び出すことがデバイス ドライバーがエラーを返したときに通常必要があります[ **EngSetLastError** ](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-engsetlasterror)拡張エラー コードをレポートする関数。 アプリケーション プログラムは、エラー コードを取得できます。

 

 






---
title: ディスプレイ ドライバーのグラフィックス DDI 関数
description: ディスプレイ ドライバーのグラフィックス DDI 関数
ms.assetid: 9edd06bd-7aac-4015-864d-b08f3e3a79fd
keywords:
- ディスプレイ ドライバー WDK Windows 2000 では、グラフィック
- グラフィックス DDI 関数 WDK Windows 2000 を表示します。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a70805ffca90452973707c91398aad21403694c6
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63374604"
---
# <a name="graphics-ddi-functions-for-display-drivers"></a>ディスプレイ ドライバーのグラフィックス DDI 関数


## <span id="ddk_graphics_ddi_functions_for_display_drivers_gg"></span><span id="DDK_GRAPHICS_DDI_FUNCTIONS_FOR_DISPLAY_DRIVERS_GG"></span>


Microsoft オペレーティング システムの NT ベースのディスプレイ ドライバーは、複数のグラフィックス DDI 関数を実装する必要があります。 小さくなりより簡単に記述は GDI の既存の機能を活用するドライバーを記述するには、ドライバーは、GDI よりも効率的に実行できる操作も実装を確認する必要があります。

ディスプレイ ドライバー グラフィックス DDI 関数は、次のトピックで説明はそれぞれ、3 つのグループに分類されます。

1.  [すべてのディスプレイ ドライバーによって必要なグラフィックス DDI 関数](required-display-driver-functions.md)します。

2.  [特定の条件下で必要なグラフィックス DDI 関数](conditionally-required-display-driver-functions.md)します。

3.  [省略可能なグラフィックス DDI 関数](optional-display-driver-functions.md)します。

 

 






---
title: 初期化と終了関数をサポートしています。
description: 初期化と終了関数をサポートしています。
ms.assetid: 306be966-be23-4680-aeda-32e9cb1ac4a9
keywords:
- 描画の WDK GDI, 初期化
- 描画の WDK GDI の初期化について
- 初期化のグラフィック ドライバー WDK Windows 2000 を表示します。
- 初期化のグラフィック ドライバー WDK Windows 2000 表示について
- GDI WDK Windows 2000 の表示、初期化
- GDI WDK Windows 2000 の表示の初期化について
- グラフィックス ドライバー WDK Windows 2000 の表示, 初期化
- グラフィックス ドライバー WDK Windows 2000 の表示の初期化について
- GDI WDK Windows 2000 の表示、終了
- グラフィックス ドライバー WDK Windows 2000 の表示、終了
- 描画 WDK GDI や終了
- グラフィック ドライバー WDK GDI を終了しています
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c2e83a50a9f43bbd8ff8c659cbe3d7cbaa32dc8f
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56557663"
---
# <a name="supporting-initialization-and-termination-functions"></a>初期化と終了関数をサポートしています。


## <span id="ddk_supporting_initialization_and_termination_functions_gg"></span><span id="DDK_SUPPORTING_INITIALIZATION_AND_TERMINATION_FUNCTIONS_GG"></span>


グラフィック ドライバーは、複数のデバイスと各デバイスには、同時に複数の使用をサポートできます。 そのため、3 つの異なる層での初期化と終了が発生する各層持つ独自のタイミングです。 次の順序で初期化が行われます。

1.  [ドライバーの初期化](driver-initialization-and-cleanup.md)

2.  [PDEV 初期化](pdev-initialization-and-cleanup.md)

3.  [画面の初期化](enabling-and-disabling-the-surface.md)

終了は、逆の順序で発生します。

 

 






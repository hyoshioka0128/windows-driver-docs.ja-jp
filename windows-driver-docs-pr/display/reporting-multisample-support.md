---
title: マルチサンプル サポートのレポート
description: マルチサンプル サポートのレポート
ms.assetid: 05db3a79-08b3-4476-a016-d9a9bfa48504
keywords:
- DirectX 8.0 リリース ノート Windows 2000 の WDK 表示、マルチ サンプリングの表示、レポート作成
- マルチ サンプリング レンダリング WDK DirectX 8.0 では、レポート作成
- WDK DirectX multisamples 8.0 では、レポートのレンダリング
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: cdcb35249b53f7e87bde35a5a55dcc51cb8cae71
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63383262"
---
# <a name="reporting-multisample-support"></a>マルチサンプル サポートのレポート


## <span id="ddk_reporting_multisample_support_gg"></span><span id="DDK_REPORTING_MULTISAMPLE_SUPPORT_GG"></span>


ドライバーは、報告サーフェス形式ごとのピクセルごとのサンプルの数を指定することで、関連するハードウェアのマルチ サンプリング機能を報告します。 [ **DDPIXELFORMAT** ](https://msdn.microsoft.com/library/windows/hardware/ff550274)と呼ばれる構造を包含する構造体が拡張されて**MultiSampleCaps**します。 この構造体には、ドライバーの反転 (全画面表示)、blt (ウィンドウ) のマルチ サンプリングの両方のピクセルごとのサンプルの数を表現できるメンバーがあります。 各メンバーは、単語の各ビットをどのでは、値は 1 ピクセルあたりのサンプルの指定した数のサポートを示します。 WORD 型です。 そのため、ドライバーは、サーフェイスの 1 つの形式のエントリをいくつかの別のサンプル数のサポートを表現できます。

 

 






---
title: GDI レンダリング エンジンとして
description: GDI レンダリング エンジンとして
ms.assetid: 3aae0c71-fc98-452c-a7a3-f20a790a466b
keywords:
- レンダリング エンジンの GDI WDK Windows 2000 の表示
- グラフィックス ドライバー WDK Windows 2000 の表示、レンダリング エンジン
- 描画の WDK GDI レンダリング エンジン
- WDK GDI のレンダリング エンジン
- PDEV WDK GDI
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: feed077997c562dc0248f53040fffc31987dfdc0
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56529578"
---
# <a name="gdi-as-a-rendering-engine"></a>GDI レンダリング エンジンとして


## <span id="ddk_gdi_as_a_rendering_engine_gg"></span><span id="DDK_GDI_AS_A_RENDERING_ENGINE_GG"></span>


レンダリング操作では、ドライバーを有効する必要があります最初、*画面*各*PDEV*構造体が有効になっています。 PDEV は、物理デバイスの論理表現です。 ハードウェアは、GDI 標準形式のビットマップとして設定できる場合、は、一部またはすべてのビットマップの画面に描画する GDI を使用できます。 GDI も処理できる高度な[ハーフトーン](gdi-halftoning-capabilities.md)します。

有効化について*PDEVs*サーフェスを参照してください、 [ **DrvEnablePDEV** ](https://msdn.microsoft.com/library/windows/hardware/ff556211)と[ **DrvEnableSurface**](https://msdn.microsoft.com/library/windows/hardware/ff556214)関数。

 

 






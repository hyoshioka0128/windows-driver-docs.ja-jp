---
title: レンダリング エンジンとしての GDI
description: レンダリング エンジンとしての GDI
ms.assetid: 3aae0c71-fc98-452c-a7a3-f20a790a466b
keywords:
- レンダリング エンジンの GDI WDK Windows 2000 の表示
- グラフィックス ドライバー WDK Windows 2000 の表示、レンダリング エンジン
- 描画の WDK GDI レンダリング エンジン
- WDK GDI のレンダリング エンジン
- PDEV WDK GDI
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 507c77f87ddd0e2852d1647ba0b1d0355b550ea6
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67375800"
---
# <a name="gdi-as-a-rendering-engine"></a>レンダリング エンジンとしての GDI


## <span id="ddk_gdi_as_a_rendering_engine_gg"></span><span id="DDK_GDI_AS_A_RENDERING_ENGINE_GG"></span>


レンダリング操作では、ドライバーを有効する必要があります最初、*画面*各*PDEV*構造体が有効になっています。 PDEV は、物理デバイスの論理表現です。 ハードウェアは、GDI 標準形式のビットマップとして設定できる場合、は、一部またはすべてのビットマップの画面に描画する GDI を使用できます。 GDI も処理できる高度な[ハーフトーン](gdi-halftoning-capabilities.md)します。

有効化について*PDEVs*サーフェスを参照してください、 [ **DrvEnablePDEV** ](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvenablepdev)と[ **DrvEnableSurface**](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvenablesurface)関数。

 

 






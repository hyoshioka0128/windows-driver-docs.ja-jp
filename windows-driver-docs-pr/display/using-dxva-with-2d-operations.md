---
title: 2D 操作での DXVA の使用
description: 2D 操作での DXVA の使用
ms.assetid: a864941d-69ac-48a4-85a2-7e05cd3c9617
keywords:
- 2 次元操作 WDK DirectX 9.0 では、DXVA
- 2D 操作 WDK DirectX 9.0 では、DXVA
- DXVA WDK DirectX 9.0
- DXVA WDK DirectX 9.0、2D 操作
- DirectX のビデオ アクセラレータ WDK DirectX 9.0
- DirectX ビデオ アクセラレータ WDK DirectX 9.0、2D 操作
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 384adf9817d63bc3ea9f8529cdff6a83c858337a
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67370631"
---
# <a name="using-dxva-with-2d-operations"></a>2D 操作での DXVA の使用


## <span id="ddk_using_dxva_with_2d_operations_gg"></span><span id="DDK_USING_DXVA_WITH_2D_OPERATIONS_GG"></span>


DirectX 9.0 と以降のドライバーの使用、D3DDP2OP\_BLT 操作を実行するコード間ブリット[DirectX ビデオ アクセラレータ](directx-video-acceleration.md)(DXVA) 画面。 そのため、ランタイムは、DirectX 9.0 またはそれ以降のドライバーを検出した場合、ランタイム呼び出す必要があります、ドライバーの[ **D3dCreateSurfaceEx** ](https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_createsurfaceex)任意 DXVA を作成する関数 (または 2D 専用) 画面。

 

 






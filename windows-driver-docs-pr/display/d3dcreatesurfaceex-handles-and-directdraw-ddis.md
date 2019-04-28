---
title: D3dCreateSurfaceEx ハンドルと DirectDraw DDI
description: D3dCreateSurfaceEx ハンドルと DirectDraw DDI
ms.assetid: 626b04a2-3c50-425a-bbdf-3fb24fc95215
keywords:
- コンテキスト WDK の Direct3D D3dCreateSurfaceEx
- D3dCreateSurfaceEx
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8351408c2feac317228a713fc1085bf418a37f0a
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63372750"
---
# <a name="d3dcreatesurfaceex-handles-and-directdraw-ddis"></a>D3dCreateSurfaceEx ハンドルと DirectDraw DDI


## <span id="ddk_d3dcreatesurfaceex_handles_and_directdraw_ddis_gg"></span><span id="DDK_D3DCREATESURFACEEX_HANDLES_AND_DIRECTDRAW_DDIS_GG"></span>


ハンドルは DirectDraw マネージ DDRAWI から DirectX 7.0 のドライバーを完全に隔離いない\_DDSURFACE\_よりと DDRAWI\_DDSURFACE\_ローカル構造体。 これらの構造体の名前は、構造体の別名には基本的に[ **DD\_画面\_詳細**](https://msdn.microsoft.com/library/windows/hardware/ff551737)と[ **DD\_画面\_ローカル**](https://msdn.microsoft.com/library/windows/hardware/ff551733)します。 DirectDraw Ddi などで[ *DdBlt* ](https://msdn.microsoft.com/library/windows/hardware/ff549205)と[ *DdFlip*](https://msdn.microsoft.com/library/windows/hardware/ff549306)ドライバーが surface 構造体のポインターが渡され、これらを使用できる必要がありますそのプライベート表現ではなく構造体。

 

 






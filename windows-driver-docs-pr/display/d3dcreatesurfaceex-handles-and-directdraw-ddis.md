---
title: D3dCreateSurfaceEx ハンドルと DirectDraw Ddi
description: D3dCreateSurfaceEx ハンドルと DirectDraw Ddi
ms.assetid: 626b04a2-3c50-425a-bbdf-3fb24fc95215
keywords:
- コンテキスト WDK の Direct3D D3dCreateSurfaceEx
- D3dCreateSurfaceEx
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8351408c2feac317228a713fc1085bf418a37f0a
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56557868"
---
# <a name="d3dcreatesurfaceex-handles-and-directdraw-ddis"></a>D3dCreateSurfaceEx ハンドルと DirectDraw Ddi


## <span id="ddk_d3dcreatesurfaceex_handles_and_directdraw_ddis_gg"></span><span id="DDK_D3DCREATESURFACEEX_HANDLES_AND_DIRECTDRAW_DDIS_GG"></span>


ハンドルは DirectDraw マネージ DDRAWI から DirectX 7.0 のドライバーを完全に隔離いない\_DDSURFACE\_よりと DDRAWI\_DDSURFACE\_ローカル構造体。 これらの構造体の名前は、構造体の別名には基本的に[ **DD\_画面\_詳細**](https://msdn.microsoft.com/library/windows/hardware/ff551737)と[ **DD\_画面\_ローカル**](https://msdn.microsoft.com/library/windows/hardware/ff551733)します。 DirectDraw Ddi などで[ *DdBlt* ](https://msdn.microsoft.com/library/windows/hardware/ff549205)と[ *DdFlip*](https://msdn.microsoft.com/library/windows/hardware/ff549306)ドライバーが surface 構造体のポインターが渡され、これらを使用できる必要がありますそのプライベート表現ではなく構造体。

 

 






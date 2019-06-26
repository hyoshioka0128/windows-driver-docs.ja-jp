---
title: D3dCreateSurfaceEx ハンドルと DirectDraw DDI
description: D3dCreateSurfaceEx ハンドルと DirectDraw DDI
ms.assetid: 626b04a2-3c50-425a-bbdf-3fb24fc95215
keywords:
- コンテキスト WDK の Direct3D D3dCreateSurfaceEx
- D3dCreateSurfaceEx
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 627b62b1e523f869c19471ddb74291ed878c0279
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67370157"
---
# <a name="d3dcreatesurfaceex-handles-and-directdraw-ddis"></a>D3dCreateSurfaceEx ハンドルと DirectDraw DDI


## <span id="ddk_d3dcreatesurfaceex_handles_and_directdraw_ddis_gg"></span><span id="DDK_D3DCREATESURFACEEX_HANDLES_AND_DIRECTDRAW_DDIS_GG"></span>


ハンドルは DirectDraw マネージ DDRAWI から DirectX 7.0 のドライバーを完全に隔離いない\_DDSURFACE\_よりと DDRAWI\_DDSURFACE\_ローカル構造体。 これらの構造体の名前は、構造体の別名には基本的に[ **DD\_画面\_詳細**](https://docs.microsoft.com/windows/desktop/api/ddrawint/ns-ddrawint-_dd_surface_more)と[ **DD\_画面\_ローカル**](https://docs.microsoft.com/windows/desktop/api/ddrawint/ns-ddrawint-_dd_surface_local)します。 DirectDraw Ddi などで[ *DdBlt* ](https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_surfcb_blt)と[ *DdFlip*](https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_surfcb_flip)ドライバーが surface 構造体のポインターが渡され、これらを使用できる必要がありますそのプライベート表現ではなく構造体。

 

 






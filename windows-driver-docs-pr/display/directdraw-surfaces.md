---
title: DirectDraw サーフェス
description: DirectDraw サーフェス
ms.assetid: be99b124-5193-4826-be28-ed6a132b84af
keywords:
- 描画サーフェイス WDK DirectDraw、サーフェスについて
- サーフェスについて、DirectDraw サーフェス WDK Windows 2000 の表示します。
- WDK DirectDraw、サーフェスについて明らかになります
- 機能は、WDK DirectDraw をビットします。
- bits WDK DirectDraw の上限を設定します。
- 描画サーフェス WDK DirectDraw
- DirectDraw サーフェス WDK Windows 2000 を表示します。
- サーフェス WDK DirectDraw
- サーフェスの WDK DirectDraw、機能ビット
- プライマリ サーフェス WDK DirectDraw
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 440d2c7f6162356df3419e578c4dce819e3f7e5f
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67379373"
---
# <a name="directdraw-surfaces"></a>DirectDraw サーフェス


## <span id="ddk_directdraw_surfaces_gg"></span><span id="DDK_DIRECTDRAW_SURFACES_GG"></span>


Microsoft の DirectDraw Surface は、Microsoft DirectX グラフィックスの画像の基本単位です。 特定の幅、高さ、およびピクセル形式のピクセルの四角形のコレクションです。または、マイクロソフトの Direct3D のコマンドまたは頂点を格納するバッファー。 サーフェスでは、それらに関連付けられているそれぞれの動作と使用状況を示すビットがあります。 これらのビットが呼び出される*サーフェス機能ビット*(または*ビットの上限を設定*略して)。 Cap ビットがレンダリングのテクセルを保持しているなど、関連付けられているサーフェイスの使用目的を示す (、DDSCAPS\_テクスチャ cap ビット)、3 D レンダリングの対象にする (DDSCAPS\_3DDEVICE)、およびその他の多くの。 Surface cap bits の詳細については、次を参照してください。、 [ **DDSCAPS** ](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff550286(v=vs.85))構造体。

*プライマリ*サーフェイス ディスプレイ カード、モニターをスキャンされているサーフェイスです。 プライマリのサーフェスの詳細については、次を参照してください。、 [Flipping](flipping.md)と[メモリ構成](memory-configurations.md)セクション。

 

 






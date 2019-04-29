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
ms.openlocfilehash: bbbbe4b3033c53677a9af0e145300f791c61db4f
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63392058"
---
# <a name="directdraw-surfaces"></a>DirectDraw サーフェス


## <span id="ddk_directdraw_surfaces_gg"></span><span id="DDK_DIRECTDRAW_SURFACES_GG"></span>


Microsoft の DirectDraw Surface は、Microsoft DirectX グラフィックスの画像の基本単位です。 特定の幅、高さ、およびピクセル形式のピクセルの四角形のコレクションです。または、マイクロソフトの Direct3D のコマンドまたは頂点を格納するバッファー。 サーフェスでは、それらに関連付けられているそれぞれの動作と使用状況を示すビットがあります。 これらのビットが呼び出される*サーフェス機能ビット*(または*ビットの上限を設定*略して)。 Cap ビットがレンダリングのテクセルを保持しているなど、関連付けられているサーフェイスの使用目的を示す (、DDSCAPS\_テクスチャ cap ビット)、3 D レンダリングの対象にする (DDSCAPS\_3DDEVICE)、およびその他の多くの。 Surface cap bits の詳細については、次を参照してください。、 [ **DDSCAPS** ](https://msdn.microsoft.com/library/windows/hardware/ff550286)構造体。

*プライマリ*サーフェイス ディスプレイ カード、モニターをスキャンされているサーフェイスです。 プライマリのサーフェスの詳細については、次を参照してください。、 [Flipping](flipping.md)と[メモリ構成](memory-configurations.md)セクション。

 

 






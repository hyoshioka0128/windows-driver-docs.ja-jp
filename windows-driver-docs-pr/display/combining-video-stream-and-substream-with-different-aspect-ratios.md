---
title: 縦横比が異なるビデオ ストリームおよびサブストリームの結合
description: このトピックでは、異なる縦横比とビデオ ストリーム、ビデオのサブストリームおよび背景色を結合する方法を示します。
ms.assetid: 3c147829-c76a-4bc7-bb14-bb49609f53d8
keywords:
- ストリームと WDK DirectX VA サブストリームの組み合わせ
- ビデオ ストリームとサブストリーム WDK DirectX VA を組み合わせる
- WDK DirectX VA を合わせたサブストリームとビデオ ストリーム
- WDK DirectX VA の縦横比
- ストリームは、WDK DirectX VA を組み合わせる
ms.date: 12/06/2018
ms.localizationpriority: medium
ms.custom: seodec18
ms.openlocfilehash: f58bb5a966f7bf6f69cabaffb2e3d72400145eaa
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63343046"
---
# <a name="combining-video-stream-and-substream-with-different-aspect-ratios"></a>Stream のビデオと縦横比が異なるとサブストリームの組み合わせ


## <span id="ddk_combining_video_stream_and_substream_with_different_aspect_ratios_"></span><span id="DDK_COMBINING_VIDEO_STREAM_AND_SUBSTREAM_WITH_DIFFERENT_ASPECT_RATIOS_"></span>


このセクションでは、Windows Server 2003 SP1 以降、および Windows XP SP2 以降にのみ適用されます。

次の例では、VMR はした宛先表面が完全にカバーしない、ビデオ ストリームの転送先の四角形のドライバーを呼び出します。 この例は、VMR ビデオ ストリームが縦横比 4:3 では、サブピクチャ ストリームがアスペクト比 16:9 での dvd の収録内容を表示するときに発生します。

次の図は、この例では、ビデオ ストリーム、ビデオのサブストリームおよび背景色が結合方法を示します。

![異なる縦横比とビデオ ストリーム、ビデオのサブストリームおよび背景色を組み合わせることを示す図](images/trgrect2.png)

前の例では、四角形は次のとおりです。

-   ビデオのストリーム ソースの四角形は {0, 0,720,480}、{107, 0, 747,480} 先の四角形。

-   サブピクチャ ストリームでは、元の四角形は {0, 0,720,480} 先の四角形は、{0, 0,854,480}。

-   ターゲットの四角形は、{0, 0,854,480}。

前の例に示すように、変換先の画面の左と右のエッジにビデオ ストリームからのピクセルは含まれません。 ドライバーの**DeinterlaceBltEx**関数は、サブピクチャ ストリームからピクセルと組み合わされるため、背景色として、ビデオ ストリームの転送先の四角形を外にあるピクセルを解釈する必要があります。

 

 






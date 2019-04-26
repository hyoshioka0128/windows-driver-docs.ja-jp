---
title: デインターレースとビデオ サブストリーム合成の結合
description: デインターレースとビデオ サブストリーム合成の結合
ms.assetid: d62fe460-104d-4aff-a88c-3dc5829321fa
keywords:
- DeinterlaceBltEx
- デインター レース WDK DirectX va なので、サブストリームの合成を組み合わせること
- 結合サブストリームの合成 WDK DirectX VA
- ビデオのサブストリーム合成 WDK DirectX VA
- サブストリームの合成 WDK DirectX VA
- VMR WDK DirectX VA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6bc6b2687d08c9b0a38c244d6a08834979bfce22
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63343016"
---
# <a name="combining-deinterlacing-and-video-substream-compositing"></a>デインターレースとビデオ サブストリーム合成の結合


## <span id="ddk_combining_deinterlacing_and_video_substream_compositing_gg"></span><span id="DDK_COMBINING_DEINTERLACING_AND_VIDEO_SUBSTREAM_COMPOSITING_GG"></span>


このセクションでは、Microsoft Windows Server 2003 Service Pack 1 (SP1) 以降、および Windows XP Service Pack 2 (SP2) 以降にのみ適用されます。

ドライバー作成者が実装できるハードウェア上で限られたメモリ帯域幅のビデオの品質を向上させるのには[ **DeinterlaceBltEx** ](https://msdn.microsoft.com/library/windows/hardware/ff563927)ディスプレイ ドライバーでの関数。 **DeinterlaceBltEx** YUV 色空間内で、関数を組み合わせて、ビデオの substreams インター レースを解除する操作やフレーム レートのビデオ ストリームの上にその複合操作は、各ビデオのフレームを変換します。 ドライバー作成者がサポートすることが推奨されます、 **DeinterlaceBltEx**デインター レース、モードのすべてのドライバーに機能します。

次のトピックをサポートする方法を説明する**DeinterlaceBltEx**:

[DeinterlaceBltEx の概要](overview-of-deinterlacebltex.md)

[レポートの DeinterlaceBltEx のサポート](reporting-support-for-deinterlacebltex.md)

[ビデオ サブストリームと宛先表面の指定](supplying-video-substream-and-destination-surfaces.md)

[ビデオ サブストリームと宛先表面での操作をサポートしています。](supporting-operations-on-video-substream-and-destination-surfaces.md)

[ターゲットの四角形の色のサンプルと背景を表示します。](displaying-samples-and-background-color-in-the-target-rectangle.md)

[Subrectangles の処理](processing-subrectangles.md)

[入力バッファーの順序](input-buffer-order.md)

[デインター レース、64 ビット オペレーティング システムで合成](deinterlacing-and-compositing-on-64-bit-operating-systems.md)

 

 






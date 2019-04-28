---
title: ビデオ VBI キャプチャ
description: ビデオ VBI キャプチャ
ms.assetid: 40544838-8678-4832-8e6f-e96202f987ad
keywords:
- ビデオ VBI キャプチャ WDK DirectDraw
- 垂直帰線消去期間 WDK DirectDraw
- VBI WDK DirectDraw
- DxTransfer
- DxApi ミニポート ドライバー WDK DirectDraw、VBI をキャプチャします。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ee21f6f16ba94d2977806c51fae6fbb820ec9078
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63365057"
---
# <a name="video-vbi-capture"></a>ビデオ VBI キャプチャ


## <span id="ddk_video_vbi_capture_gg"></span><span id="DDK_VIDEO_VBI_CAPTURE_GG"></span>


DirectX 5.2 では、垂直帰線消去期間 (VBI) のビデオ キャプチャの 2 つの DirectDraw ドライバー関数が導入されました。 これらの関数は[ *DxTransfer* ](https://msdn.microsoft.com/library/windows/hardware/ff562887)と[ *DxGetTransferStatus*](https://msdn.microsoft.com/library/windows/hardware/ff557438)します。

*DxTransfer*関数では、ビデオ、および VBI キャプチャが容易になります。 この関数は IRQ 時に呼び出されると、ため、できるだけ早く返す必要があります。 ディスプレイ ハードウェアが、時に、バス マスターを行う準備がない場合*DxTransfer*と呼ばれる場合は、ビデオのミニポート ドライバー、バス マスター数の内部キューにならないようにし、(キューに保存されているバス マスターの実際の数が最大には、ドライバー開発者の場合)。 これにより、ハードウェアの準備ができたときに、バス マスターを実行するハードウェアです。 つまり、ドライバーがポーリングされません、およびバス マスターが完了するまで待機する必要があります。

DirectDraw を呼び出すと、 *DxTransfer*関数に転送 ID を提供、 **dwTransferID**のメンバー、 [ **DDTRANSFERININFO** ](https://msdn.microsoft.com/library/windows/hardware/ff550356)構造体。 ビデオのミニポート ドライバーは、この id を使用できますし、ときに、 *DxGetTransferStatus*関数が呼び出されます。

バス マスターが完了したら、ディスプレイ ハードウェアは IRQ を生成する必要があります。 ビデオのミニポート ドライバーに呼び出す必要がありますし、 [ **IRQCallback** ](https://msdn.microsoft.com/library/windows/hardware/ff568158)関数で指定された[ *DxEnableIRQ*](https://msdn.microsoft.com/library/windows/hardware/ff557413)します。 この**IRQCallback**呼び出し、ビデオのミニポート ドライバーの指定、DDIRQ\_バスマスター フラグ。 DirectDraw を呼び出して、 [ *DxGetTransferStatus* ](https://msdn.microsoft.com/library/windows/hardware/ff557438)どのバスを判断する関数マスターが完了しました。 ビデオのミニポート ドライバーは、転送 ID を返す必要があります (**dwTransferID**) DirectDraw が以前のドライバーに渡される*DxTransfer*呼び出します。 この方法で、ドライバーに 5 つのバス マスターがある場合は、キューで DirectDraw を判断できます最も最近完了したもの。

 

 






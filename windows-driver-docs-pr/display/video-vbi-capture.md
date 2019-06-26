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
ms.openlocfilehash: cd0696abed9b168383c9b79bc2482eac763f7069
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67372616"
---
# <a name="video-vbi-capture"></a>ビデオ VBI キャプチャ


## <span id="ddk_video_vbi_capture_gg"></span><span id="DDK_VIDEO_VBI_CAPTURE_GG"></span>


DirectX 5.2 では、垂直帰線消去期間 (VBI) のビデオ キャプチャの 2 つの DirectDraw ドライバー関数が導入されました。 これらの関数は[ *DxTransfer* ](https://docs.microsoft.com/windows/desktop/api/dxmini/nc-dxmini-pdx_transfer)と[ *DxGetTransferStatus*](https://docs.microsoft.com/windows/desktop/api/dxmini/nc-dxmini-pdx_gettransferstatus)します。

*DxTransfer*関数では、ビデオ、および VBI キャプチャが容易になります。 この関数は IRQ 時に呼び出されると、ため、できるだけ早く返す必要があります。 ディスプレイ ハードウェアが、時に、バス マスターを行う準備がない場合*DxTransfer*と呼ばれる場合は、ビデオのミニポート ドライバー、バス マスター数の内部キューにならないようにし、(キューに保存されているバス マスターの実際の数が最大には、ドライバー開発者の場合)。 これにより、ハードウェアの準備ができたときに、バス マスターを実行するハードウェアです。 つまり、ドライバーがポーリングされません、およびバス マスターが完了するまで待機する必要があります。

DirectDraw を呼び出すと、 *DxTransfer*関数に転送 ID を提供、 **dwTransferID**のメンバー、 [ **DDTRANSFERININFO** ](https://docs.microsoft.com/windows/desktop/api/dxmini/ns-dxmini-_ddtransferininfo)構造体。 ビデオのミニポート ドライバーは、この id を使用できますし、ときに、 *DxGetTransferStatus*関数が呼び出されます。

バス マスターが完了したら、ディスプレイ ハードウェアは IRQ を生成する必要があります。 ビデオのミニポート ドライバーに呼び出す必要がありますし、 [ **IRQCallback** ](https://docs.microsoft.com/windows/desktop/api/dxmini/nc-dxmini-pdx_irqcallback)関数で指定された[ *DxEnableIRQ*](https://docs.microsoft.com/windows/desktop/api/dxmini/nc-dxmini-pdx_enableirq)します。 この**IRQCallback**呼び出し、ビデオのミニポート ドライバーの指定、DDIRQ\_バスマスター フラグ。 DirectDraw を呼び出して、 [ *DxGetTransferStatus* ](https://docs.microsoft.com/windows/desktop/api/dxmini/nc-dxmini-pdx_gettransferstatus)どのバスを判断する関数マスターが完了しました。 ビデオのミニポート ドライバーは、転送 ID を返す必要があります (**dwTransferID**) DirectDraw が以前のドライバーに渡される*DxTransfer*呼び出します。 この方法で、ドライバーに 5 つのバス マスターがある場合は、キューで DirectDraw を判断できます最も最近完了したもの。

 

 






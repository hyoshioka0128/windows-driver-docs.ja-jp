---
title: ビデオ要求の処理 (Windows 2000 モデル)
description: ビデオ要求の処理 (Windows 2000 モデル)
ms.assetid: 86b3037e-2d18-46b0-8b02-c66be65a4001
keywords:
- ビデオのミニポート ドライバー WDK Windows 2000、要求の処理
- 要求処理の WDK ビデオのミニポート
- I/O WDK ビデオのミニポート
- HwVidStartIO
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 375947591df95ffe9ef003b8009b9e2af8e146c5
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67363687"
---
# <a name="processing-video-requests-windows-2000-model"></a>ビデオ要求の処理 (Windows 2000 モデル)


## <span id="ddk_processing_video_requests_windows_2000_model__gg"></span><span id="DDK_PROCESSING_VIDEO_REQUESTS_WINDOWS_2000_MODEL__GG"></span>


ディスプレイ ドライバーの呼び出しで発生するすべての I/O 要求**EngDeviceIoControl**ビデオ ポート ドライバー。 ビデオ ポート ドライバーを呼び出して、対応するミニポート ドライバーの[ *HwVidStartIO* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/video/nc-video-pvideo_hw_start_io)それぞれへのポインターを関数[**ビデオ\_要求\_パケット**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/video/ns-video-_video_request_packet)構造体を設定します。 送信されるすべての VRPs *HwVidStartIO*が、 **IoControlCode**メンバーは、IOCTL に設定\_ビデオ\_*XXX*します。

ビデオ ポート ドライバーは、ミニポート ドライバーごとに送信することによってすべてのビデオのミニポート ドライバーの受信要求の同期を管理することも*HwVidStartIO*ルーチン、一度に処理するための 1 つだけの VRP します。 *HwVidStartIO*ミニポート ドライバーが要求された操作を完了してコントロールを返すまで、各入力 VRP を所有しています。 I/O マネージャーが後続の呼び出しへの応答で送信するすべての未処理の IRP コードへのビデオ ポート ドライバーを保持ミニポート ドライバーは、現在 VRP を完了するまで[ **EngDeviceIoControl** ](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-engdeviceiocontrol)によって、対応するドライバーが表示されます。

ビデオの要求の受信時に[ *HwVidStartIO* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/video/nc-video-pvideo_hw_start_io) 、VRP を調べて、ビデオ アダプターの要求を処理、VRP で適切な状態とその他の情報を設定およびを返す必要があります**は TRUE。** .

 

 






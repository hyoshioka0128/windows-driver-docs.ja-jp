---
title: ビデオ要求の処理 (Windows 2000 モデル)
description: ビデオ要求の処理 (Windows 2000 モデル)
ms.assetid: 86b3037e-2d18-46b0-8b02-c66be65a4001
keywords:
- ビデオミニポートドライバー WDK Windows 2000、要求の処理
- 要求処理 WDK ビデオミニポート
- I/o WDK ビデオミニポート
- HwVidStartIO
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e1e0b9ded291e5e2bba556d7f88c6565a7c8830c
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72829682"
---
# <a name="processing-video-requests-windows-2000-model"></a>ビデオ要求の処理 (Windows 2000 モデル)


## <span id="ddk_processing_video_requests_windows_2000_model__gg"></span><span id="DDK_PROCESSING_VIDEO_REQUESTS_WINDOWS_2000_MODEL__GG"></span>


ビデオポートドライバーによって**EngDeviceIoControl**へのディスプレイドライバーの呼び出しで発生したすべての i/o 要求。 次に、ビデオポートドライバーは、対応するミニポートドライバーの[*HwVidStartIO*](https://docs.microsoft.com/windows-hardware/drivers/ddi/video/nc-video-pvideo_hw_start_io)関数を呼び出して、設定されている各[**ビデオ\_要求\_パケット**](https://docs.microsoft.com/windows-hardware/drivers/ddi/video/ns-video-_video_request_packet)構造へのポインターを返します。 *HwVidStartIO*に送信されるすべての vrps は、 **iocontrolcode**メンバーを IOCTL\_VIDEO\_*XXX*に設定しています。

また、ビデオポートドライバーは、各ミニポートドライバーの*HwVidStartIO*ルーチンを一度に1つの VRP に送信することで、すべてのビデオミニポートドライバーの受信要求の同期も管理します。 *HwVidStartIO*は、ミニポートドライバーが要求された操作を完了し、制御を返すまで、各入力 VRP を所有します。 ミニポートドライバーが現在の VRP を完了するまで、ビデオポートドライバーは、対応するディスプレイドライバーによって[**EngDeviceIoControl**](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-engdeviceiocontrol)への後続の呼び出しに応答して送信される未処理の IRP コードを保持します。

ビデオ要求を受信すると、 [*HwVidStartIO*](https://docs.microsoft.com/windows-hardware/drivers/ddi/video/nc-video-pvideo_hw_start_io)は VRP を調べて、アダプターでビデオ要求を処理し、VRP に適切な状態とその他の情報を設定して、 **TRUE**を返す必要があります。

 

 






---
title: ビデオの要求の処理 (Windows 2000 モデル)
description: ビデオの要求の処理 (Windows 2000 モデル)
ms.assetid: 86b3037e-2d18-46b0-8b02-c66be65a4001
keywords:
- ビデオのミニポート ドライバー WDK Windows 2000、要求の処理
- 要求処理の WDK ビデオのミニポート
- I/O WDK ビデオのミニポート
- HwVidStartIO
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c377d2f24d2361c64604aa6b17b9d334f13242f5
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56557784"
---
# <a name="processing-video-requests-windows-2000-model"></a>ビデオの要求の処理 (Windows 2000 モデル)


## <span id="ddk_processing_video_requests_windows_2000_model__gg"></span><span id="DDK_PROCESSING_VIDEO_REQUESTS_WINDOWS_2000_MODEL__GG"></span>


ディスプレイ ドライバーの呼び出しで発生するすべての I/O 要求**EngDeviceIoControl**ビデオ ポート ドライバー。 ビデオ ポート ドライバーを呼び出して、対応するミニポート ドライバーの[ *HwVidStartIO* ](https://msdn.microsoft.com/library/windows/hardware/ff567367)それぞれへのポインターを関数[**ビデオ\_要求\_パケット**](https://msdn.microsoft.com/library/windows/hardware/ff570547)構造体を設定します。 送信されるすべての VRPs *HwVidStartIO*が、 **IoControlCode**メンバーは、IOCTL に設定\_ビデオ\_*XXX*します。

ビデオ ポート ドライバーは、ミニポート ドライバーごとに送信することによってすべてのビデオのミニポート ドライバーの受信要求の同期を管理することも*HwVidStartIO*ルーチン、一度に処理するための 1 つだけの VRP します。 *HwVidStartIO*ミニポート ドライバーが要求された操作を完了してコントロールを返すまで、各入力 VRP を所有しています。 I/O マネージャーが後続の呼び出しへの応答で送信するすべての未処理の IRP コードへのビデオ ポート ドライバーを保持ミニポート ドライバーは、現在 VRP を完了するまで[ **EngDeviceIoControl** ](https://msdn.microsoft.com/library/windows/hardware/ff564838)によって、対応するドライバーが表示されます。

ビデオの要求の受信時に[ *HwVidStartIO* ](https://msdn.microsoft.com/library/windows/hardware/ff567367) 、VRP を調べて、ビデオ アダプターの要求を処理、VRP で適切な状態とその他の情報を設定およびを返す必要があります**は TRUE。**.

 

 






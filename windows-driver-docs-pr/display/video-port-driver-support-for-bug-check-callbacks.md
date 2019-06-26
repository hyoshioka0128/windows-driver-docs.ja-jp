---
title: バグ チェック コールバックのビデオ ポート ドライバー サポート
description: バグ チェック コールバックのビデオ ポート ドライバー サポート
ms.assetid: 181fd4f2-feed-4759-80a7-aec97b9094b3
keywords:
- ビデオのミニポート ドライバー WDK Windows 2000 では、バグ チェック コールバック
- バグ チェック コールバック WDK ビデオのミニポート
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1e3e90d207eb07c221161ee17a8ba4555e453c9f
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67372626"
---
# <a name="video-port-driver-support-for-bug-check-callbacks"></a>バグ チェック コールバックのビデオ ポート ドライバー サポート


## <span id="ddk_video_port_driver_support_for_bug_check_callbacks_gg"></span><span id="DDK_VIDEO_PORT_DRIVER_SUPPORT_FOR_BUG_CHECK_CALLBACKS_GG"></span>


Windows XP SP1 以降では、ビデオのミニポート ドライバーを実装および登録できる[ **HwVidBugcheckCallback**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/video/nc-video-pvideo_bugcheck_callback)、システムを呼び出すときに関数[ **0 xea (スレッドのバグ チェック\_STUCK\_IN\_デバイス\_ドライバー)** ](https://docs.microsoft.com/windows-hardware/drivers/debugger/bug-check-0xea--thread-stuck-in-device-driver)に発生します。 *HwVidBugcheckCallback*ドライバー開発者は、ドライバーの問題の診断に使用できるダンプ ファイルに独自のデータを追加することができます。

登録について*HwVidBugcheckCallback*、次のトピックを参照してください。

[ビデオのミニポート ドライバー関数を個別に登録](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/index)

[**VideoPortRegisterBugcheckCallback**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/video/nf-video-videoportregisterbugcheckcallback)

 

 






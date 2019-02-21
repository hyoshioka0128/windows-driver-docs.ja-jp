---
title: バグ チェック コールバックのビデオ ポート ドライバー サポート
description: バグ チェック コールバックのビデオ ポート ドライバー サポート
ms.assetid: 181fd4f2-feed-4759-80a7-aec97b9094b3
keywords:
- ビデオのミニポート ドライバー WDK Windows 2000 では、バグ チェック コールバック
- バグ チェック コールバック WDK ビデオのミニポート
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4de71773780a510b68e0cd448c221d2be7fc522e
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56556967"
---
# <a name="video-port-driver-support-for-bug-check-callbacks"></a>バグ チェック コールバックのビデオ ポート ドライバー サポート


## <span id="ddk_video_port_driver_support_for_bug_check_callbacks_gg"></span><span id="DDK_VIDEO_PORT_DRIVER_SUPPORT_FOR_BUG_CHECK_CALLBACKS_GG"></span>


Windows XP SP1 以降では、ビデオのミニポート ドライバーを実装および登録できる[ **HwVidBugcheckCallback**](https://msdn.microsoft.com/library/windows/hardware/ff567324)、システムを呼び出すときに関数[ **0 xea (スレッドのバグ チェック\_STUCK\_IN\_デバイス\_ドライバー)** ](https://msdn.microsoft.com/library/windows/hardware/ff560350)に発生します。 *HwVidBugcheckCallback*ドライバー開発者は、ドライバーの問題の診断に使用できるダンプ ファイルに独自のデータを追加することができます。

登録について*HwVidBugcheckCallback*、次のトピックを参照してください。

[ビデオのミニポート ドライバー関数を個別に登録](https://msdn.microsoft.com/library/windows/hardware/ff567672)

[**VideoPortRegisterBugcheckCallback**](https://msdn.microsoft.com/library/windows/hardware/ff570353)

 

 






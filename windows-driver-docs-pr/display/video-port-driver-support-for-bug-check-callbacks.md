---
title: バグ チェック コールバックのビデオ ポート ドライバー サポート
description: バグ チェック コールバックのビデオ ポート ドライバー サポート
ms.assetid: 181fd4f2-feed-4759-80a7-aec97b9094b3
keywords:
- ビデオミニポートドライバー WDK Windows 2000、バグチェックコールバック
- バグチェックコールバックの WDK ビデオミニポート
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 51a7080ea6c95b11ad1480197b6c0eba677f2522
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72829186"
---
# <a name="video-port-driver-support-for-bug-check-callbacks"></a>バグ チェック コールバックのビデオ ポート ドライバー サポート


## <span id="ddk_video_port_driver_support_for_bug_check_callbacks_gg"></span><span id="DDK_VIDEO_PORT_DRIVER_SUPPORT_FOR_BUG_CHECK_CALLBACKS_GG"></span>


Windows XP SP1 以降では、ビデオミニポートドライバーは[**HwVidBugcheckCallback**](https://docs.microsoft.com/windows-hardware/drivers/ddi/video/nc-video-pvideo_bugcheck_callback)を実装し、登録することができます。これは、[**バグチェック 0xea (\_デバイス\_ドライバーのスレッド\_スタック\_)** ](https://docs.microsoft.com/windows-hardware/drivers/debugger/bug-check-0xea--thread-stuck-in-device-driver)が発生したときにシステムが呼び出す関数です。 *HwVidBugcheckCallback*は、ドライバーの開発者がドライバーの問題を診断するために使用できる、独自のデータをダンプファイルに追加できます。

*HwVidBugcheckCallback*の登録の詳細については、次のトピックを参照してください。

[個別に登録されたビデオミニポートドライバーの機能](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)

[**Videoportregisterバグチェックコールバック**](https://docs.microsoft.com/windows-hardware/drivers/ddi/video/nf-video-videoportregisterbugcheckcallback)

 

 






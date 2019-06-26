---
title: ビデオ ミニポート ドライバーのタイマー
description: ビデオ ミニポート ドライバーのタイマー
ms.assetid: 257ea76e-7be6-4895-8e83-0f50c96e5969
keywords:
- ビデオのミニポート ドライバー WDK Windows 2000 では、タイマー
- タイマー WDK ビデオのミニポート
- HwVidTimer
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 633464727896f2aa3e0c1d02975515a806525f8f
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67385655"
---
# <a name="timers-in-video-miniport-drivers"></a>ビデオ ミニポート ドライバーのタイマー


## <span id="ddk_timers_in_video_miniport_drivers_gg"></span><span id="DDK_TIMERS_IN_VIDEO_MINIPORT_DRIVERS_GG"></span>


ビデオのミニポート ドライバーが持つことができます、 [ **HwVidTimer** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/video/nc-video-pvideo_hw_timer)ドライバー開発者の判断での関数。 A *HwVidTimer*関数により、タイムアウトになる操作や状態を監視するミニポート ドライバーは、呼び出すことによってよりも細かい単位の間隔の経過と共に変化[ **VideoPortStallExecution**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/video/nf-video-videoportstallexecution). *HwVidTimer*からとして発生している場合は、他のシステム操作を妨げませんも**VideoPortStallExecution**は。

たとえば、VGA 機能をエミュレートするアダプターのミニポート ドライバーがある、 *HwVidTimer*ドライバーは、VGA スタイルのグラフィックスをエミュレートできるようにそのアダプターの"VGA"の状態を監視する関数は定期的に登録します。

呼び出しの後に[ **VideoPortStartTimer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/video/nf-video-videoportstarttimer)、ビデオ ポート ドライバー呼び出し*HwVidTimer*ビデオのミニポート ドライバー呼び出されるまで毎秒 1 回[ **VideoPortStopTimer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/video/nf-video-videoportstoptimer)します。 ビデオのミニポート ドライバーが有効にしてへの呼び出しを無効にする、 *HwVidTimer*繰り返し関数。

なお、 *HwVidTimer*関数自体への呼び出しを無効にできません**VideoPortStopTimer**します。 別のビデオのミニポート ドライバー関数は、有効化、またはへの呼び出しの無効化を制御する必要があります、 *HwVidTimer*関数の使用により**VideoPortStartTimer**と**VideoPortStopTimer**.

 

 






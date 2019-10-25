---
title: ビデオ ミニポート ドライバーのタイマー
description: ビデオ ミニポート ドライバーのタイマー
ms.assetid: 257ea76e-7be6-4895-8e83-0f50c96e5969
keywords:
- ビデオミニポートドライバー WDK Windows 2000、タイマー
- タイマー WDK ビデオミニポート
- HwVidTimer
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e917c96fe18156d60323c807ab8c45979ed4e3c6
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72825426"
---
# <a name="timers-in-video-miniport-drivers"></a>ビデオ ミニポート ドライバーのタイマー


## <span id="ddk_timers_in_video_miniport_drivers_gg"></span><span id="DDK_TIMERS_IN_VIDEO_MINIPORT_DRIVERS_GG"></span>


ビデオミニポートドライバーは、ドライバーライターの裁量で[**HwVidTimer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/video/nc-video-pvideo_hw_timer)関数を持つことができます。 *HwVidTimer*関数を使用すると、ミニポートドライバーは、 [**Videoportstallexecution**](https://docs.microsoft.com/windows-hardware/drivers/ddi/video/nf-video-videoportstallexecution)を呼び出すことによって可能な時間よりも粗い間隔で、状態の変化を監視することができます。 また、 *HwVidTimer*では、 **Videoportstallexecution**と同様に、他のシステム操作が発生するのを防ぐことはできません。

たとえば、VGA 機能をエミュレートするアダプターのミニポートドライバーには、アダプターの "VGA" レジスタの状態を定期的に監視し、ドライバーが VGA スタイルのグラフィックスをエミュレートできるようにする*HwVidTimer*関数が含まれている場合があります。

[**Videoportstarttimer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/video/nf-video-videoportstarttimer)を呼び出した後、ビデオのミニポートドライバーが[**videoportstarttimer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/video/nf-video-videoportstoptimer)*を呼び出すまで*、ビデオポートドライバーは毎秒1回呼び出します。 ビデオミニポートドライバーは、 *HwVidTimer*関数への呼び出しを繰り返し有効または無効にすることができます。

*HwVidTimer*関数は、 **Videoportst er**でそれ自体への呼び出しを無効にすることはできないことに注意してください。 別のビデオミニポートドライバー関数は、 **Videoportstarttimer**と**Videoportstarttimer er**を使用して *、関数の*呼び出しの有効化または無効化を制御する必要があります。

 

 






---
title: ビデオのミニポート ドライバーのタイマー
description: ビデオのミニポート ドライバーのタイマー
ms.assetid: 257ea76e-7be6-4895-8e83-0f50c96e5969
keywords:
- ビデオのミニポート ドライバー WDK Windows 2000 では、タイマー
- タイマー WDK ビデオのミニポート
- HwVidTimer
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 87fe04e53916866dc27ef9cc36436ffc3f987a37
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56558183"
---
# <a name="timers-in-video-miniport-drivers"></a>ビデオのミニポート ドライバーのタイマー


## <span id="ddk_timers_in_video_miniport_drivers_gg"></span><span id="DDK_TIMERS_IN_VIDEO_MINIPORT_DRIVERS_GG"></span>


ビデオのミニポート ドライバーが持つことができます、 [ **HwVidTimer** ](https://msdn.microsoft.com/library/windows/hardware/ff567371)ドライバー開発者の判断での関数。 A *HwVidTimer*関数により、タイムアウトになる操作や状態を監視するミニポート ドライバーは、呼び出すことによってよりも細かい単位の間隔の経過と共に変化[ **VideoPortStallExecution**](https://msdn.microsoft.com/library/windows/hardware/ff570368). *HwVidTimer*からとして発生している場合は、他のシステム操作を妨げませんも**VideoPortStallExecution**は。

たとえば、VGA 機能をエミュレートするアダプターのミニポート ドライバーがある、 *HwVidTimer*ドライバーは、VGA スタイルのグラフィックスをエミュレートできるようにそのアダプターの"VGA"の状態を監視する関数は定期的に登録します。

呼び出しの後に[ **VideoPortStartTimer**](https://msdn.microsoft.com/library/windows/hardware/ff570370)、ビデオ ポート ドライバー呼び出し*HwVidTimer*ビデオのミニポート ドライバー呼び出されるまで毎秒 1 回[ **VideoPortStopTimer**](https://msdn.microsoft.com/library/windows/hardware/ff570371)します。 ビデオのミニポート ドライバーが有効にしてへの呼び出しを無効にする、 *HwVidTimer*繰り返し関数。

なお、 *HwVidTimer*関数自体への呼び出しを無効にできません**VideoPortStopTimer**します。 別のビデオのミニポート ドライバー関数は、有効化、またはへの呼び出しの無効化を制御する必要があります、 *HwVidTimer*関数の使用により**VideoPortStartTimer**と**VideoPortStopTimer**.

 

 






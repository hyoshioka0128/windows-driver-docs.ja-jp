---
title: 子デバイスの検出
description: 子デバイスの検出
ms.assetid: 36c0c4ef-7810-4e8a-b349-0b7c1f8c2f0c
keywords:
- ビデオミニポートドライバー WDK Windows 2000、子デバイス
- 子デバイス WDK ビデオミニポート、検出
- 子デバイスの検出 WDK ビデオミニポート
- HwVidGetVideoChildDescriptor
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 259ac6757cd990a8bbb9233a63908db74ed6ecf3
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72839753"
---
# <a name="detecting-child-devices"></a>子デバイスの検出


## <span id="ddk_detecting_child_devices_gg"></span><span id="DDK_DETECTING_CHILD_DEVICES_GG"></span>


プラグアンドプレイ manager がグラフィックスアダプターの子デバイスを検出できるようにするには、ミニポートドライバーで[*HwVidGetVideoChildDescriptor*](https://docs.microsoft.com/windows-hardware/drivers/ddi/video/nc-video-pvideo_hw_get_child_descriptor)を実装する必要があります。

既定では、親デバイスが起動するまで[*HwVidGetVideoChildDescriptor*](https://docs.microsoft.com/windows-hardware/drivers/ddi/video/nc-video-pvideo_hw_get_child_descriptor)を呼び出すことはできません。つまり、 [*HwVidFindAdapter*](https://docs.microsoft.com/windows-hardware/drivers/ddi/video/nc-video-pvideo_hw_find_adapter)が完了するまで*HwVidGetVideoChildDescriptor*を呼び出すことはできません。 この既定値をオーバーライドして、子列挙をいつでも実行できるようにするには、 [**VIDEO\_HW\_初期化\_データ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/video/ns-video-_video_hw_initialization_data)の**Allowの列挙型**のメンバーを**TRUE**に設定します。

一部のデバイスでは、新しいハードウェアがシステムに接続されたとき、または既存のハードウェアがシステムから切断されたときに、割り込みが発生します。 このような割り込みを処理するには、ミニポートドライバーで次の操作を行う必要があります。

-   [**VideoPortEnumerateChildren**](https://docs.microsoft.com/windows-hardware/drivers/ddi/video/nf-video-videoportenumeratechildren)を呼び出す DPC ([**HwVidDpcRoutine**](https://docs.microsoft.com/windows-hardware/drivers/ddi/video/nc-video-pminiport_dpc_routine)) を実装します。

-   デバイスの割り込みが発生したときに DPC をキューに入れ、 [**VideoPortQueueDpc**](https://docs.microsoft.com/windows-hardware/drivers/ddi/video/nf-video-videoportqueuedpc)を呼び出す割り込みハンドラー ([*HwVidInterrupt*](https://docs.microsoft.com/windows-hardware/drivers/ddi/video/nc-video-pvideo_hw_interrupt)) を実装します。

[**VideoPortEnumerateChildren**](https://docs.microsoft.com/windows-hardware/drivers/ddi/video/nf-video-videoportenumeratechildren)は、各親デバイスの子に対してミニポートドライバーの[*HwVidGetVideoChildDescriptor*](https://docs.microsoft.com/windows-hardware/drivers/ddi/video/nc-video-pvideo_hw_get_child_descriptor)関数が呼び出されるようにすることで、アダプターの子デバイスの reenumeration を強制的に実行します。 プラグアンドプレイマネージャーは、それに応じて親デバイスとその子との間のリレーションシップを更新します。

 

 






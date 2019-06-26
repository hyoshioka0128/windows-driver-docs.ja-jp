---
title: 子デバイスの検出
description: 子デバイスの検出
ms.assetid: 36c0c4ef-7810-4e8a-b349-0b7c1f8c2f0c
keywords:
- ビデオのミニポート ドライバー WDK Windows 2000 では、子デバイス
- 子デバイス WDK ビデオ ミニポート、検出します。
- 子デバイス WDK のビデオのミニポートの検出
- HwVidGetVideoChildDescriptor
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: be2ea7678a3883d317618a2ee416da83f6a93f0b
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67384879"
---
# <a name="detecting-child-devices"></a>子デバイスの検出


## <span id="ddk_detecting_child_devices_gg"></span><span id="DDK_DETECTING_CHILD_DEVICES_GG"></span>


実装する必要があります[ *HwVidGetVideoChildDescriptor* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/video/nc-video-pvideo_hw_get_child_descriptor)グラフィックス アダプターの子デバイスを検出することができる、プラグ アンド プレイ マネージャーは、ミニポート ドライバー。

既定では、 [ *HwVidGetVideoChildDescriptor* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/video/nc-video-pvideo_hw_get_child_descriptor)まで、親デバイスが開始されている後に呼び出すことができません、 *HwVidGetVideoChildDescriptor*呼び出すことができませんまで後[ *HwVidFindAdapter* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/video/nc-video-pvideo_hw_find_adapter)が完了します。 設定することができます、いつでも発生する子列挙できますつまり、この既定をオーバーライドする、 **AllowEarlyEnumeration**のメンバー [**ビデオ\_HW\_の初期化。\_データ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/video/ns-video-_video_hw_initialization_data)に**TRUE**します。

一部のデバイスは、システムまたは既存のハードウェアが、システムから切断されている場合、新しいハードウェアが接続されているときに、割り込みを生成します。 このような割り込みを処理するために、ミニポート ドライバーは、次の操作を行う必要があります。

-   DPC の実装 ([**HwVidDpcRoutine**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/video/nc-video-pminiport_dpc_routine)) を呼び出す[ **VideoPortEnumerateChildren**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/video/nf-video-videoportenumeratechildren)します。

-   割り込みハンドラーの実装 ([*HwVidInterrupt*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/video/nc-video-pvideo_hw_interrupt)) を呼び出す[ **VideoPortQueueDpc** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/video/nf-video-videoportqueuedpc)ときに、割り込み、DPC キューに入れ、デバイスに発生します。

[**VideoPortEnumerateChildren** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/video/nf-video-videoportenumeratechildren)強制的によって、ミニポート ドライバーのアダプターの子のデバイスの再列挙[ *HwVidGetVideoChildDescriptor* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/video/nc-video-pvideo_hw_get_child_descriptor)関数親デバイスの子のそれぞれに対して呼び出されます。 プラグ アンド プレイ マネージャーは、親デバイスとその子間のリレーションシップを適宜更新されます。

 

 






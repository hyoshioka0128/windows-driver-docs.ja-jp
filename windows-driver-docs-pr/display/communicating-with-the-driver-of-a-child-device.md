---
title: 子デバイスのドライバーとの通信
description: 子デバイスのドライバーとの通信
ms.assetid: f1311941-bfba-44a4-867c-95fcbef19510
keywords:
- ビデオのミニポート ドライバー WDK Windows 2000 では、子デバイス
- 子デバイス WDK ビデオ ミニポート ドライバーとの通信
- HwVidQueryInterface
- IRP_MN_QUERY_INTERFACE
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: dc1d01f6495a3b87998805b3dacac26354c290c7
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67370656"
---
# <a name="communicating-with-the-driver-of-a-child-device"></a>子デバイスのドライバーとの通信


## <span id="ddk_communicating_with_the_driver_of_a_child_device_gg"></span><span id="DDK_COMMUNICATING_WITH_THE_DRIVER_OF_A_CHILD_DEVICE_GG"></span>


ビデオのミニポート ドライバーと子デバイスのドライバーでは、インターフェイスを介して親ミニポート ドライバー、ハードウェアと通信するために、子ドライバーを相互に定義できます。 子のドライバーは、送信することによってこのインターフェイスを取得、 [ **IRP\_MN\_クエリ\_インターフェイス**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-query-interface)親ミニポート ドライバーのビデオ ポート ドライバーに要求します。 このような要求を受信するには、ビデオ ポート ドライバーに呼び出し、ミニポート ドライバーの[ *HwVidQueryInterface* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/video/nc-video-pvideo_hw_query_interface)関数は、定義されていて、ミニポート ドライバー インターフェイスへのポインターを返します。 によって公開される関数を使用して、ミニポート ドライバーに子デバイスのドライバーを呼び出して*HwVidQueryInterface*いつでもできます。

ミニポート ドライバーが実装していない場合[ *HwVidQueryInterface* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/video/nc-video-pvideo_hw_query_interface)かに、ミニポート ドライバーのデバイスの親が失敗した呼び出し、ビデオ ポート ドライバーを渡す要求。 子ドライバーは IRP を送信する場合\_MN\_クエリ\_を別のインターフェイス、ミニポート ドライバーおよびその他のドライバーの子の子が実装していない*HwVidQueryInterface*ビデオ、呼び出しが失敗またはポートのドライバーでは、エラーを返します。

ミニポート ドライバーですべての関数によって公開される自身へのアクセスを同期する必要がある子ドライバー、ビデオ ポート ドライバーの知識がなくても、ミニポート ドライバーに呼び出すには、ため[ *HwVidQueryInterface* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/video/nc-video-pvideo_hw_query_interface). これは呼び出すことによって、 [ **VideoPortAcquireDeviceLock** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/video/nf-video-videoportacquiredevicelock)と[ **VideoPortReleaseDeviceLock** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/video/nf-video-videoportreleasedevicelock)を取得し、ビデオ ポートを解放するにはドライバーで維持されるデバイスをロック、それぞれします。

によって列挙子デバイス[ *HwVidGetVideoChildDescriptor*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/video/nc-video-pvideo_hw_get_child_descriptor)します。

 

 






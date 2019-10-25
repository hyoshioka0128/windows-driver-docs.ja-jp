---
title: 子デバイスのドライバーとの通信
description: 子デバイスのドライバーとの通信
ms.assetid: f1311941-bfba-44a4-867c-95fcbef19510
keywords:
- ビデオミニポートドライバー WDK Windows 2000、子デバイス
- 子デバイス WDK ビデオミニポート、ドライバーとの通信
- HwVidQueryInterface
- IRP_MN_QUERY_INTERFACE
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 54e988f64a4f6f23eecbef1a67c4420c5a3968c2
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72839050"
---
# <a name="communicating-with-the-driver-of-a-child-device"></a>子デバイスのドライバーとの通信


## <span id="ddk_communicating_with_the_driver_of_a_child_device_gg"></span><span id="DDK_COMMUNICATING_WITH_THE_DRIVER_OF_A_CHILD_DEVICE_GG"></span>


ビデオミニポートドライバーと子デバイスのドライバーは、子ドライバーが親ミニポートドライバーを通じてハードウェアと通信できるようにするインターフェイスを相互に定義できます。 子ドライバーは、親ミニポートドライバーのビデオポートドライバーに、 [**IRP\_\_クエリ\_インターフェイス**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-query-interface)要求を送信することによって、このインターフェイスを取得します。 このような要求を受信すると、ビデオポートドライバーはミニポートドライバーの[*HwVidQueryInterface*](https://docs.microsoft.com/windows-hardware/drivers/ddi/video/nc-video-pvideo_hw_query_interface)関数を呼び出します。この関数が定義されている場合は、ミニポートドライバーがインターフェイスへのポインターを返します。 子デバイスのドライバーは、 *HwVidQueryInterface*によって公開されている関数を介して、いつでもミニポートドライバーを呼び出すことができます。

ミニポートドライバーで[*HwVidQueryInterface*](https://docs.microsoft.com/windows-hardware/drivers/ddi/video/nc-video-pvideo_hw_query_interface)が実装されていない場合、または呼び出しに失敗した場合は、ビデオポートドライバーがミニポートドライバーのデバイスの親に要求を渡します。 子ドライバーが\_クエリ\_インターフェイスをポートの別の子に\_送信し、他の子ドライバーが*HwVidQueryInterface*を実装していないか、または呼び出しに失敗した場合、ビデオポートドライバーはエラーを返します。

子ドライバーはビデオポートドライバーの知識がなくてもミニポートドライバーを呼び出すことができるため、ミニポートドライバーは、 [*HwVidQueryInterface*](https://docs.microsoft.com/windows-hardware/drivers/ddi/video/nc-video-pvideo_hw_query_interface)によって公開されているすべての関数で自身へのアクセスを同期する必要があります。 これを行うには、 [**VideoPortAcquireDeviceLock**](https://docs.microsoft.com/windows-hardware/drivers/ddi/video/nf-video-videoportacquiredevicelock)と[**Videoportreleasedevicelock**](https://docs.microsoft.com/windows-hardware/drivers/ddi/video/nf-video-videoportreleasedevicelock)を呼び出して、それぞれビデオポートドライバーで保持されているデバイスロックを取得し、解放します。

子デバイスは、 [*HwVidGetVideoChildDescriptor*](https://docs.microsoft.com/windows-hardware/drivers/ddi/video/nc-video-pvideo_hw_get_child_descriptor)によって列挙されます。

 

 






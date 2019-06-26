---
title: デバイスがスリープ状態のときの I/O 要求のキュー
description: デバイスがスリープ状態のときの I/O 要求のキュー
ms.assetid: 8cc0cea0-e5be-4705-ad4d-13a44d536469
keywords:
- I/O WDK 電源管理
- キューの I/O 要求
- スリープの電源管理の WDK カーネル
- WDK のスリープ状態のデバイスの電源管理
- キューの Irp
- 電源 Irp WDK カーネル、I/O 要求のキュー
- 動作状態は、WDK の電源管理を返します
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 680fdd04c194d1466379b853ef6e7f9f456aae86
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67378751"
---
# <a name="queuing-io-requests-while-a-device-is-sleeping"></a>デバイスがスリープ状態のときの I/O 要求のキュー





デバイスがスリープ状態の間は、そのドライバーは、デバイスに送られるすべての I/O 要求をキューする必要があります。 [ **IoAllocateWorkItem**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ioallocateworkitem)、 [ **IoQueueWorkItem**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ioqueueworkitem)、および[ **IoFreeWorkItem**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iofreeworkitem)サポート ルーチンが遅延処理キュー Irp の 1 つの方法を提供します。 例については、キューのメカニズムでの PnP ドライバーの説明を参照してください。[を保持している受信 Irp ときに、デバイスが一時停止](holding-incoming-irps-when-a-device-is-paused.md)します。

デバイスが作業 (D0) 状態になっている場合にのみ、ドライバーはそのデバイスにアクセスできます。 デバイスがスリープ状態にしている場合、ドライバーは任意のデバイス登録を修正できません。デバイスが稼働状態に返される最初する必要があります。

 

 





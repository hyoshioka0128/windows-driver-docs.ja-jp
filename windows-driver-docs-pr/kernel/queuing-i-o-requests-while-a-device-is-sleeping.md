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
ms.openlocfilehash: 7e8235955f0cfe59c2fcba47f5bb5dc65f4ef289
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63353602"
---
# <a name="queuing-io-requests-while-a-device-is-sleeping"></a>デバイスがスリープ状態のときの I/O 要求のキュー





デバイスがスリープ状態の間は、そのドライバーは、デバイスに送られるすべての I/O 要求をキューする必要があります。 [ **IoAllocateWorkItem**](https://msdn.microsoft.com/library/windows/hardware/ff548276)、 [ **IoQueueWorkItem**](https://msdn.microsoft.com/library/windows/hardware/ff549466)、および[ **IoFreeWorkItem**](https://msdn.microsoft.com/library/windows/hardware/ff549133)サポート ルーチンが遅延処理キュー Irp の 1 つの方法を提供します。 例については、キューのメカニズムでの PnP ドライバーの説明を参照してください。[を保持している受信 Irp ときに、デバイスが一時停止](holding-incoming-irps-when-a-device-is-paused.md)します。

デバイスが作業 (D0) 状態になっている場合にのみ、ドライバーはそのデバイスにアクセスできます。 デバイスがスリープ状態にしている場合、ドライバーは任意のデバイス登録を修正できません。デバイスが稼働状態に返される最初する必要があります。

 

 





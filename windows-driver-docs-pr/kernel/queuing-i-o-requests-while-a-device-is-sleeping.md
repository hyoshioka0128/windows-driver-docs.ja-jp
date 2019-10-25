---
title: デバイスがスリープ状態のときの I/O 要求のキュー
description: デバイスがスリープ状態のときの I/O 要求のキュー
ms.assetid: 8cc0cea0-e5be-4705-ad4d-13a44d536469
keywords:
- I/o WDK 電源管理
- i/o 要求をキューに置いています
- スリープ電源管理 WDK カーネル
- スリープ状態のデバイス WDK 電源管理
- キューの Irp
- 電源 Irp WDK カーネル、キュー i/o 要求
- 動作状態は WDK 電源管理を返します
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4ea6a59c99086bfffaa5d6d87bd3d3f0de70f3e3
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838478"
---
# <a name="queuing-io-requests-while-a-device-is-sleeping"></a>デバイスがスリープ状態のときの I/O 要求のキュー





デバイスがスリープ状態の間は、デバイスに送信された i/o 要求をそのドライバーがキューに置いている必要があります。 [**Ioallocateworkitem**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioallocateworkitem)、 [**ioqueueworkitem**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioqueueworkitem)、および[**IoFreeWorkItem**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iofreeworkitem) support ルーチンは、遅延処理のための irp をキューに1つの方法で提供します。 例については、「[デバイスが一時停止しているときに受信 irp を保持する](holding-incoming-irps-when-a-device-is-paused.md)」で説明されているキューメカニズムに関するページを参照してください。

デバイスが動作中 (D0) 状態にある場合にのみ、ドライバーはそのデバイスにアクセスできます。 デバイスがスリープ状態の場合、ドライバーはデバイスの登録に触れることができません。まず、デバイスを動作状態に戻す必要があります。

 

 





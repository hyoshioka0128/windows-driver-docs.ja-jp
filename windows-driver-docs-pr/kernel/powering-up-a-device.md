---
title: デバイスの電源投入
description: デバイスの電源投入
ms.assetid: 115cc904-922d-447e-b221-cb3e489dd08d
keywords:
- I/o WDK 電源管理
- デバイスの電源 ups WDK カーネル
- デバイスの電源をオンにする (WDK カーネル)
- IRP_MN_SET_POWER
- 動作状態は WDK 電源管理を返します
- デバイスをオンにする WDK 電源管理
- 自動電源 ups WDK カーネル
- power WDK カーネル
- Irp WDK 電源管理
- スタートアップ電源管理 WDK カーネル
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3d2b154c29ce0069de9640d1148727342f457c77
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72827631"
---
# <a name="powering-up-a-device"></a>デバイスの電源投入





バスドライバーは、その子デバイスの1つに対して\_デバイスの要求を[**開始\_\_** ](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-start-device) 、デバイスの電源を入れ、 [**PoSetPowerState**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-posetpowerstate)を呼び出して、デバイスの電源状態を電源マネージャーに報告する必要があります。 デバイスの電源をオンにするのは、デバイスの起動時の暗黙的な部分です。 デバイスの電源ポリシー所有者は、 **PowerDeviceD0**の[**電源要求\_\_設定**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-set-power)された irp\_を送信しません。そのため、ドライバーは起動時にこれらの irp を受信しないようにする必要があります。

電力を節約するためにデバイスの電源がオフになっている場合は、i/o 要求が到着したときにそのデバイスの電源を入れる必要があります。 この場合、デバイスの電源ポリシーの所有者は、デバイスを動作状態に戻すために **\_電源\_設定**された IRP\_を送信する必要があります。 IRP が完了すると、デバイスのドライバーは、i/o を停止し、キューからの要求の処理を開始します。

 

 





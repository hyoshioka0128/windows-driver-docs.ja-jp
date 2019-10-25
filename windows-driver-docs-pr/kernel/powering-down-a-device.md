---
title: デバイスの電源切断
description: デバイスの電源切断
ms.assetid: d2525e15-9590-4fc0-955c-ca3540c13375
keywords:
- デバイスの電源ダウン WDK カーネル
- デバイスの電源切断 (WDK カーネル)
- IRP_MN_REMOVE_DEVICE
- デバイスをオフにする WDK 電源管理
- 自動パワーダウン WDK カーネル
- 電源管理のシャットダウン WDK カーネル
- オフパワー WDK カーネル
- Irp WDK 電源管理
- 予期しない削除 WDK の電源管理
- デバイス削除の WDK 電源管理
- デバイスの削除
- I/o WDK 電源管理
- 予期しないデバイス削除の WDK 電源管理
- アイドル検出 WDK 電源管理
- power WDK カーネルを節約する
- I/o 要求パケットの WDK 電源管理
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6b8fb0eb5ec4ce7e4db0c2e8d619e0fdea022077
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838500"
---
# <a name="powering-down-a-device"></a>デバイスの電源切断





デバイスでウェイクアップが有効になっていない限り、システムのシャットダウン時にドライバーの電源がオフになります。 デバイスは、削除または突然削除したときに常に電源をオフにする必要があります。

デバイスが削除されると、プラグアンドプレイ manager は、デバイススタックに\_デバイスの要求を[**削除\_、IRP\_** ](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-remove-device)送信します。 この IRP に応答して、デバイスのドライバーによってデバイスの電源が切れていることを確認する必要があります。 デバイスの電源を切ることは、削除処理の暗黙的な部分です。デバイスの電源ポリシーの所有者は、 **PowerDeviceD3**の[ **\_電力\_設定**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-set-power)された IRP\_送信する必要はありません。

ドライバーが IRP\_処理し、 **\_デバイスの要求\_削除**すると、保留中の i/o が完了するまで待機し、必要な削除処理を実行し、 [**PoSetPowerState**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-posetpowerstate)を呼び出して、デバイスが状態 D3 であることを電源マネージャーに通知します。このデバイス用に作成したデバイスオブジェクトを削除します。 通常、バスドライバーはデバイスの電源をオフにします。

デバイスが Windows 2000 以降のオペレーティングシステムから予期せずに削除された場合、プラグアンドプレイマネージャーは、\_削除要求を、対応するデバイススタックの一番上にある[ **\_\_IRP**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-surprise-removal)を送信します。 この IRP への応答として、デバイスのドライバーは、「 [IRP\_\_\_の処理](handling-an-irp-mn-surprise-removal-request.md)」で説明されているように、予期しない削除処理を実行する必要があります。

システムのシャットダウン時に、電源管理者は、システムの電源状態 (S4 または S5) の **\_電源\_設定**された IRP\_を送信します。 デバイスの電源ポリシー所有者は、この IRP を受信したときに、 **PowerDeviceD3**に対して **\_\_設定**された irp\_を送信する必要があります。これにより、低いドライバーが作業を完了し、デバイスの電源を切ることができるようになります。

ドライバーは必要に応じて、デバイスのアイドル状態の検出を実行できます。また、電源マネージャーがアイドル状態の検出を実行するように要求することもできます。これにより、使用されていないときにデバイスの電源を切ることができます。 詳細については、「[アイドル状態のデバイスの検出](detecting-an-idle-device.md)」を参照してください。

 

 





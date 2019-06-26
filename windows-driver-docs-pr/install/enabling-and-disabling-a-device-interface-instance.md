---
title: デバイス インターフェイス インスタンスの有効化と無効化
description: デバイス インターフェイス インスタンスの有効化と無効化
ms.assetid: 4e3341c2-ba95-458e-8d92-a35545a773e0
keywords:
- インターフェイス クラス WDK デバイスのインストール
- デバイス インターフェイスのインスタンスを無効にします。
- IoSetDeviceInterfaceState
- デバイスのインターフェイス クラス WDK デバイスのインストール
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 60909ce1384cd97cec34c793634d2b0c6f43be1a
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67374992"
---
# <a name="enabling-and-disabling-a-device-interface-instance"></a>デバイス インターフェイス インスタンスの有効化と無効化





デバイスを正常に起動するには後のインターフェイスに登録されているドライバーを呼び出して[ **IoSetDeviceInterfaceState** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iosetdeviceinterfacestate)インターフェイス インスタンスを有効にします。 ドライバーによって返されるシンボリック リンクの名前を渡します[ **IoRegisterDeviceInterface** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ioregisterdeviceinterface)ブール値と共に**TRUE**インターフェイス インスタンスを有効にします。

ドライバーでは、そのデバイスが正常に開始する場合、に呼び出す必要がありますこのルーチン、プラグ アンド プレイ (PnP) を処理中にマネージャーの[ **IRP_MN_START_DEVICE** ](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-start-device)要求。

IRP_MN_START_DEVICE 要求が完了すると、PnP マネージャーは、それらを要求したカーネル モードまたはユーザー モード コンポーネントをデバイス インターフェイスの到着の通知を発行します。 詳細については、次を参照してください。[デバイス インターフェイスの変更通知を登録する](https://docs.microsoft.com/windows-hardware/drivers/kernel/registering-for-device-interface-change-notification)します。

ドライバーを呼び出し、デバイス インターフェイスのインスタンスを無効にする[ **IoSetDeviceInterfaceState**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iosetdeviceinterfacestate)を渡して、 *SymbolicLinkName*によって返される[ **IoRegisterDeviceInterface** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ioregisterdeviceinterface)と**FALSE**の値として*を有効にする*します。

処理する場合、ドライバーがデバイスのインターフェイスを無効にする必要があります、 [ **IRP_MN_SURPRISE_REMOVAL** ](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-surprise-removal)または[ **IRP_MN_REMOVE_DEVICE** ](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-remove-device)デバイスの要求。 Irp のこれらの削除を処理する場合、ドライバーによるデバイスのインターフェイスは無効する場合、にする必要があります、その後しようとは、デバイスを削除するとき、PnP マネージャーが、インターフェイスを無効になります。

デバイスが停止したときにドライバーが、インターフェイスを無効 ([**IRP_MN_STOP_DEVICE**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-stop-device)); 代わりに、有効な任意のデバイス インターフェイスのままにする必要がありますが、までキューの I/O 要求を受け取る別[ **IRP_MN_START_DEVICE** ](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-start-device)要求。 同様に、ドライバー、デバイスがスリープ状態で配置時にそのインターフェイスを無効する必要があります。 デバイスのスリープ状態になるまで、I/O 要求をキューにする必要があります。 詳細については、次を参照してください。[サポート デバイスがあるウェイク アップ機能](https://docs.microsoft.com/windows-hardware/drivers/kernel/supporting-devices-that-have-wake-up-capabilities)します。

 

 






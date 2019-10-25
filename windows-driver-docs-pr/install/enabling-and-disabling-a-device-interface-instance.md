---
title: デバイスインターフェイスインスタンスの有効化と無効化
description: デバイスインターフェイスインスタンスの有効化と無効化
ms.assetid: 4e3341c2-ba95-458e-8d92-a35545a773e0
keywords:
- インターフェイスクラス WDK デバイスのインストール
- デバイスインターフェイスインスタンスの無効化
- IoSetDeviceInterfaceState
- デバイスインターフェイスクラス WDK デバイスのインストール
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 098ee2e4eb58e90eff81f567acc1fcce30003b6b
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72840639"
---
# <a name="enabling-and-disabling-a-device-interface-instance"></a>デバイスインターフェイスインスタンスの有効化と無効化





デバイスが正常に起動されると、インターフェイスを登録したドライバーは[**Iosetdeviceinterfacestate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iosetdeviceinterfacestate)を呼び出して、インターフェイスインスタンスを有効にします。 ドライバーは、 [**IoRegisterDeviceInterface**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioregisterdeviceinterface)によって返されたシンボリックリンク名とブール値**TRUE**を渡して、インターフェイスインスタンスを有効にします。

ドライバーがデバイスを正常に起動できる場合は、プラグアンドプレイ (PnP) マネージャーの[**IRP_MN_START_DEVICE**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-start-device)要求を処理するときに、このルーチンを呼び出す必要があります。

IRP_MN_START_DEVICE 要求が完了すると、PnP マネージャーは、要求されたカーネルモードまたはユーザーモードコンポーネントにデバイスインターフェイスの到着通知を発行します。 詳細については、「[デバイスインターフェイスの変更通知の登録](https://docs.microsoft.com/windows-hardware/drivers/kernel/registering-for-device-interface-change-notification)」を参照してください。

デバイスインターフェイスインスタンスを無効にするには、ドライバーは[**Iosetdeviceinterfacestate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iosetdeviceinterfacestate)を呼び出し、 [**IoRegisterDeviceInterface**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioregisterdeviceinterface)によって返された*SymbolicLinkName*と**FALSE** *を渡します。*

ドライバーは、デバイスの[**IRP_MN_SURPRISE_REMOVAL**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-surprise-removal)または[**IRP_MN_REMOVE_DEVICE**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-remove-device)要求を処理するときに、デバイスのインターフェイスを無効にする必要があります。 ドライバーがこれらの削除 Irp を処理するときにデバイスのインターフェイスを無効にしない場合、PnP マネージャーはデバイスを削除するときに、そのインターフェイスを無効にするため、後でこの操作を実行しないようにする必要があります。

ドライバーは、デバイスが停止したときにインターフェイスを無効にしないようにする必要があります ([**IRP_MN_STOP_DEVICE**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-stop-device))。代わりに、デバイスインターフェイスが有効になっていて、別の[**IRP_MN_START_DEVICE**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-start-device)要求を受信するまで、i/o 要求をキューに入れておく必要があります。 同様に、デバイスがスリープ状態になっている場合、ドライバーはそのインターフェイスを無効にしないでください。 デバイスがウェイクアップするまで、i/o 要求をキューに入れます。 詳細については、「[ウェイクアップ機能を搭載したデバイスのサポート](https://docs.microsoft.com/windows-hardware/drivers/kernel/supporting-devices-that-have-wake-up-capabilities)」を参照してください。

 

 






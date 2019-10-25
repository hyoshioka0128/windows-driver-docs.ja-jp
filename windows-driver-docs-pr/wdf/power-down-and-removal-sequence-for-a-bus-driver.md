---
title: バス ドライバーの電源切断および取り外しシーケンス
description: バス ドライバーの電源切断および取り外しシーケンス
ms.assetid: 71397945-D9DB-43E2-AE06-548684F72B63
ms.date: 03/28/2019
ms.localizationpriority: medium
ms.openlocfilehash: d1ae0aaaacd0360bfa33f5526575943605cc43b6
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842249"
---
# <a name="power-down-and-removal-sequence-for-a-bus-driver"></a>バス ドライバーの電源切断および取り外しシーケンス


次の図は、バスに接続されているデバイスの電源をオンにして削除するときに、フレームワークが KMDF バスドライバーのイベントコールバック関数を呼び出す順序を示しています。 シーケンスは、動作中の電源状態 (D0) にある操作デバイスを使用して、図の上部から開始します。

![バスドライバーの電源ダウンと削除シーケンス](images/pdo-powerdown.png)

フレームワークは、デバイスがシステムから物理的に削除されるまで PDO を削除しません。 たとえば、ユーザーがデバイスマネージャーでデバイスを無効にした場合、またはハードウェアの安全な取り外しユーティリティでデバイスを停止しても、物理的にはデバイスを削除しない場合、フレームワークは PDO を保持します。 デバイスを再度有効にした場合、フレームワークは同じ PDO を使用し、「[物理デバイスオブジェクトの電源投入シーケンス](power-up-sequence-for-a-bus-driver.md)」に示されているように、 [*Evtdevicepreparehardware*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_prepare_hardware)コールバックを呼び出すことによって起動シーケンスを開始します。

**注**: 通常、フレームワークは、ドライバーが列挙するすべての子デバイスに対して[*EvtDeviceReleaseHardware*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_release_hardware)関数を呼び出した後、バスドライバーの[*EvtDeviceReleaseHardware*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_release_hardware)コールバック関数を呼び出します。  親がデバイスの電源アップまたは停電の障害を検出した場合、フレームワークは、すべての子デバイスの[*EvtDeviceReleaseHardware*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_release_hardware)関数を呼び出す前に、ドライバーの[*EvtDeviceReleaseHardware*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_release_hardware)を呼び出す可能性があります。  [WdfDeviceInitSetReleaseHardwareOrderOnFailure](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdeviceinitsetreleasehardwareorderonfailure)を呼び出して、すべての子デバイスが削除された後にのみ、フレームワークがバスドライバーの[*EvtDeviceReleaseHardware*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_release_hardware)コールバックを呼び出すようにすることを検討してください。



 






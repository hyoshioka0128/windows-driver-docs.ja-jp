---
title: バス ドライバーの電源切断および取り外しシーケンス
description: バス ドライバーの電源切断および取り外しシーケンス
ms.assetid: 71397945-D9DB-43E2-AE06-548684F72B63
ms.date: 03/28/2019
ms.localizationpriority: medium
ms.openlocfilehash: 078a45682635d4670782f75f57fca1b017388f6f
ms.sourcegitcommit: 282e17efc5ff5bc4541e277d67567d37aa2d957b
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/28/2019
ms.locfileid: "58563983"
---
# <a name="power-down-and-removal-sequence-for-a-bus-driver"></a>バス ドライバーの電源切断および取り外しシーケンス


次の図は、バスに接続されているデバイスを削除して電源をオフのときに、フレームワーク KMDF バス ドライバーのイベントのコールバック関数を呼び出す順序を示します。 シーケンスは、図の上部にある作業の電源の状態 (D0) では、運用のデバイスで始まります。

![バス ドライバーの電源と削除の順序](images/pdo-powerdown.png)

フレームワークでは、デバイスは、システムから物理的に削除されるまで、PDO は削除されません。 たとえば、ユーザーは、デバイス マネージャーでデバイスを無効にします。 または、ハードウェアの安全なユーティリティで停止しますが、デバイスを物理的に削除されません、フレームワークは、PDO を保持します。 デバイスが再度有効に後で場合、フレームワークは同じ PDO を使用し、呼び出すことによって、スタートアップ シーケンスを開始、 [ *EvtDevicePrepareHardware* ](https://msdn.microsoft.com/library/windows/hardware/ff540880)コールバックのように[の電源投入シーケンス物理デバイス オブジェクト](power-up-sequence-for-a-bus-driver.md)します。

**注意**:通常、フレームワークがバス ドライバーの[ *EvtDeviceReleaseHardware* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nc-wdfdevice-evt_wdf_device_release_hardware)コールバック関数を呼び出した後、 [ *EvtDeviceReleaseHardware*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nc-wdfdevice-evt_wdf_device_release_hardware)すべての子デバイス ドライバーを列挙する関数。  デバイスの電源投入または電源の障害が発生して、親が発生した場合、フレームワークは、ドライバーを呼び出すことができます[ *EvtDeviceReleaseHardware* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nc-wdfdevice-evt_wdf_device_release_hardware)それが呼び出される前に、 [ *EvtDeviceReleaseHardware* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nc-wdfdevice-evt_wdf_device_release_hardware)関数のすべての子デバイス。  呼び出し元を検討してください[WdfDeviceInitSetReleaseHardwareOrderOnFailure](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nf-wdfdevice-wdfdeviceinitsetreleasehardwareorderonfailure)をフレームワークが呼び出す、バス ドライバーのように[ *EvtDeviceReleaseHardware* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nc-wdfdevice-evt_wdf_device_release_hardware)コールバック。すべての子デバイスが削除されました後でのみ。



 






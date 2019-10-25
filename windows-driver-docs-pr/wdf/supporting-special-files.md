---
title: 特別なファイルのサポート
description: 特別なファイルのサポート
ms.assetid: 350e715f-be36-4999-99a2-6175d9763b3f
keywords:
- 特別なファイル WDK KMDF
- ページングファイル WDK KMDF
- ダンプファイル WDK KMDF
- 休止状態ファイル WDK KMDF
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4da17da91ada5ea6a7053dbefa23e9d3860616f9
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72831694"
---
# <a name="supporting-special-files"></a>特別なファイルのサポート


*特別なファイル*としては、ページングファイル、ダンプファイル、休止状態ファイルなどがあります。 ドライバーのターゲットデバイスが、これらのファイルに使用される可能性のある記憶装置である場合、ドライバーは次の操作を行う必要があります。

-   [**WdfDeviceSetSpecialFileSupport**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdevicesetspecialfilesupport)を呼び出して、特別なファイルの種類ごとにサポートを有効または無効にします。 (各ドライバーの特別なファイルのサポートは、既定では無効になっています。)

    [子デバイスを列挙](enumerating-the-devices-on-a-bus.md)するバスドライバーも、特殊なファイルをサポートできる各子デバイスの[**WdfDeviceSetSpecialFileSupport**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdevicesetspecialfilesupport)を呼び出す必要があります。

-   特別なファイルをサポートするときに、あるデバイスが別のデバイスに依存している場合は、 [**WdfDeviceAddDependentUsageDeviceObject**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdeviceadddependentusagedeviceobject)を呼び出します。

-   必要に応じて、 [*EvtDeviceUsageNotification*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_usage_notification)または (kmdf 1.11 から開始) [*EvtDeviceUsageNotificationEx*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_usage_notification_ex)コールバック関数を指定します。これにより、特別なファイルが作成または削除されたときにドライバーに通知されます。

ドライバーがデバイスの[**WdfDeviceSetSpecialFileSupport**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdevicesetspecialfilesupport)を呼び出し、デバイスで特別なファイルが開いている場合、このフレームワークでは、PnP マネージャーがデバイスを削除または停止することを許可していません。

ドライバーが[**WdfDeviceAddDependentUsageDeviceObject**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdeviceadddependentusagedeviceobject)を呼び出した後、 [**WdfDeviceRemoveDependentUsageDeviceObject**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdeviceremovedependentusagedeviceobject)を呼び出して、別のデバイスに対するデバイスの依存関係を削除できます。

 

 






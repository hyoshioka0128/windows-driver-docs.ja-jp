---
title: 特別なファイルのサポート
description: 特別なファイルのサポート
ms.assetid: 350e715f-be36-4999-99a2-6175d9763b3f
keywords:
- WDK KMDF の特殊なファイル
- WDK KMDF のページング ファイル
- ダンプ ファイル WDK KMDF
- 休止状態ファイル WDK KMDF
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 30c1be82ea7ff5bdf2cf6d11df75bf9328ec3e9d
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67368048"
---
# <a name="supporting-special-files"></a>特別なファイルのサポート


*特別なファイル*ページング ファイル、ダンプ ファイル、および休止状態ファイルが含まれます。 ドライバーのターゲット デバイスがこれらのファイル システムを使用する記憶域デバイスの場合は、ドライバー、次の操作する必要があります。

-   呼び出す[ **WdfDeviceSetSpecialFileSupport** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nf-wdfdevice-wdfdevicesetspecialfilesupport)を有効にするまたは特殊なファイルの種類ごとにサポートを無効にします。 (特別なファイルの各ドライバーのサポートは既定で無効です。)

    バス ドライバーを[列挙子デバイス](enumerating-the-devices-on-a-bus.md)も呼び出す必要があります[ **WdfDeviceSetSpecialFileSupport** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nf-wdfdevice-wdfdevicesetspecialfilesupport)特別なファイルをサポートできる子デバイスごとにします。

-   呼び出す[ **WdfDeviceAddDependentUsageDeviceObject**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nf-wdfdevice-wdfdeviceadddependentusagedeviceobject)、特別なファイルをサポートするときに、1 つのデバイスを別のデバイスに依存する場合。

-   必要に応じて指定、 [ *EvtDeviceUsageNotification* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nc-wdfdevice-evt_wdf_device_usage_notification) (KMDF 1.11 以降) または[ *EvtDeviceUsageNotificationEx* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nc-wdfdevice-evt_wdf_device_usage_notification_ex)コールバック関数の場合、ドライバーは特殊なファイルが作成または削除されたときに通知します。

ドライバーを呼び出す場合[ **WdfDeviceSetSpecialFileSupport** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nf-wdfdevice-wdfdevicesetspecialfilesupport)デバイスは、特別なファイルが開いて、デバイスの場合、フレームワークを許可していない、PnP マネージャーを削除するか、デバイスを停止します。

ドライバーが呼び出された後[ **WdfDeviceAddDependentUsageDeviceObject**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nf-wdfdevice-wdfdeviceadddependentusagedeviceobject)、呼び出すことができます[ **WdfDeviceRemoveDependentUsageDeviceObject** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nf-wdfdevice-wdfdeviceremovedependentusagedeviceobject)を別のデバイスでデバイスの依存関係を削除します。

 

 






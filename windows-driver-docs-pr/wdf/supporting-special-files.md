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
ms.openlocfilehash: 960698fdcd12875c75a21f7f1490401c6319cd7e
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56574484"
---
# <a name="supporting-special-files"></a>特別なファイルのサポート


*特別なファイル*ページング ファイル、ダンプ ファイル、および休止状態ファイルが含まれます。 ドライバーのターゲット デバイスがこれらのファイル システムを使用する記憶域デバイスの場合は、ドライバー、次の操作する必要があります。

-   呼び出す[ **WdfDeviceSetSpecialFileSupport** ](https://msdn.microsoft.com/library/windows/hardware/ff546903)を有効にするまたは特殊なファイルの種類ごとにサポートを無効にします。 (特別なファイルの各ドライバーのサポートは既定で無効です。)

    バス ドライバーを[列挙子デバイス](enumerating-the-devices-on-a-bus.md)も呼び出す必要があります[ **WdfDeviceSetSpecialFileSupport** ](https://msdn.microsoft.com/library/windows/hardware/ff546903)特別なファイルをサポートできる子デバイスごとにします。

-   呼び出す[ **WdfDeviceAddDependentUsageDeviceObject**](https://msdn.microsoft.com/library/windows/hardware/ff545864)、特別なファイルをサポートするときに、1 つのデバイスを別のデバイスに依存する場合。

-   必要に応じて指定、 [ *EvtDeviceUsageNotification* ](https://msdn.microsoft.com/library/windows/hardware/ff540915) (KMDF 1.11 以降) または[ *EvtDeviceUsageNotificationEx* ](https://msdn.microsoft.com/library/windows/hardware/hh406365)コールバック関数の場合、ドライバーは特殊なファイルが作成または削除されたときに通知します。

ドライバーを呼び出す場合[ **WdfDeviceSetSpecialFileSupport** ](https://msdn.microsoft.com/library/windows/hardware/ff546903)デバイスは、特別なファイルが開いて、デバイスの場合、フレームワークを許可していない、PnP マネージャーを削除するか、デバイスを停止します。

ドライバーが呼び出された後[ **WdfDeviceAddDependentUsageDeviceObject**](https://msdn.microsoft.com/library/windows/hardware/ff545864)、呼び出すことができます[ **WdfDeviceRemoveDependentUsageDeviceObject** ](https://msdn.microsoft.com/library/windows/hardware/ff546829)を別のデバイスでデバイスの依存関係を削除します。

 

 






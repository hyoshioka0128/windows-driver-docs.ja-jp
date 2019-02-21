---
title: デバイスのセットアップ情報の取得
description: デバイスのセットアップ情報の取得
ms.assetid: 95e88e4a-5a31-4d82-99ea-c9a4d7766c0f
keywords:
- オーディオ アダプター WDK、セットアップ情報の取得
- アダプターのドライバー WDK オーディオは、セットアップ情報の取得
- ポート クラス オーディオ アダプター WDK、セットアップ情報の取得
- デバイスのセットアップ情報の取得
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 230312578cde427e1503f6a4b647ce43eece226f
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56537505"
---
# <a name="retrieving-device-setup-information"></a>デバイスのセットアップ情報の取得


## <span id="retrieving_device_setup_information"></span><span id="RETRIEVING_DEVICE_SETUP_INFORMATION"></span>


セットアップ情報をレジストリから取得するアダプターのドライバーを呼び出すことができます、 [ **PcGetDeviceProperty** ](https://msdn.microsoft.com/library/windows/hardware/ff537701)関数、およびミニポート ドライバーには、ポート ドライバーを呼び出すことができます[ **IPort::GetDeviceProperty** ](https://msdn.microsoft.com/library/windows/hardware/ff536941)メソッド。

これらの呼び出しのいずれか、呼び出し元を選択します。 次のデバイスのいずれかに、デバイス プロパティのパラメーターを設定して要求するセットアップ情報の種類\_レジストリ\_ファイル Wdm.h のヘッダーからプロパティの列挙値。

-   **DevicePropertyAddress**

-   **DevicePropertyBootConfiguration**

-   **DevicePropertyBootConfigurationTranslated**

-   **DevicePropertyBusNumber**

-   **DevicePropertyBusTypeGuid**

-   **DevicePropertyClassGuid**

-   **DevicePropertyClassName**

-   **DevicePropertyCompatibleIDs**

-   **DevicePropertyDetachability**

-   **DevicePropertyDeviceDescription**

-   **DevicePropertyDriverKeyName**

-   **DevicePropertyEnumeratorName**

-   **DevicePropertyFriendlyName**

-   **DevicePropertyHardwareID**

-   **DevicePropertyInstallState**

-   **DevicePropertyLegacyBusType**

-   **DevicePropertyLocationInformation**

-   **DevicePropertyManufacturer**

-   **DevicePropertyPhysicalDeviceObjectName**

-   **DevicePropertyUINumber**

については、DeviceProperty*Xxx*上記の値を参照してください[ **IoGetDeviceProperty**](https://msdn.microsoft.com/library/windows/hardware/ff549203)します。

 

 





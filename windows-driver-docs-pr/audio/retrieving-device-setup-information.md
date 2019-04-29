---
title: デバイス セットアップ情報の取得
description: デバイス セットアップ情報の取得
ms.assetid: 95e88e4a-5a31-4d82-99ea-c9a4d7766c0f
keywords:
- オーディオ アダプター WDK、セットアップ情報の取得
- アダプターのドライバー WDK オーディオは、セットアップ情報の取得
- ポート クラス オーディオ アダプター WDK、セットアップ情報の取得
- デバイスのセットアップ情報の取得
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 230312578cde427e1503f6a4b647ce43eece226f
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63328671"
---
# <a name="retrieving-device-setup-information"></a>デバイス セットアップ情報の取得


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

 

 





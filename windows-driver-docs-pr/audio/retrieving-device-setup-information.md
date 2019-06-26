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
ms.openlocfilehash: 7f176bd20c8313e2981041e9554bc3ae9737c823
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67355267"
---
# <a name="retrieving-device-setup-information"></a>デバイス セットアップ情報の取得


## <span id="retrieving_device_setup_information"></span><span id="RETRIEVING_DEVICE_SETUP_INFORMATION"></span>


セットアップ情報をレジストリから取得するアダプターのドライバーを呼び出すことができます、 [ **PcGetDeviceProperty** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nf-portcls-pcgetdeviceproperty)関数、およびミニポート ドライバーには、ポート ドライバーを呼び出すことができます[ **IPort::GetDeviceProperty** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nf-portcls-iport-getdeviceproperty)メソッド。

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

については、DeviceProperty*Xxx*上記の値を参照してください[ **IoGetDeviceProperty**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iogetdeviceproperty)します。

 

 





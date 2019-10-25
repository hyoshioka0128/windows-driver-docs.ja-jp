---
title: デバイス セットアップ情報の取得
description: デバイス セットアップ情報の取得
ms.assetid: 95e88e4a-5a31-4d82-99ea-c9a4d7766c0f
keywords:
- オーディオアダプター WDK、セットアップ情報の取得
- アダプタードライバー WDK オーディオ、セットアップ情報の取得
- ポートクラスオーディオアダプター WDK、セットアップ情報の取得
- デバイスのセットアップ情報を取得しています
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f00508bdca84a825bfa43dee1d956d5f06edcdf1
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72830181"
---
# <a name="retrieving-device-setup-information"></a>デバイス セットアップ情報の取得


## <span id="retrieving_device_setup_information"></span><span id="RETRIEVING_DEVICE_SETUP_INFORMATION"></span>


レジストリからセットアップ情報を取得するために、アダプタードライバーは[**Pcgetdeviceproperty**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-pcgetdeviceproperty)関数を呼び出すことができます。また、ミニポートドライバーは、ポートドライバーの[**IPort:: getdeviceproperty**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-iport-getdeviceproperty)メソッドを呼び出すことができます。

これらの呼び出しのいずれかについて、呼び出し元は、デバイスプロパティパラメーターを次のいずれかのデバイス\_レジストリに設定することによって、要求するセットアップ情報の種類を選択します。これは、ヘッダーファイルの\_プロパティの列挙値です。

-   **DevicePropertyAddress**

-   **DevicePropertyBootConfiguration**

-   **DevicePropertyBootConfigurationTranslated**

-   **DevicePropertyBusNumber**

-   **DevicePropertyBusTypeGuid**

-   **DevicePropertyClassGuid**

-   **DevicePropertyClassName**

-   **Deviceproperty互換 Id**

-   **DevicePropertyDetachability**

-   **DevicePropertyDeviceDescription**

-   **DevicePropertyDriverKeyName**

-   **Deviceproperty列挙 Atorname**

-   **DevicePropertyFriendlyName**

-   **DevicePropertyHardwareID**

-   **DevicePropertyInstallState**

-   **DevicePropertyLegacyBusType**

-   **DevicePropertyLocationInformation**

-   **DevicePropertyManufacturer**

-   **DevicePropertyPhysicalDeviceObjectName**

-   **DevicePropertyUINumber**

上の DeviceProperty*Xxx*値の詳細については、「 [**Iogetdeviceproperty**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iogetdeviceproperty)」を参照してください。

 

 





---
title: デバイス プロパティの変更の規則
description: デバイス プロパティの変更の規則
ms.assetid: EB554B5C-310A-4b2c-A2D5-22A113415400
keywords:
- デバイスのプロパティを変更するための規則の WDK デバイス インストール
- デバイスのプロパティを変更する、WDK デバイスのインストール
- デバイスの WDK デバイス インストールのプロパティを変更します。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 67d00b231a9ee0ee8b6812c4cf10e925634e5b39
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67377664"
---
# <a name="rules-for-modifying-device-properties"></a>デバイス プロパティの変更の規則


多く[デバイス プロパティ](device-properties.md)複雑な依存関係があるその他のプロパティまたはデバイスの状態にします。 値などの[ **DEVPKEY_Device_Class** ](https://docs.microsoft.com/windows-hardware/drivers/install/devpkey-device-class)と[ **DEVPKEY_Device_ClassGuid** ](https://docs.microsoft.com/windows-hardware/drivers/install/devpkey-device-classguid)互いと一致する必要があります。

予約済みのプロパティの直接的な変更には、デバイス インストール状態が無効になる可能性があります。 たとえば場合、 [ **DEVPKEY_Device_DeviceDesc** ](https://docs.microsoft.com/windows-hardware/drivers/install/devpkey-device-devicedesc)が変更された、システム (バックアップ、ドライバーのロールバック、Windows Update など) の機能が中断する可能性があります。

次のプロパティは読み取り専用とで設定できることはありません[ **SetupDiSetDeviceProperty**](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdisetdevicepropertyw):

-   [**DEVPKEY_Device_Address**](https://docs.microsoft.com/windows-hardware/drivers/install/devpkey-device-address)

-   [**DEVPKEY_Device_BusNumber**](https://docs.microsoft.com/windows-hardware/drivers/install/devpkey-device-busnumber)

-   [**DEVPKEY_Device_BusTypeGuid**](https://docs.microsoft.com/windows-hardware/drivers/install/devpkey-device-bustypeguid)

-   [**DEVPKEY_Device_Capabilities**](https://docs.microsoft.com/windows-hardware/drivers/install/devpkey-device-capabilities)

-   [**DEVPKEY_Device_EnumeratorName**](https://docs.microsoft.com/windows-hardware/drivers/install/devpkey-device-enumeratorname)

-   [**DEVPKEY_Device_LegacyBusType**](https://docs.microsoft.com/windows-hardware/drivers/install/devpkey-device-legacybustype)

-   [**DEVPKEY_Device_PDOName**](https://docs.microsoft.com/windows-hardware/drivers/install/devpkey-device-pdoname)

-   [**DEVPKEY_Device_PowerData**](https://docs.microsoft.com/windows-hardware/drivers/install/devpkey-device-powerdata)

-   [**DEVPKEY_Device_RemovalPolicy**](https://docs.microsoft.com/windows-hardware/drivers/install/devpkey-device-removalpolicy)

-   [**DEVPKEY_Device_RemovalPolicyDefault**](https://docs.microsoft.com/windows-hardware/drivers/install/devpkey-device-removalpolicydefault)

-   [**DEVPKEY_Device_UINumber**](https://docs.microsoft.com/windows-hardware/drivers/install/devpkey-device-uinumber)

書き込み可能なは、次のプロパティです。 ただし、オペレーティング システムで使用するために予約されていますが、直接設定する必要があります。

-   [**DEVPKEY_Device_Class**](https://docs.microsoft.com/windows-hardware/drivers/install/devpkey-device-class)

-   [**DEVPKEY_Device_ClassGuid**](https://docs.microsoft.com/windows-hardware/drivers/install/devpkey-device-classguid)

-   [**DEVPKEY_Device_Driver**](https://docs.microsoft.com/windows-hardware/drivers/install/devpkey-device-driver)

-   [**DEVPKEY_Device_DriverDesc**](https://docs.microsoft.com/windows-hardware/drivers/install/devpkey-device-driverdesc)

-   [**DEVPKEY_Device_Manufacturer**](https://docs.microsoft.com/windows-hardware/drivers/install/devpkey-device-manufacturer)

**注**  *クラス インストーラー*と*共同インストーラー*フレンドリ名以外のデバイス プロパティを変更する必要があります ([**DEVPKEY_Device_FriendlyName**](https://docs.microsoft.com/windows-hardware/drivers/install/devpkey-device-friendlyname)) とデバイスの上限と下限のフィルター ドライバー ([**DEVPKEY_Device_UpperFilters** ](https://docs.microsoft.com/windows-hardware/drivers/install/devpkey-device-upperfilters)と[ **DEVPKEY_Device_LowerFilters**](https://docs.microsoft.com/windows-hardware/drivers/install/devpkey-device-lowerfilters)). 詳細については、次を参照してください。[デバイス インスタンスのプロパティへのアクセス](accessing-device-instance-properties--windows-vista-and-later-.md)します。

 

 

 






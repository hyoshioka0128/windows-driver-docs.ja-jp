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
ms.openlocfilehash: 6bedb78dec0465b00360a87a216ec4d0933d0c50
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63378357"
---
# <a name="rules-for-modifying-device-properties"></a>デバイス プロパティの変更の規則


多く[デバイス プロパティ](device-properties.md)複雑な依存関係があるその他のプロパティまたはデバイスの状態にします。 値などの[ **DEVPKEY_Device_Class** ](https://msdn.microsoft.com/library/windows/hardware/ff542385)と[ **DEVPKEY_Device_ClassGuid** ](https://msdn.microsoft.com/library/windows/hardware/ff542388)互いと一致する必要があります。

予約済みのプロパティの直接的な変更には、デバイス インストール状態が無効になる可能性があります。 たとえば場合、 [ **DEVPKEY_Device_DeviceDesc** ](https://msdn.microsoft.com/library/windows/hardware/ff542407)が変更された、システム (バックアップ、ドライバーのロールバック、Windows Update など) の機能が中断する可能性があります。

次のプロパティは読み取り専用とで設定できることはありません[ **SetupDiSetDeviceProperty**](https://msdn.microsoft.com/library/windows/hardware/ff552163):

-   [**DEVPKEY_Device_Address**](https://msdn.microsoft.com/library/windows/hardware/ff542359)

-   [**DEVPKEY_Device_BusNumber**](https://msdn.microsoft.com/library/windows/hardware/ff542364)

-   [**DEVPKEY_Device_BusTypeGuid**](https://msdn.microsoft.com/library/windows/hardware/ff542371)

-   [**DEVPKEY_Device_Capabilities**](https://msdn.microsoft.com/library/windows/hardware/ff542373)

-   [**DEVPKEY_Device_EnumeratorName**](https://msdn.microsoft.com/library/windows/hardware/ff542489)

-   [**DEVPKEY_Device_LegacyBusType**](https://msdn.microsoft.com/library/windows/hardware/ff542541)

-   [**DEVPKEY_Device_PDOName**](https://msdn.microsoft.com/library/windows/hardware/ff542580)

-   [**DEVPKEY_Device_PowerData**](https://msdn.microsoft.com/library/windows/hardware/ff542586)

-   [**DEVPKEY_Device_RemovalPolicy**](https://msdn.microsoft.com/library/windows/hardware/ff542597)

-   [**DEVPKEY_Device_RemovalPolicyDefault**](https://msdn.microsoft.com/library/windows/hardware/ff542603)

-   [**DEVPKEY_Device_UINumber**](https://msdn.microsoft.com/library/windows/hardware/ff542660)

書き込み可能なは、次のプロパティです。 ただし、オペレーティング システムで使用するために予約されていますが、直接設定する必要があります。

-   [**DEVPKEY_Device_Class**](https://msdn.microsoft.com/library/windows/hardware/ff542385)

-   [**DEVPKEY_Device_ClassGuid**](https://msdn.microsoft.com/library/windows/hardware/ff542388)

-   [**DEVPKEY_Device_Driver**](https://msdn.microsoft.com/library/windows/hardware/ff542427)

-   [**DEVPKEY_Device_DriverDesc**](https://msdn.microsoft.com/library/windows/hardware/ff542436)

-   [**DEVPKEY_Device_Manufacturer**](https://msdn.microsoft.com/library/windows/hardware/ff542558)

**注**  *クラス インストーラー*と*共同インストーラー*フレンドリ名以外のデバイス プロパティを変更する必要があります ([**DEVPKEY_Device_FriendlyName**](https://msdn.microsoft.com/library/windows/hardware/ff542502)) とデバイスの上限と下限のフィルター ドライバー ([**DEVPKEY_Device_UpperFilters** ](https://msdn.microsoft.com/library/windows/hardware/ff542667)と[ **DEVPKEY_Device_LowerFilters**](https://msdn.microsoft.com/library/windows/hardware/ff542554)). 詳細については、次を参照してください。[デバイス インスタンスのプロパティへのアクセス](accessing-device-instance-properties--windows-vista-and-later-.md)します。

 

 

 






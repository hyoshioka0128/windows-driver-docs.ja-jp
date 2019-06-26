---
title: ベンダー定義の ACPI デバイス インターフェイスを提供する
description: ベンダー定義の ACPI デバイス インターフェイスを提供する
ms.assetid: 5a7fd03b-6d4f-481b-8e4e-0e1deaf88583
keywords:
- ACPI デバイス WDK、デバイス インターフェイス
- デバイスのベンダ定義の WDK ACPI インターフェイスします。
- デバイスの WDK ACPI インターフェイスします。
- 機能ドライバー WDK ACPI、デバイスのベンダ定義のインターフェイス
- WDM 関数ドライバー WDK ACPI、デバイスのベンダ定義のインターフェイス
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 24d4b33ce8796b54295f69c5c1e85e7ae66faf65
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67355818"
---
# <a name="providing-a-vendor-defined-acpi-device-interface"></a>ベンダー定義の ACPI デバイス インターフェイスを提供する





仕入先が、省略可能なことができます提供*デバイス インターフェイス*とカスタムの Ioctl ACPI デバイスの機能のデバイス オブジェクトを操作するためのサポート (*FDO*)。

通常、関数のドライバーを呼び出します[ **IoRegisterDeviceInterface** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ioregisterdeviceinterface)でその[ **AddDevice** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_add_device)デバイス インターフェイスを登録するルーチン。 ドライバー呼び出し[ **IoSetDeviceInterfaceState** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iosetdeviceinterfacestate)プラグ アンド プレイ、FDO の開始後に、インターフェイスを有効にします。 プラグ アンド プレイによってデバイスが削除される場合は、ドライバーが、インターフェイスを無効にする必要があります。

デバイスのインターフェイス クラス GUID では、ベンダー定義です。

 

 





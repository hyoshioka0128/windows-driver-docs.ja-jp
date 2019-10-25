---
title: ベンダー定義の ACPI デバイス インターフェイスを提供する
description: ベンダー定義の ACPI デバイス インターフェイスを提供する
ms.assetid: 5a7fd03b-6d4f-481b-8e4e-0e1deaf88583
keywords:
- ACPI デバイス WDK、デバイスインターフェイス
- ベンダ定義のデバイスインターフェイス WDK ACPI
- デバイスインターフェイス WDK ACPI
- 関数ドライバー WDK ACPI、ベンダ定義デバイスインターフェイス
- WDM 関数ドライバー WDK ACPI、ベンダ定義デバイスインターフェイス
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5439b53fba5dce1cd0af961c2c1a9e81fbc66750
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72831471"
---
# <a name="providing-a-vendor-defined-acpi-device-interface"></a>ベンダー定義の ACPI デバイス インターフェイスを提供する





ベンダは、オプションの*デバイスインターフェイス*と、ACPI デバイスの機能デバイスオブジェクト (*FDO*) を操作するカスタム ioctl のサポートを提供できます。

通常、関数ドライバーは[**AddDevice**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_add_device)ルーチンで[**IoRegisterDeviceInterface**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioregisterdeviceinterface)を呼び出して、デバイスインターフェイスを登録します。 ドライバーは[**Iosetdeviceinterfacestate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iosetdeviceinterfacestate)を呼び出して、プラグアンドプレイ FDO を開始した後にインターフェイスを有効にします。 デバイスがプラグアンドプレイによって削除された場合、ドライバーはインターフェイスを無効にする必要があります。

デバイスインターフェイスクラス GUID は、ベンダーによって定義されています。

 

 





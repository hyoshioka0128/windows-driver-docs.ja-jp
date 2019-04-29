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
ms.openlocfilehash: 28f13f79930dce8b58de1a07428f9ff0b6ec09e5
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63328827"
---
# <a name="providing-a-vendor-defined-acpi-device-interface"></a>ベンダー定義の ACPI デバイス インターフェイスを提供する





仕入先が、省略可能なことができます提供*デバイス インターフェイス*とカスタムの Ioctl ACPI デバイスの機能のデバイス オブジェクトを操作するためのサポート (*FDO*)。

通常、関数のドライバーを呼び出します[ **IoRegisterDeviceInterface** ](https://msdn.microsoft.com/library/windows/hardware/ff549506)でその[ **AddDevice** ](https://msdn.microsoft.com/library/windows/hardware/ff540521)デバイス インターフェイスを登録するルーチン。 ドライバー呼び出し[ **IoSetDeviceInterfaceState** ](https://msdn.microsoft.com/library/windows/hardware/ff549700)プラグ アンド プレイ、FDO の開始後に、インターフェイスを有効にします。 プラグ アンド プレイによってデバイスが削除される場合は、ドライバーが、インターフェイスを無効にする必要があります。

デバイスのインターフェイス クラス GUID では、ベンダー定義です。

 

 





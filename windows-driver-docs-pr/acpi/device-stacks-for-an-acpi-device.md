---
title: ACPI デバイスのデバイス スタック
description: ACPI デバイスのデバイス スタック
ms.assetid: f177d29f-eaf9-4126-8cb3-9355d977bfb0
keywords:
- ACPI デバイス WDK、デバイス スタック
- デバイス スタックの WDK ACPI
- WDK ACPI の機能のデバイス オブジェクト
- FDOs WDK ACPI
- DOs WDK ACPI をフィルター処理します。
- ルート バス ドライバー WDK ACPI
- ドライバー WDK ACPI、デバイス スタックを関数します。
- WDM 関数ドライバー WDK ACPI、デバイス スタック
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 71b194c354abde00a56417143950921a2511715a
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63328853"
---
# <a name="device-stacks-for-an-acpi-device"></a>ACPI デバイスのデバイス スタック





このセクションでは、オプションの機能のデバイス オブジェクトを含む、デバイスを ACPI のデバイス スタックをについて説明します (*FDO*) WDM 関数のベンダーから提供されたドライバーによって作成します。

システムでは、システムの ACPI 名前空間内の各デバイスは、次の図に示すように 2 つのデバイス スタックの 1 つ作成します。

![左側でのフィルターは、および右側に、acpi デバイス スタックを示すダイアグラムを 2 つのフィルターなしの acpi デバイス スタック操作を行います](images/acpidev1.png)

ACPI デバイスがシステム ボードに統合されて、ハードウェア デバイスの場合は、システムは、bus フィルター デバイス オブジェクト (フィルター操作を実行) を使用デバイス スタックを作成します。 デバイスの物理デバイス オブジェクト (*PDO*) が作成されるシステム提供のルートでバス ドライバーと ACPI ドライバー作成 bus フィルター操作を行います。 操作フィルターの存在は、デバイス スタック上の他のデバイス オブジェクトに対して透過的です。

場合は、デバイスは、システム ボードに統合されたハードウェア デバイスではない、ACPI ドライバーは、デバイスを列挙し、PDO を作成します。 いずれの場合も、ベンダーは省略可能な FDO を指定できます。

### <a name="system-supplied-root-bus-driver-and-acpi-driver"></a>ルートのシステム提供のバス ドライバーと ACPI ドライバー

Microsoft は、ルートのバス ドライバーを提供し、 [ACPI ドライバー](https://msdn.microsoft.com/library/windows/hardware/ff540493)します。 ACPI BIOS システムで HAL が原因、デバイス ツリーで、オペレーティング システムと、BIOS のインターフェイスとして機能しますベース システムの起動時に読み込まれる ACPI ドライバー。 ACPI ドライバーは、他のドライバーに対して透過的です。

### <a name="vendor-supplied-function-driver"></a>ドライバーのベンダーによって提供される関数

仕入先には、デバイスの ACPI オプション WDM 関数のドライバーを指定できます。 関数のドライバーでは、デバイスの操作のリージョンと、関連するデバイスに固有の操作を実装します。

 

 





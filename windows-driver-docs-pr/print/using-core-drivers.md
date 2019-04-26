---
title: コア ドライバーの使用
description: コア ドライバーの使用
ms.assetid: 333f3f17-0cdc-48d3-bb30-f8e2d7216d89
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: fffa11f020d3233267b23e614e818898019365f7
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63339644"
---
# <a name="using-core-drivers"></a>コア ドライバーの使用


ライターの印刷ドライバーが一覧表示する主要なモデル、INF のモデルのセクションでは GUID を使用して作成したコア ドライバーを使用できます、 **PackageAware**と**CoreDriverSections**キーワード。

次に、例を示します。

```cpp
[Version]
Signature="$Windows NT$"
ClassGUID={4D36E979-E325-11CE-BFC1-08002BE10318}
Class=Printer
Provider="OEM Company"
CatalogFile=PackageAware.cat     ; Single Catalog file for all OS versions
DriverVer=10/10/2005, 1.2.3.4

[Manufacturer]
"OEM Company" = Company, NTx86.6.0

;Models section for installation of x86 driver on 
; Windows Vista and later

[Company.NTx86.6.0]
"My Device Description"  = DriverInstall_Vista, OEM_Company_NameABC_123A
; Core driver definition as discussed in the section Writing Core Drivers
"{GUID1}" = {GUID1}, {GUID1}

[DriverInstall_Vista]
CopyFiles=@file.dll
CoreDriverSections="{D20EA372-DD35-4950-9ED8-A6335AFE79F0},UNIDRV.OEM,UNIDRV_DATA,TTFSUB.OEM", "{GUID1},MANUFACTURER_CORE"
The package install section must also be added, and list all core driver dependencies:
[PrinterPackageInstallation.x86]
PackageAware=TRUE
CoreDriverDependencies={D20EA372-DD35-4950-9ED8-A6335AFE79F0},{GUID1}
```

 

 





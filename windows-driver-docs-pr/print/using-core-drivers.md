---
title: Core のドライバーを使用します。
description: Core のドライバーを使用します。
ms.assetid: 333f3f17-0cdc-48d3-bb30-f8e2d7216d89
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: fffa11f020d3233267b23e614e818898019365f7
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56539669"
---
# <a name="using-core-drivers"></a>Core のドライバーを使用します。


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

 

 





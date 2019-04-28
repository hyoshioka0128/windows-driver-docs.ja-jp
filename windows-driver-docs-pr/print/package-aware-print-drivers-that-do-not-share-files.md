---
title: ファイルを共有しないパッケージ対応印刷ドライバー
description: ファイルを共有しないパッケージ対応印刷ドライバー
ms.assetid: cd114766-37f4-43b5-8e2a-d85f95c973ab
keywords:
- パッケージに対応した印刷ドライバー WDK
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4b76f1947ae78a9c321fe66068bf870900002489
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63362843"
---
# <a name="package-aware-print-drivers-that-do-not-share-files"></a>ファイルを共有しないパッケージ対応印刷ドライバー


ドライバー パッケージ内のファイルは、名前は一意とが、他のドライバー パッケージで行われない、PrinterPackageInstallation セクションを INF ファイルに追加します。 ここでは、追加、 **PackageAware**23 行目の次の例で示すように、キーワードを =。

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
"My Device Description"  
   = DriverInstall_Vista, OEM_Company_NameABC_640A

[DriverInstall_Vista]
CopyFiles=@OEMRES.DLL,@OEMABC.GPD
DataFile=OEMABC.GPD

[PrinterPackageInstallation.x86]
PackageAware=TRUE

; Source Media Information Sections
[DestinationDirs]
DefaultDestDir=66000

[SourceDisksNames.x86]
1   = %MediaDescription%,,,"I386"

[SourceDisksFiles]
OEMRES.DLL  = 1
OEMABC.GPD  = 1
OEMCORE.DLL = 1

[Strings]
MediaDescription = "Description for Vendor provided media"
```

 

 





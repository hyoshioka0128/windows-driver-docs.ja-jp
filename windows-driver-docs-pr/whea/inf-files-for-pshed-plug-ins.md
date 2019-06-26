---
title: PSHED プラグインの INF ファイル
description: PSHED プラグインの INF ファイル
ms.assetid: 60bb9902-c558-4ee1-9b33-1a08885e7c06
keywords:
- PSHED プラグイン WDK WHEA、INF ファイル
- プラットフォーム固有のハードウェア エラー ドライバー プラグインを WDK WHEA、INF ファイル
- INF ファイル WDK WHEA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d6c3cabad180eea41df3a78649186e809b68646a
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67386467"
---
# <a name="inf-files-for-pshed-plug-ins"></a>PSHED プラグインの INF ファイル


によって、PSHED プラグインがインストールされている、[情報 (INF) ファイル](https://docs.microsoft.com/windows-hardware/drivers/install/inf-files)します。 PSHED プラグインの INF ファイルには、次の標準的な INF ファイルでセクションが含まれます。

[**バージョンの INF セクション**](https://docs.microsoft.com/windows-hardware/drivers/install/inf-version-section)

[**INF SourceDisksNames セクション**](https://docs.microsoft.com/windows-hardware/drivers/install/inf-sourcedisksnames-section)

[**INF SourceDisksFiles セクション**](https://docs.microsoft.com/windows-hardware/drivers/install/inf-sourcedisksfiles-section)

[**INF DestinationDirs セクション**](https://docs.microsoft.com/windows-hardware/drivers/install/inf-destinationdirs-section)

[**製造元の INF セクション**](https://docs.microsoft.com/windows-hardware/drivers/install/inf-manufacturer-section)

[**INF*モデル*セクション**](https://docs.microsoft.com/windows-hardware/drivers/install/inf-models-section)

[**INF *DDInstall*セクション**](https://docs.microsoft.com/windows-hardware/drivers/install/inf-ddinstall-section)

[**INF *DDInstall*します。「サービス」セクション**](https://docs.microsoft.com/windows-hardware/drivers/install/inf-ddinstall-services-section)

[**INF 文字列 セクション**](https://docs.microsoft.com/windows-hardware/drivers/install/inf-strings-section)

内で、 [ **INF*モデル*セクション**](https://docs.microsoft.com/windows-hardware/drivers/install/inf-models-section)、プラットフォーム ベンダーは、いずれかを使用できる[ハードウェア識別子 (ID)](https://docs.microsoft.com/windows-hardware/drivers/install/hardware-ids) PSHED プラグインの。 使用して ID を指定したハードウェア、 *hw id*内のエントリ、*モデル*セクションし、ACPI 名前空間または別のデバイスの名前空間でのハードウェア ID を指定できます。 仕入先を指定できますも、[互換性 ID](https://docs.microsoft.com/windows-hardware/drivers/install/compatible-ids)の値を持つ*PNP0C33*します。 この互換性のある ID を使用して、Microsoft と互換性のあるハードウェア エラー デバイスを定義します。 仕入先を使用して互換性のある ID を指定します、*互換性のある id*内のエントリ、*モデル*セクション。

PSHED プラグインの INF ファイルに含める必要がありますも、 [ **AddReg** ](https://docs.microsoft.com/windows-hardware/drivers/install/inf-addreg-directive)にエントリを追加するファイルのセクションを参照するディレクティブ、**システム**\\ **CurrentControlSet**\\**コントロール**\\**PSHED**\\**プラグイン**レジストリのキー。 このエントリは、プラグインの PSHED がシステムにインストールされていることを PSHED に通知します。 これにより、システムを起動するたびにすべてインストールされている PSHED プラグインが正常にロードされていることを確認するよう PSHED できます。

例:

```cpp
;
; Example PSHED plug-in INF file
;

[Version]
Signature = "$Windows NT$"
Provider = %Msft%
CatalogFile = "ExamplePSHEDPlugin.cat"
DriverVer = 01/01/06,1.0

[SourceDiskNames]
1 = %DiskName%

[SourceDiskFiles]
%FileName% = 1

[DestinationDirs]
DefaultDestDir = 12 ; %SystemRoot%\system32\drivers
ExamplePSHEDPlugin.DriverFiles = 12 ; %SystemRoot%\system32\drivers

[Manufacturer]
%Msft% = Microsoft

[Microsoft]
%DeviceDesc% = ExamplePSHEDPluginInstall,%DeviceId%

[ExamplePSHEDPluginInstall]
OptionDesc = %Description%
CopyFiles = ExamplePSHEDPlugin.DriverFiles
AddReg = ExamaplePSHEDPlugin.AddReg

[ExamplePSHEDPluginInstall.Services]
AddService = %ServiceName%,,ExamplePSHEDPlugin.Service

[ExamplePSHEDPlugin.DriverFiles]
%FileName%,,,0x00000040 ; COPYFLG_OVERWRITE_OLDER_ONLY

[ExamplePSHEDPlugin.AddReg]
HKLM,%PSHEDControlPath%,%ServiceName%,0x00000000,%FileName%

[ExamplePSHEDPlugin.Service]
DisplayName = %ServiceName%
Description = %ServiceDesc%
ServiceType = 1  ; SERVICE_KERNEL_DRIVER
StartType = 3    ; SERVICE_DEMAND_START
ErrorControl = 1 ; SERVICE_ERROR_NORMAL
ServiceBinary = %12%\%FileName%

[Strings]
%Msft% = "Microsoft Corporation"
%DiskName% = "Example PSHED Plug-In Installation Disk"
%FileName% = "ExamplePSHEDPlugin.sys"
%DeviceDesc% = "Example PSHED Plug-In Device"
%DeviceId% = "ACPI\PSHEDPI"
%Description% = "Example PSHED Plug-In"
%ServiceName% = "ExamplePSHEDPlugin"
%ServiceDesc% = "Example PSHED Plug-In"
%PSHEDControlPath% = "System\CurrentControlSet\Control\PSHED\Plugins"
```

 

 





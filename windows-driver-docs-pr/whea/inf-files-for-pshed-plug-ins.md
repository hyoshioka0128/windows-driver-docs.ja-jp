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
ms.openlocfilehash: 604861b275a238d875dd06be3b32fb929a0159d3
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63340797"
---
# <a name="inf-files-for-pshed-plug-ins"></a>PSHED プラグインの INF ファイル


によって、PSHED プラグインがインストールされている、[情報 (INF) ファイル](https://msdn.microsoft.com/library/windows/hardware/ff547402)します。 PSHED プラグインの INF ファイルには、次の標準的な INF ファイルでセクションが含まれます。

[**バージョンの INF セクション**](https://msdn.microsoft.com/library/windows/hardware/ff547502)

[**INF SourceDisksNames セクション**](https://msdn.microsoft.com/library/windows/hardware/ff547478)

[**INF SourceDisksFiles セクション**](https://msdn.microsoft.com/library/windows/hardware/ff547472)

[**INF DestinationDirs セクション**](https://msdn.microsoft.com/library/windows/hardware/ff547383)

[**製造元の INF セクション**](https://msdn.microsoft.com/library/windows/hardware/ff547454)

[**INF*モデル*セクション**](https://msdn.microsoft.com/library/windows/hardware/ff547456)

[**INF *DDInstall*セクション**](https://msdn.microsoft.com/library/windows/hardware/ff547344)

[**INF *DDInstall*します。「サービス」セクション**](https://msdn.microsoft.com/library/windows/hardware/ff547349)

[**INF 文字列 セクション**](https://msdn.microsoft.com/library/windows/hardware/ff547485)

内で、 [ **INF*モデル*セクション**](https://msdn.microsoft.com/library/windows/hardware/ff547456)、プラットフォーム ベンダーは、いずれかを使用できる[ハードウェア識別子 (ID)](https://msdn.microsoft.com/library/windows/hardware/ff546152) PSHED プラグインの。 使用して ID を指定したハードウェア、 *hw id*内のエントリ、*モデル*セクションし、ACPI 名前空間または別のデバイスの名前空間でのハードウェア ID を指定できます。 仕入先を指定できますも、[互換性 ID](https://msdn.microsoft.com/library/windows/hardware/ff539950)の値を持つ*PNP0C33*します。 この互換性のある ID を使用して、Microsoft と互換性のあるハードウェア エラー デバイスを定義します。 仕入先を使用して互換性のある ID を指定します、*互換性のある id*内のエントリ、*モデル*セクション。

PSHED プラグインの INF ファイルに含める必要がありますも、 [ **AddReg** ](https://msdn.microsoft.com/library/windows/hardware/ff546320)にエントリを追加するファイルのセクションを参照するディレクティブ、**システム**\\ **CurrentControlSet**\\**コントロール**\\**PSHED**\\**プラグイン**レジストリのキー。 このエントリは、プラグインの PSHED がシステムにインストールされていることを PSHED に通知します。 これにより、システムを起動するたびにすべてインストールされている PSHED プラグインが正常にロードされていることを確認するよう PSHED できます。

次に、例を示します。

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

 

 





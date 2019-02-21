---
title: コールアウト ドライバーの INF ファイル
description: コールアウト ドライバーの INF ファイル
ms.assetid: 2cdaf6a4-3297-4081-a64e-7ab5dc74e7e8
keywords:
- Windows Filtering Platform コールアウト ドライバー WDK をインストールします。
- コールアウト ドライバー WDK Windows フィルタ リング プラットフォームをインストールします。
- コールアウト ドライバー WDK Windows フィルタ リング プラットフォームをインストールします。
- INF ファイル WDK Windows フィルタ リング プラットフォーム
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2e694073d8d3d7c3f80d951f412a0649997b46ae
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56552410"
---
# <a name="inf-files-for-callout-drivers"></a>コールアウト ドライバーの INF ファイル


Windows フィルタ リング プラットフォームのコールアウト ドライバーは、セットアップ情報ファイル (INF) ファイルによってインストールされます。 コールアウト ドライバーの INF ファイルには、次の INF ファイル セクションのみが含まれます。

[**バージョンの INF セクション**](https://msdn.microsoft.com/library/windows/hardware/ff547502)

[**INF SourceDisksNames セクション**](https://msdn.microsoft.com/library/windows/hardware/ff547478)

[**INF SourceDisksFiles セクション**](https://msdn.microsoft.com/library/windows/hardware/ff547472)

[**INF DestinationDirs セクション**](https://msdn.microsoft.com/library/windows/hardware/ff547383)

[**INF DefaultInstall セクション**](https://msdn.microsoft.com/library/windows/hardware/ff547356)

[**INF DefaultInstall.Services セクション**](https://msdn.microsoft.com/library/windows/hardware/ff547360)

[**INF 文字列 セクション**](https://msdn.microsoft.com/library/windows/hardware/ff547485)

次に、例を示します。

```INF
;
; Example callout driver INF file
;

[Version]
Signature = "$Windows NT$"
Provider = %Msft%
CatalogFile = "ExampleCalloutDriver.cat"
DriverVer = 01/15/05,1.0

[SourceDisksNames]
1 = %DiskName%

[SourceDisksFiles]
ExampleCalloutDriver.sys = 1

[DestinationDirs]
DefaultDestDir = 12 ; %windir%\system32\drivers
ExampleCalloutDriver.DriverFiles = 12 ; %windir%\system32\drivers

[DefaultInstall]
OptionDesc = %Description%
CopyFiles = ExampleCalloutDriver.DriverFiles

[DefaultInstall.Services]
AddService = %ServiceName%,,ExampleCalloutDriver.Service

[DefaultUninstall]
DelFiles = ExampleCalloutDriver.DriverFiles

[DefaultUninstall.Services]
DelService = ExampleCalloutDriver,0x200 ; SPSVCINST_STOPSERVICE

[ExampleCalloutDriver.DriverFiles]
ExampleCalloutDriver.sys,,,0x00000040 ; COPYFLG_OVERWRITE_OLDER_ONLY

[ExampleCalloutDriver.Service]
DisplayName = %ServiceName%
Description = %ServiceDesc%
ServiceType = 1  ; SERVICE_KERNEL_DRIVER
StartType = 0    ; SERVICE_BOOT_START
ErrorControl = 1 ; SERVICE_ERROR_NORMAL
ServiceBinary = %12%\ExampleCalloutDriver.sys

[Strings]
%Msft% = "Microsoft Corporation"
%DiskName% = "Example Callout Driver Installation Disk"
%Description% = "Example Callout Driver"
%ServiceName% = "ExampleCalloutDriver"
%ServiceDesc% = "Example Callout Driver"
```

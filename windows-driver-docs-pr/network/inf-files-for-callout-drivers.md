---
title: コールアウト ドライバーの INF ファイル
description: コールアウト ドライバーの INF ファイル
ms.assetid: 2cdaf6a4-3297-4081-a64e-7ab5dc74e7e8
keywords:
- Windows Filtering Platform コールアウトドライバー WDK、インストール
- コールアウトドライバー WDK Windows フィルタリングプラットフォーム、インストール
- コールアウトドライバーのインストール WDK Windows フィルタリングプラットフォーム
- INF ファイル WDK Windows フィルタリングプラットフォーム
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 585b153026c899a02da817315f43b1613d404746
ms.sourcegitcommit: 0e0dc5f080df541cbb13b87a49c5eb88f757d4b7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/28/2019
ms.locfileid: "72987835"
---
# <a name="inf-files-for-callout-drivers"></a>コールアウト ドライバーの INF ファイル

Windows Filtering Platform コールアウトドライバーは、セットアップ情報ファイル (INF) ファイルによってインストールされます。 コールアウトドライバーの INF ファイルには、次の INF ファイルのセクションのみが含まれています。

[**INF バージョンセクション**](https://docs.microsoft.com/windows-hardware/drivers/install/inf-version-section)

[**INF SourceDisksNames セクション**](https://docs.microsoft.com/windows-hardware/drivers/install/inf-sourcedisksnames-section)

[**INF SourceDisksFiles セクション**](https://docs.microsoft.com/windows-hardware/drivers/install/inf-sourcedisksfiles-section)

[**INF DestinationDirs セクション**](https://docs.microsoft.com/windows-hardware/drivers/install/inf-destinationdirs-section)

[**INF DefaultInstall セクション**](https://docs.microsoft.com/windows-hardware/drivers/install/inf-defaultinstall-section)

[**INF DefaultInstall セクション**](https://docs.microsoft.com/windows-hardware/drivers/install/inf-defaultinstall-services-section)

[**INF 文字列セクション**](https://docs.microsoft.com/windows-hardware/drivers/install/inf-strings-section)

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
Msft = "Microsoft Corporation"
DiskName = "Example Callout Driver Installation Disk"
Description = "Example Callout Driver"
ServiceName = "ExampleCalloutDriver"
ServiceDesc = "Example Callout Driver"
```

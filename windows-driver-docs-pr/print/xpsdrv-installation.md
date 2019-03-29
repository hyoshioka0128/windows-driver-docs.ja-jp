---
title: XPSDrv インストール
description: XPSDrv インストール
ms.assetid: 0b5ef114-2862-46f9-bd32-ae09fa4e6a92
keywords:
- XPSDrv プリンター ドライバー WDK をインストールします。
- WDK の INF ファイルの印刷、XPSDrv プリンター ドライバー
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 33e6591271f42e4ff777b0daf4d6df9ccfc75d01
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56570543"
---
# <a name="xpsdrv-installation"></a>XPSDrv インストール


スプーラーが正しくインストールするのに XPSDrv ドライバーは、次に含める必要があります。

-   [ **CopyFiles** ](https://msdn.microsoft.com/library/windows/hardware/ff546346)ドライバーの INF ファイルのディレクティブが参照する必要があります、[フィルター パイプライン構成ファイル](filter-pipeline-configuration-file.md)します。

-   ニーズ ディレクティブは、Xpsdrv.oem を参照する必要があります。 ニーズ ディレクティブの詳細については、次を参照してください。 [ **INF DDInstall セクション**](https://msdn.microsoft.com/library/windows/hardware/ff547344)と[Inf のソース メディア](https://msdn.microsoft.com/library/windows/hardware/ff552302)します。

-   構成のモジュールは、Unidrv に基づいている場合、Unidrv.oem と Xpsgpd.oem にニーズ ディレクティブが参照する必要があります。 同様に、XPSDrv ドライバーの構成のモジュールは、PScript5 に基づいている場合は、ニーズのディレクティブは Pscript.oem と Xpsppd.oem 参照する必要があります。

次のコード例は、INF ファイルを上記の変更を示しています。

```cpp
[Version]
Signature="$Windows NT$"
Provider=%MS%
ClassGUID={4D36E979-E325-11CE-BFC1-08002BE10318}
Class=Printer
CatalogFile=ntprint.cat
DriverVer=10/11/2005,6.0.5242.0

[Manufacturer]
Microsoft

[Microsoft]
"XPSDrv Sample Driver" = INSTALL_XDSMPL_FILTERS

[INSTALL_XDSMPL_FILTERS]
CopyFiles=XPSDrvSample,ConfigPlugin,COLORPROFILES
DriverFile=mxdwdrv.dll
ConfigFile=unidrvui.dll
HelpFile=unidrv.HLP 
DataFile=XDSmpl.GPD
Include=NTPRINT.INF
Needs=UNIDRV.OEM, XPSGPD.OEM, XPSDRV.OEM
ICMProfiles=xdwscRGB.cdmp

[XPSDrvSample]
xdsmpl-pipelineconfig.xml
...
```

 

 





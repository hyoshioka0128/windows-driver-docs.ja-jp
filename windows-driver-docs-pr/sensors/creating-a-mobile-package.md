---
title: モバイルパッケージの作成
description: このトピックでは、モバイルデバイスにサンプルドライバーをインストールするためのパッケージの作成について説明します。
ms.assetid: E929D80D-17BF-4079-8CF9-972020306358
ms.date: 07/20/2018
ms.localizationpriority: medium
ms.openlocfilehash: 7b3918ee4680eca84c7ad5a9b0e70ff3d22e892f
ms.sourcegitcommit: d5f54510b9500413dd3084b59cb8869f2f6b13cf
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/09/2019
ms.locfileid: "68866769"
---
# <a name="creating-a-mobile-package"></a>モバイルパッケージの作成

このトピックでは、モバイルデバイスにサンプルドライバーをインストールするためのパッケージの作成について説明します。

次のタスクを実行して、サンプルドライバーのパッケージを作成します。

1. 次のコードをコピーし、メモ帳に貼り付けます。

```XML
<?xml version="1.0" encoding="utf-8"?>
<!--
Copyright (c) Microsoft Corporation.  All rights reserved.
-->
<Package xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns:xsd="http://www.w3.org/2001/XMLSchema"
  Owner="OEMName"
  OwnerType="OEM"
  Component="Drivers"
  SubComponent="Adxl345Acc"
  ReleaseType="Production"
  xmlns="urn:Microsoft.WindowsPhone/PackageSchema.v8.00">
  <Components>
    <OSComponent>
      <Files>
        <File DestinationDir="$(runtime.drivers)\umdf" Source="$(_RELEASEDIR)\Adxl345Acc.dll" />
      </Files>

      <RegKeys>
        <RegKey KeyName="$(hklm.system)\ControlSet001\Enum\Root\umdf2\Adxl345Acc">
          <RegValue Name="ClassGUID"    Type="REG_SZ"        Value="{5175D334-C371-4806-B3BA-71FD53C9258D}"  />
          <RegValue Name="Class"        Type="REG_SZ"        Value="Sensor" />
          <RegValue Name="ConfigFlags"  Type="REG_DWORD"     Value="00000020"  />
          <RegValue Name="HardwareID"   Type="REG_MULTI_SZ"  Value="umdf2\Adxl345Acc"  />
        </RegKey>
      </RegKeys>
    </OSComponent>

    <!-- Use Phone-specific INF for security. -->
    <Driver InfSource="$(DRIVERS_FILES_PATH)\Adxl345Acc.inf">
      <Security InfSectionName="Sensor_Inst_SecurityAddReg">
          <AccessedByCapability Id="ID_CAP_SENSORS" Rights="$(GENERIC_READ)$(GENERIC_EXECUTE)" />
      </Security>
      <Reference Source="$(_RELEASEDIR)\Adxl345Acc.dll" />
    </Driver>

  </Components>

</Package>
```

>[!NOTE]
> **Security InfSectionName**要素の値は、このトピックで説明する**AddReg**フィールドの値とまったく同じである必要があります。[INX ファイルを確認](review-and-revise-the-inf-file.md)します。

2. メモ帳のメインメニューで、[**ファイル** &gt;名を付け**て保存**] をクリックし、[名前を付け**て**保存] ダイアログウィンドウで、ドロップダウンボックスを使用して [名前を付け**て保存**] フィールドを [**すべてのファイル**] に設定します。 * * * *

3. [**ファイル名**] テキストボックスに、次のように入力します。

*adxl345acc*
4. [**名前を付けて保存**] ダイアログウィンドウの上部にある [保存先] ボックスを使用して、Microsoft Visual Studio のプロジェクトフォルダーに移動します。 [**保存**] をクリックします。

前の手順で示したように*adxl345acc*ファイルを作成した後、Windows Driver KIT (WDK) に含まれている**pkggen**ツールを使用してファイルをパッケージ化することもできます。

WDK を既定の場所にインストールした場合、 **pkggen**は次の場所にあります。 *%WPDKCONTENTROOT%\Tools\bin\i386*

モバイルデバイスのパッケージを作成する方法については、「[パッケージジェネレーターのコマンドライン引数](https://docs.microsoft.com/en-us/windows-hardware/manufacture/mobile/command-line-arguments-for-package-generator)」を参照してください。 包括的な概要については、「 [Mobile Pacakages の作成](https://docs.microsoft.com/previous-versions/windows/hardware/packaging/dn756642(v=vs.85))」を参照してください。

## <a name="related-topics"></a>関連トピック

[モバイルパッケージの作成](https://docs.microsoft.com/previous-versions/windows/hardware/packaging/dn756642(v=vs.85))

[INX ファイルを確認する](review-and-revise-the-inf-file.md)

[パッケージ ジェネレーターのコマンドライン引数](https://docs.microsoft.com/windows-hardware/manufacture/mobile/command-line-arguments-for-package-generator)

---
title: モバイルのパッケージを作成します。
description: このトピックでは、モバイル デバイスのドライバーのサンプルをインストールするためのパッケージの作成についてを説明します。
ms.assetid: E929D80D-17BF-4079-8CF9-972020306358
ms.date: 07/20/2018
ms.localizationpriority: medium
ms.openlocfilehash: 6e21c33ad075d64279643e85b292ff5056bc29fc
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67382892"
---
# <a name="creating-a-mobile-package"></a>モバイルのパッケージを作成します。


このトピックでは、モバイル デバイスのドライバーのサンプルをインストールするためのパッケージの作成についてを説明します。

サンプルのドライバー パッケージを作成するには、次のタスクを実行します。

1. 次のコードをコピーしてノートパッドに貼り付けます。

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
> 値、**セキュリティ InfSectionName**要素正確に同じでなければなりませんの値として、 **AddReg**フィールドのこのトピックで説明します。[INX ファイルを確認して](review-and-revise-the-inf-file.md)します。

 

2. メモ帳のメイン メニューでクリックして**ファイル** &gt; **名前を付けて保存**、次に、**名前を付けて保存**ダイアログ ウィンドウで、ドロップダウン ボックスを使用して、設定、**型として保存**フィールドを**すべてのファイル*** * *。

3. **ファイル名**テキスト ボックスに、次を入力します。

*adxl345acc.pkg.xml*
4. 上部にある [宛先] ボックスを使用して、**付けて**ダイアログ ウィンドウに、Microsoft Visual Studio でプロジェクト フォルダーに移動します。 クリックして**保存**します。

作成した後、 *adxl345acc.pkg.xml*ファイルのように、上記の手順を繰り返し、使用することも、 **pkggen.exe**ツールで、Windows Driver Kit (WDK)、ファイルをパッケージ化するのに含まれています。

既定の場所に WDK をインストールしたかどうかは、検索できる**pkggen.exe**の次の場所。

*%Systemroot%\\Program Files (x86)\\Windows キット\\10\\ツール\\bin\\i386*を参照してください[pkggen.exe ツールを実行して](https://docs.microsoft.com/previous-versions/windows/hardware/packaging/dn756642(v=vs.85)#run-pkg)のモバイル デバイス用のパッケージを作成する方法の手順です。 参照してくださいと[モバイル パッケージを作成する](https://docs.microsoft.com/previous-versions/windows/hardware/packaging/dn756642(v=vs.85))のより包括的な概要。

## <a name="related-topics"></a>関連トピック
[モバイルのパッケージを作成する](https://docs.microsoft.com/previous-versions/windows/hardware/packaging/dn756642(v=vs.85))
[INX ファイルを確認して](review-and-revise-the-inf-file.md)
[pkggen.exe ツールを実行します。](https://docs.microsoft.com/previous-versions/windows/hardware/packaging/dn756642(v=vs.85)#run-pkg)




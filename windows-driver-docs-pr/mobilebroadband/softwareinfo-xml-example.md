---
title: SoftwareInfo XML の例
description: SoftwareInfo XML の例
ms.assetid: 3ee92b21-ed4e-4ed9-9199-3f43f2f8ec00
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: dd0d12ed67003e4ea8db9b1ecef1a300942ec890
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56551401"
---
# <a name="softwareinfo-xml-example"></a>SoftwareInfo XML の例

[!include[MBAE deprecation warning](mbae-deprecation-warning.md)]

次の XML ドキュメントを使用して、 [ServiceInfo XML スキーマ](serviceinfo-xml-schema.md)Contoso ワイヤレス サービスの属性を指定します。

``` syntax
<?xml version="1.0" encoding="utf-8" standalone="yes"?>

<SoftwareInfo xmlns="http://schemas.microsoft.com/windows/2010/08/DeviceMetadata/SoftwareInfo">

  <DeviceCompanionApplications>
    <Package>
      <Identity Name="64022CONTOSO.ContosoDeviceApp" Publisher="CN=05558413-FFF6-4AA5-8176-AD43036533FA" />
      <Applications>
        <Application Id="DeviceAppForPrinters">
          <DeviceNotificationHandlers>
            <DeviceNotificationHandler EventID="NotificationHandler" EventAsset="Fabrikam.OperatorApp. NotificationHandler" />
          </DeviceNotificationHandlers>
        </Application>
      </Applications>
    </Package>
  </DeviceCompanionApplications>

  <PrivilegedApplications>
    <Package>
      <Identity Name="64022CONTOSO.ContosoDeviceApp" Publisher="CN=05558413-FFF6-4AA5-8176-AD43036533FA" AccessCustomDriver="false" />
    </Package>
  </PrivilegedApplications>

</SoftwareInfo>
```

 

 






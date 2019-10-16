---
title: PackageInfo XML の例
description: PackageInfo XML の例
ms.assetid: 4e514e79-d450-4cae-a40d-16ce86f95e43
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a3eb1ab27d978d8eaa79d9fdcfe7ad1b24637d2b
ms.sourcegitcommit: f017184b00f59b088df87a5bd85fec51b7aed8b2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/15/2019
ms.locfileid: "72323729"
---
# <a name="packageinfo-xml-example"></a>PackageInfo XML の例

[!include[MBAE deprecation warning](mbae-deprecation-warning.md)]

次の XML ドキュメントでは、 [Packageinfo xml スキーマ](packageinfo-xml-schema.md)を使用して、ベンダーのメタデータパッケージのコンポーネントを指定しています。

パッケージは、次のハードウェア ID を持つサービス用です。

MBAE:0:L9@E}} DT2。 \*F65MQA57Y + L

**注**: packageinfo .xml に含まれる1つのハードウェア id には、"doid:" プレフィックスが追加されている必要があります。 @no__t

 

パッケージは EN-US ロケール用でもあります。このロケールでは、ドキュメントはメタデータパッケージのコンポーネントの既定のロケールとして設定されます。

``` syntax
<?xml version="1.0" encoding ="UTF-8" ?>

  <PackageInfo xmlns=http://schemas.microsoft.com/windows/DeviceMetadata/PackageInfo/2007/11/
               xmlns:v2=” http://schemas.microsoft.com/windows/2010/08/DeviceMetadata/PackageInfov2”>

  <MetadataKey>
      <HardwareIDList>
        <HardwareID>DOID:MBAE:0:L9@E}}DT2.*F65MQA57Y+L</HardwareID>
      </HardwareIDList>
      <Locale default="true">EN-US</Locale>
      <LastModifiedDate>2008-01-24T00:00:00Z</LastModifiedDate>
      <v2:MultipleLocale>true</v2:MultipleLocale>
  </MetadataKey>

  <PackageStructure>
      <Metadata MetadataID="http://schemas.microsoft.com/windows/DeviceMetadata/PackageInfo/2007/11">PackageInfo.xml</Metadata>
      <Metadata MetadataID="http://schemas.microsoft.com/windows/DeviceMetadata/ServiceInfo/2007/11/">ServiceInformation</Metadata>
      <Metadata MetadataID=”http://schemas.microsoft.com/windows/DeviceMetadata/WindowsInfo/2007/11/”>WindowsInformation</Metadata>
    </PackageStructure>
</PackageInfo>
```

 

 






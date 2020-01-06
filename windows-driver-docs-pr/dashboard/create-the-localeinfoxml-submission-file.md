---
title: LocaleInfo.xml サブミッション ファイルの作成
description: LocaleInfo.xml サブミッション ファイルの作成
ms.assetid: 2b16b045-4d34-418c-8f68-7f688adf8e7e
ms.topic: article
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2f65d958e15445b0a5c492d546795f8bbe500bd3
ms.sourcegitcommit: d30691c8276f7dddd3f8333e84744ddeea1e1020
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/19/2019
ms.locfileid: "75209248"
---
# <a name="create-the-localeinfoxml-submission-file"></a>LocaleInfo.xml サブミッション ファイルの作成

## <a name="localeinfo-xml-schema"></a>LocaleInfo XML スキーマ

デバイス マニフェスト サブミッション パッケージには、LocaleInfo.xml ドキュメントが 1 つ含まれています。このドキュメントの情報は、デバイス メタデータ パッケージ内のロケール情報を検証する際にパートナー センターで使われます。

LocaleInfo.xml ドキュメント内のデータは、以降で説明する LocaleInfo XML スキーマに基づいて書式が設定されます。

> [!NOTE]
> XML ドキュメントは UTF-8 エンコーディングで保存されている必要があります。

アドレス範囲について詳しくは、「[How to Create a Device Metadata Package for Devices and Printers ([デバイスとプリンター] 用デバイス メタデータ パッケージの作成方法)](https://go.microsoft.com/fwlink/?LinkId=253559)」をご覧ください。

### <a name="span-idlocaleinfo_xml_schema_namespacespanspan-idlocaleinfo_xml_schema_namespacespanspan-idlocaleinfo_xml_schema_namespacespanlocaleinfo-xml-schema-namespace"></a><span id="LocaleInfo_XML_Schema_NameSpace"></span><span id="localeinfo_xml_schema_namespace"></span><span id="LOCALEINFO_XML_SCHEMA_NAMESPACE"></span>LocaleInfo XML スキーマの名前空間

LocaleInfo XML スキーマの名前空間は次のようになります: `http://schemas.microsoft.com/Windows/2010/08/MetadataSubmission/LocaleInfo`

### <a name="span-idoverview_of_localeinfo_xml_elements_attributesspanspan-idoverview_of_localeinfo_xml_elements_attributesspanspan-idoverview_of_localeinfo_xml_elements_attributesspanoverview-of-localeinfo-xml-elementsattributes"></a><span id="Overview_of_LocaleInfo_XML_Elements_Attributes"></span><span id="overview_of_localeinfo_xml_elements_attributes"></span><span id="OVERVIEW_OF_LOCALEINFO_XML_ELEMENTS_ATTRIBUTES"></span>LocaleInfo XML の要素/属性の概要

次の表では、LocaleInfo XML スキーマのメタデータの要素と属性について説明します。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th>要素/属性</th>
<th>要素/属性の型</th>
<th>必須/省略可能</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>MultipleLocale</p></td>
<td><p>xs:boolean</p></td>
<td><p>省略可能</p></td>
</tr>
<tr class="even">
<td><p>LocaleDeclaredInPackageInfo</p></td>
<td><p>tns:LocaleDeclaredInPackageInfoType</p></td>
<td><p>省略可能</p></td>
</tr>
<tr class="odd">
<td><p>既定</p></td>
<td><p>xs:boolean</p></td>
<td><p>必須</p></td>
</tr>
<tr class="even">
<td><p>SupportedLocaleList</p></td>
<td><p>tns:SupportedLocaleListType</p></td>
<td><p>省略可能</p></td>
</tr>
<tr class="odd">
<td><p>ロケール</p></td>
<td><p>xs:string</p></td>
<td><p>省略可能</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idlocaleinfo_xml_schema_definitionspanspan-idlocaleinfo_xml_schema_definitionspanspan-idlocaleinfo_xml_schema_definitionspanlocaleinfo-xml-schema-definition"></a><span id="LocaleInfo_XML_Schema_Definition"></span><span id="localeinfo_xml_schema_definition"></span><span id="LOCALEINFO_XML_SCHEMA_DEFINITION"></span>LocaleInfo XML スキーマの定義

LocaleInfo XML スキーマの定義は以下のとおりです。

``` syntax
<?xml version="1.0" encoding="UTF-8"?>
<xs:schema targetNamespace="http://schemas.microsoft.com/Windows/2010/08/MetadataSubmission/LocaleInfo" xmlns:tns="http://schemas.microsoft.com/Windows/2010/08/MetadataSubmission/LocaleInfo" xmlns:xs="http://www.w3.org/2001/XMLSchema" elementFormDefault="qualified" blockDefault="#all">

 <xs:element name="LocaleInfo" type="tns:LocaleInfoType" />

 <xs:complexType name="LocaleInfoType">
  <xs:sequence>
   <xs:element name="MultipleLocale" type="xs:boolean" />
   <xs:element name="LocaleDeclaredInPackageInfo" type="tns:LocaleDeclaredInPackageInfoType" />
   <xs:element name="SupportedLocaleList" type="tns:SupportedLocaleListType" minOccurs="0" />
   <xs:any namespace="##other" processContents="lax" minOccurs="0" maxOccurs="unbounded" />
  </xs:sequence>
 </xs:complexType>

  <xs:complexType name="LocaleDeclaredInPackageInfoType">
    <xs:simpleContent>
      <xs:extension base="xs:string">
        <xs:attribute name="default" type="xs:boolean" use="required" />
      </xs:extension>
    </xs:simpleContent>
  </xs:complexType>

  <xs:complexType name="SupportedLocaleListType">
    <xs:sequence>
      <xs:element name="Locale" type="xs:string" maxOccurs="unbounded" />
      <xs:any namespace="##other" processContents="lax" minOccurs="0" maxOccurs="unbounded" />
    </xs:sequence>
  </xs:complexType>

</xs:schema>
```

## <a name="localeinfo-xml-schema-reference"></a>LocaleInfo XML スキーマ リファレンス

LocaleInfo XML スキーマには、以下の要素と属性が定義されています。

- LocaleInfo

  - MultipleLocale

  - LocaleDeclaredInPackageInfo

      -   既定

   -   SupportedLocaleList

       - ロケール

### <a name="multiplelocale-element"></a>MultipleLocale 要素

MultipleLocale 要素は、デバイス メタデータ パッケージが複数のロケールをサポートしているかどうかを指定します。 この値は、パッケージを適切に検証するためにパートナー センターで使われます。

``` syntax
<xs:element name="MultipleLocale" type="xs:boolean" />
```

**注釈**

デバイス メタデータ パッケージで複数のロケールがサポートされている場合、MultipleLocale 要素は "true" である必要があります。 デバイス メタデータ パッケージでサポートされるロケールが 1 つである場合は、"true" でも "false" でもかまいません。 MultipleLocale の値は、PackageInfo.xml に指定された値と一致している必要があります。

### <a name="span-idlocaledeclaredinpackageinfo_elementspanspan-idlocaledeclaredinpackageinfo_elementspanspan-idlocaledeclaredinpackageinfo_elementspanlocaledeclaredinpackageinfo-element"></a><span id="LocaleDeclaredInPackageInfo_Element"></span><span id="localedeclaredinpackageinfo_element"></span><span id="LOCALEDECLAREDINPACKAGEINFO_ELEMENT"></span>LocaleDeclaredInPackageInfo 要素

LocaleDeclaredInPackageInfo 要素は、デバイス メタデータ パッケージ内で宣言されるロケールとパッケージの属性についての情報を指定します。 この情報は、デバイス メタデータ パッケージに宣言されているロケール メタデータを適切に検証するためにパートナー センターで使われます。

``` syntax
<xs:element name="LocaleDeclaredInPackageInfo" type="tns:LocaleDeclaredInPackageInfoType" />

<xs:complexType name="LocaleDeclaredInPackageInfoType">
  <xs:simpleContent>
    <xs:extension base="xs:string">
      <xs:attribute name="default" type="xs:boolean" use="required" />
    </xs:extension>
  </xs:simpleContent>
</xs:complexType>
```

**注釈**

LocaleDeclaredInPackageInfo 要素は、PackageInfo.xml に指定されたロケール値と一致している必要があります。

### <a name="span-iddefault_attributespanspan-iddefault_attributespanspan-iddefault_attributespandefault-attribute"></a><span id="default_Attribute"></span><span id="default_attribute"></span><span id="DEFAULT_ATTRIBUTE"></span>default 属性

default 属性は、デバイス メタデータ パッケージが、PackageInfo.xml に示されている既定のパッケージであるかどうかを指定します。

``` syntax
<xs:attribute name="default" type="xs:boolean" use="required" />
```

**注釈**

default 要素は、PackageInfo.xml に指定された既定値と一致している必要があります。

### <a name="span-idsupportedlocalelist_elementspanspan-idsupportedlocalelist_elementspanspan-idsupportedlocalelist_elementspansupportedlocalelist-element"></a><span id="SupportedLocaleList_Element"></span><span id="supportedlocalelist_element"></span><span id="SUPPORTEDLOCALELIST_ELEMENT"></span>SupportedLocaleList 要素

SupportedLocaleList 要素は、デバイス メタデータ パッケージでサポートされている他のロケールを指定します。 この情報は、デバイス メタデータ パッケージ内の追加ロケール メタデータを適切に検証するためにパートナー センターで使われます。

``` syntax
<xs:element name="SupportedLocaleList" type="tns:SupportedLocaleListType" minOccurs="0" />

<xs:complexType name="SupportedLocaleListType">
  <xs:sequence>
    <xs:element name="Locale" type="xs:string" maxOccurs="unbounded" />
    <xs:any namespace="##other" processContents="lax" minOccurs="0" maxOccurs="unbounded" />
  </xs:sequence>
</xs:complexType>
```

### <a name="span-idlocale_elementspanspan-idlocale_elementspanspan-idlocale_elementspanlocale-element"></a><span id="Locale_Element"></span><span id="locale_element"></span><span id="LOCALE_ELEMENT"></span>Locale 要素

Locale 要素は、デバイス メタデータ パッケージでサポートされている追加のロケールを指定します。 この値がパートナー センターでどのように使われるかについて詳しくは、SupportedLocaleList 要素をご覧ください。

## <a name="span-idlocaleinfo_xml_examplespanspan-idlocaleinfo_xml_examplespanspan-idlocaleinfo_xml_examplespanlocaleinfo-xml-example"></a><span id="LocaleInfo_XML_Example"></span><span id="localeinfo_xml_example"></span><span id="LOCALEINFO_XML_EXAMPLE"></span>LocaleInfo XML の例


以下の XML ドキュメントでは、LocaleInfo 情報の構成要素が LocaleInfo XML スキーマを使って指定されています。

この例は、en-US、ja-JP、fr-FR の各ロケールをサポートするデバイス メタデータ パッケージを対象としています。 PackageInfo.xml には en-US ロケールがリストされており、PackageInfo.xml に示された既定のロケールのパッケージとなっています。

``` syntax
<?xml version="1.0" encoding="utf-8"?>
<LocaleInfo xmlns="http://schemas.microsoft.com/Windows/2010/08/MetadataSubmission/LocaleInfo">
  
  <MultipleLocale>
    true
  </MultipleLocale>
  
  <LocaleDeclaredInPackageInfo default="true">
    en-US
  </LocaleDeclaredInPackageInfo>
  
  <SupportedLocaleList>
    <Locale>en-US</Locale>
    <Locale>ja-JP</Locale>
    <Locale>fr-FR</Locale>
  </SupportedLocaleList>
  
</LocaleInfo>
```

 

 






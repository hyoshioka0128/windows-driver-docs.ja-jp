---
title: MetadataKey
description: MetadataKey
ms.assetid: 1915db47-98bb-40f5-be3b-75e9af80f506
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8946fa983c1568129fe3dd9b2b082b444543c8d9
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56538901"
---
# <a name="metadatakey"></a>MetadataKey

[!include[MBAE deprecation warning](mbae-deprecation-warning.md)]

MetadataKey 要素には、サービス メタデータ パッケージの属性を指定します。 これには次のものがあります。

-   デバイスでサポートされている各ハードウェア関数の識別子。

-   言語固有のロケールをパッケージ内のテキスト文字列。

## <a name="span-idusagespanspan-idusagespanspan-idusagespanusage"></a><span id="Usage"></span><span id="usage"></span><span id="USAGE"></span>使用状況


``` syntax
<MetadataKey>
  child elements
</MetadataKey>
```

## <a name="span-idattributesspanspan-idattributesspanspan-idattributesspanattributes"></a><span id="Attributes"></span><span id="attributes"></span><span id="ATTRIBUTES"></span>属性


属性はありません。

## <a name="span-idchildelementsspanspan-idchildelementsspanspan-idchildelementsspanchild-elements"></a><span id="Child_elements"></span><span id="child_elements"></span><span id="CHILD_ELEMENTS"></span>子要素


<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>要素</th>
<th>説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><a href="hardwareidlist.md" data-raw-source="[HardwareIDList](hardwareidlist.md)">HardwareIDList</a></p></td>
<td><p><a href="hardwareidlist.md" data-raw-source="[HardwareIDList](hardwareidlist.md)">HardwareIDList</a>要素は、デバイスの 1 つまたは複数のハードウェアの識別文字列を指定します。</p></td>
</tr>
<tr class="even">
<td><p><a href="lastmodifieddate.md" data-raw-source="[LastModifiedDate](lastmodifieddate.md)">LastModifiedDate</a></p></td>
<td><p><a href="lastmodifieddate.md" data-raw-source="[LastModifiedDate](lastmodifieddate.md)">LastModifiedDate</a>要素は、サービス メタデータ パッケージを最後に変更されたタイムスタンプを指定します。</p></td>
</tr>
<tr class="odd">
<td><p><a href="locale.md" data-raw-source="[Locale](locale.md)">ロケール</a></p></td>
<td><p><a href="locale.md" data-raw-source="[Locale](locale.md)">ロケール</a>要素は、サービス メタデータ パッケージのローカライズされたバージョンを指定します。</p></td>
</tr>
<tr class="even">
<td><p><a href="modelidlist.md" data-raw-source="[ModelIDList](modelidlist.md)">ModelIDList</a></p></td>
<td><p><a href="modelidlist.md" data-raw-source="[ModelIDList](modelidlist.md)">ModelIDList</a>要素は、各デバイスの種類またはサービス メタデータ パッケージ内で指定されているモデルの GUID を指定します。</p></td>
</tr>
<tr class="odd">
<td><p><a href="multiplelocale.md" data-raw-source="[MultipleLocale](multiplelocale.md)">MultipleLocale</a></p></td>
<td><p><a href="multiplelocale.md" data-raw-source="[MultipleLocale](multiplelocale.md)">MultipleLocale</a>要素は、サービス メタデータ パッケージが複数のロケールをサポートしているかどうかを指定します。</p></td>
</tr>
</tbody>
</table>

 

## <a name="span-idparentelementsspanspan-idparentelementsspanspan-idparentelementsspanparent-elements"></a><span id="Parent_elements"></span><span id="parent_elements"></span><span id="PARENT_ELEMENTS"></span>親要素


<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>要素</th>
<th>説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><a href="packageinfo.md" data-raw-source="[PackageInfo](packageinfo.md)">PackageInfo</a></p></td>
<td><p><a href="packageinfo.md" data-raw-source="[PackageInfo](packageinfo.md)">PackageInfo</a>要素は、親要素の<a href="packageinfo-xml-schema.md" data-raw-source="[PackageInfo XML schema](packageinfo-xml-schema.md)">PackageInfo XML スキーマ</a>します。 PackageInfo の要素の子要素は、デバイス メタデータ パッケージの属性を指定します。</p></td>
</tr>
</tbody>
</table>

 

## <a name="span-idxsdspanspan-idxsdspanxsd"></a><span id="XSD"></span><span id="xsd"></span>XSD


``` syntax
<xs:element name="MetadataKey" type="tns:MetadataKeyType" />

<xs:complexType name="MetadataKeyType">
  <xs:sequence>
    <xs:choice>
      <xs:sequence>
       <xs:element name="HardwareIDList" type="tns:HardwareIDListType" />
       <xs:element name="ModelIDList" type="tns:ModelIDListType" minOccurs="0" />
      </xs:sequence>
      <xs:element name="ModelIDList" type="tns:ModelIDListType" />
    </xs:choice>
    <xs:element name="Locale" type="tns:LocaleType" />
    <xs:element name="LastModifiedDate" type="xs:dateTime" />
    <xs:element ref="v2:MultipleLocale" minOccurs="0" />
    <xs:any namespace="##other" processContents="lax" minOccurs="0" maxOccurs="unbounded" />
  </xs:sequence>
</xs:complexType>
```

PackageInfov2 XML スキーマのメタデータを次に示します。

``` syntax
<?xml version="1.0" encoding="UTF-8"?>

<xs:schema targetNamespace="http://schemas.microsoft.com/windows/2010/08/DeviceMetadata/PackageInfov2"
           xmlns:tns="http://schemas.microsoft.com/windows/2010/08/DeviceMetadata/PackageInfov2"
           xmlns:xs="http://www.w3.org/2001/XMLSchema"
           elementFormDefault="qualified"
           blockDefault="#all">

<xs:element name="MultipleLocale" type ="xs:boolean" />

</xs:schema>
```

## <a name="span-idremarksspanspan-idremarksspanspan-idremarksspanremarks"></a><span id="Remarks"></span><span id="remarks"></span><span id="REMARKS"></span>「解説」


MetadataKey 要素の子要素は、オペレーティング システムは、次の操作を使用してメタデータを指定します。

-   サービス メタデータ パッケージのいずれかに基づいて、デバイスのデバイスのメタデータ ストアを検索[ModelID](modelid.md)または[HardwareID](hardwareid.md)値。 オペレーティング システムを比較もメタデータ パッケージを 1 つ以上のデバイスのモデルまたはハードウェア ID が一致している場合、[ロケール](locale.md)ユーザーのコンピューターに現在の言語設定にメタデータ パッケージ内の値。

-   パッケージがあるより新しい場合、サービス メタデータ パッケージとデバイスのメタデータ ストアを更新[LastModifiedDate](lastmodifieddate.md)デバイス メタデータ ストア内の既存のパッケージよりも値。

MetadataKey 要素を含める必要があります。

-   1 つのインスタンス、[ロケール](locale.md)と[LastModifiedDate](lastmodifieddate.md)要素。

-   いずれか 1 つのインスタンス、 [HardwareIDList](hardwareidlist.md)または[ModelIDList](modelidlist.md)要素。 MetadataKey 要素は、両方の要素の 1 つのインスタンスを含めることができます。

MetadataKey 要素が必要です。

 

 






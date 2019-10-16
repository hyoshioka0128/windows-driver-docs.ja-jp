---
title: MetadataKey
description: MetadataKey
ms.assetid: 1915db47-98bb-40f5-be3b-75e9af80f506
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8946fa983c1568129fe3dd9b2b082b444543c8d9
ms.sourcegitcommit: f017184b00f59b088df87a5bd85fec51b7aed8b2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/15/2019
ms.locfileid: "72323626"
---
# <a name="metadatakey"></a>MetadataKey

[!include[MBAE deprecation warning](mbae-deprecation-warning.md)]

MetadataKey 要素は、サービスメタデータパッケージの属性を指定します。 これには次のものがあります。

-   デバイスでサポートされている各ハードウェア機能の識別子。

-   パッケージ内のテキスト文字列の言語固有のロケール。

## <a name="span-idusagespanspan-idusagespanspan-idusagespanusage"></a><span id="Usage"></span><span id="usage"></span><span id="USAGE"></span>ユーセジリンク


``` syntax
<MetadataKey>
  child elements
</MetadataKey>
```

## <a name="span-idattributesspanspan-idattributesspanspan-idattributesspanattributes"></a><span id="Attributes"></span><span id="attributes"></span><span id="ATTRIBUTES"></span>アトリビュート


属性はありません。

## <a name="span-idchild_elementsspanspan-idchild_elementsspanspan-idchild_elementsspanchild-elements"></a><span id="Child_elements"></span><span id="child_elements"></span><span id="CHILD_ELEMENTS"></span>子要素


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
<td><p><a href="hardwareidlist.md" data-raw-source="[HardwareIDList](hardwareidlist.md)">ハードウェア Id リスト</a></p></td>
<td><p>Hardware <a href="hardwareidlist.md" data-raw-source="[HardwareIDList](hardwareidlist.md)">Idlist</a>要素は、デバイスに対して1つ以上のハードウェア id 文字列を指定します。</p></td>
</tr>
<tr class="even">
<td><p><a href="lastmodifieddate.md" data-raw-source="[LastModifiedDate](lastmodifieddate.md)">LastModifiedDate</a></p></td>
<td><p><a href="lastmodifieddate.md" data-raw-source="[LastModifiedDate](lastmodifieddate.md)">LastModifiedDate</a>要素は、サービスメタデータパッケージが最後に変更されたタイムスタンプを指定します。</p></td>
</tr>
<tr class="odd">
<td><p><a href="locale.md" data-raw-source="[Locale](locale.md)">国</a></p></td>
<td><p><a href="locale.md" data-raw-source="[Locale](locale.md)">Locale</a>要素は、サービスメタデータパッケージのローカライズされたバージョンを指定します。</p></td>
</tr>
<tr class="even">
<td><p><a href="modelidlist.md" data-raw-source="[ModelIDList](modelidlist.md)">ModelIDList</a></p></td>
<td><p><a href="modelidlist.md" data-raw-source="[ModelIDList](modelidlist.md)">Modelidlist</a>要素は、サービスメタデータパッケージ内に指定されている各デバイスの種類またはモデルの GUID を指定します。</p></td>
</tr>
<tr class="odd">
<td><p><a href="multiplelocale.md" data-raw-source="[MultipleLocale](multiplelocale.md)">多重ロケール</a></p></td>
<td><p>複数の<a href="multiplelocale.md" data-raw-source="[MultipleLocale](multiplelocale.md)">ロケール</a>要素は、サービスメタデータパッケージが複数のロケールをサポートするかどうかを指定します。</p></td>
</tr>
</tbody>
</table>

 

## <a name="span-idparent_elementsspanspan-idparent_elementsspanspan-idparent_elementsspanparent-elements"></a><span id="Parent_elements"></span><span id="parent_elements"></span><span id="PARENT_ELEMENTS"></span>親要素


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
<td><p><a href="packageinfo.md" data-raw-source="[PackageInfo](packageinfo.md)">Packageinfo</a>要素は、 <a href="packageinfo-xml-schema.md" data-raw-source="[PackageInfo XML schema](packageinfo-xml-schema.md)">packageinfo XML スキーマ</a>の親要素です。 PackageInfo 要素の子要素は、デバイスメタデータパッケージの属性を指定します。</p></td>
</tr>
</tbody>
</table>

 

## <a name="span-idxsdspanspan-idxsdspanxsd"></a><span id="XSD"></span><span id="xsd"></span>XSD.EXE


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

PackageInfov2 XML スキーマメタデータを次に示します。

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

## <a name="span-idremarksspanspan-idremarksspanspan-idremarksspanremarks"></a><span id="Remarks"></span><span id="remarks"></span><span id="REMARKS"></span>注釈


MetadataKey 要素の子要素は、次の操作を実行するためにオペレーティングシステムで使用されるメタデータを指定します。

-   デバイスの[Modelid](modelid.md)または[HardwareID](hardwareid.md)値に基づいて、サービスメタデータパッケージのデバイスメタデータストアを検索します。 複数のメタデータパッケージがデバイスのモデルまたはハードウェア ID と一致する場合、オペレーティングシステムでは、メタデータパッケージ内の[ロケール](locale.md)値と、ユーザーのコンピューターの現在の言語設定が比較されます。

-   デバイスメタデータストア内の既存のパッケージよりも新しい[LastModifiedDate](lastmodifieddate.md)値がパッケージに含まれている場合は、サービスメタデータパッケージを使用してデバイスメタデータストアを更新します。

MetadataKey 要素には以下が含まれている必要があります。

-   [Locale](locale.md)要素と[LastModifiedDate](lastmodifieddate.md)要素の1つのインスタンス。

-   [ハードウェア Id リスト](hardwareidlist.md)または[modelidlist](modelidlist.md)要素のいずれかのインスタンス。 MetadataKey 要素には、両方の要素のインスタンスを1つ含めることができます。

MetadataKey 要素が必要です。

 

 






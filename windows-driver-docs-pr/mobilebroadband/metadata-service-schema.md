---
title: メタデータ
description: メタデータ
ms.assetid: bab7803c-df1f-4282-a9d7-5536d30d00dc
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3fdd31bab9ea198ec707da98bcc99868f7646e66
ms.sourcegitcommit: f017184b00f59b088df87a5bd85fec51b7aed8b2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/15/2019
ms.locfileid: "72323673"
---
# <a name="metadata"></a>メタデータ

[!include[MBAE deprecation warning](mbae-deprecation-warning.md)]

Metadata 要素は、サービスメタデータパッケージで参照される XML スキーマの名前空間を指定します。

## <a name="span-idusagespanspan-idusagespanspan-idusagespanusage"></a><span id="Usage"></span><span id="usage"></span><span id="USAGE"></span>ユーセジリンク


``` syntax
<Metadata
  MetadataID = "xs:anyURI">
  text
</Metadata>
```

## <a name="span-idattributesspanspan-idattributesspanspan-idattributesspanattributes"></a><span id="Attributes"></span><span id="attributes"></span><span id="ATTRIBUTES"></span>アトリビュート


<table>
<colgroup>
<col width="25%" />
<col width="25%" />
<col width="25%" />
<col width="25%" />
</colgroup>
<thead>
<tr class="header">
<th>備わっている</th>
<th>タスクバーの検索ボックスに</th>
<th>必須かどうか</th>
<th>説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>MetadataID</p></td>
<td><p>xs: anyURI</p></td>
<td><p>[はい]</p></td>
<td><p>サービスメタデータパッケージ内で参照される XML スキーマの名前空間を指定します。</p></td>
</tr>
</tbody>
</table>

 

## <a name="span-idtext_valuespanspan-idtext_valuespanspan-idtext_valuespantext-value"></a><span id="Text_value"></span><span id="text_value"></span><span id="TEXT_VALUE"></span>テキスト値


サービスメタデータ XML スキーマの名前空間の Uniform Resource Identifier (URI)。 XML スキーマは、サービスメタデータパッケージ内で参照されているスキーマのいずれかである必要があります。

## <a name="span-idchild_elementsspanspan-idchild_elementsspanspan-idchild_elementsspanchild-elements"></a><span id="Child_elements"></span><span id="child_elements"></span><span id="CHILD_ELEMENTS"></span>子要素


子要素はありません。

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
<td><p><a href="packagestructure.md" data-raw-source="[PackageStructure](packagestructure.md)">PackageStructure</a></p></td>
<td><p><a href="packagestructure.md" data-raw-source="[PackageStructure](packagestructure.md)">Packagestructure</a>要素は、サービスメタデータパッケージによって参照される XML スキーマを指定します。</p></td>
</tr>
</tbody>
</table>

 

## <a name="span-idxsdspanspan-idxsdspanxsd"></a><span id="XSD"></span><span id="xsd"></span>XSD.EXE


``` syntax
<xs:element name="PackageStructure" type="tns:PackageStructureType" />

<xs:complexType name="PackageStructureType">
   <xs:sequence>
     <xs:element name="Metadata" type="tns:MetadataType" minOccurs="3" maxOccurs="unbounded" />
   </xs:sequence>
</xs:complexType>

<xs:complexType name="MetadataType">
  <xs:simpleContent>
    <xs:extension base="xs:string">
      <xs:attribute name="MetadataID" type="xs:anyURI" use="required" />
    </xs:extension>
  </xs:simpleContent>
</xs:complexType>
```

## <a name="span-idremarksspanspan-idremarksspanspan-idremarksspanremarks"></a><span id="Remarks"></span><span id="remarks"></span><span id="REMARKS"></span>注釈


[Packageinfo](packageinfo.md)要素では、メタデータ要素の少なくとも2つのインスタンスを指定する必要があります。 各インスタンスでは、サービスメタデータパッケージの作成に使用される次の必要な XML スキーマのいずれかの名前空間を指定する必要があります。

-   [PackageInfo XML スキーマ](packageinfo-xml-schema.md)

-   [ServiceInfo XML スキーマ](serviceinfo-xml-schema.md)

-   [WindowsInfo XML スキーマ](windowsinfo-xml-schema.md)

-   [ソフトウェア情報 XML スキーマ](softwareinfo-xml-schema.md)

最も簡単な方法は、上記の例を Packageinfo .xml ファイルにコピーすることです。 上で指定したフォルダーのいずれかがサービスメタデータパッケージに含まれていない場合は、 [Packagestructure](packagestructure.md)要素からメタデータ要素を削除してください。

``` syntax
<PackageStructure>
  <Metadata MetadataID="http://schemas.microsoft.com/windows/DeviceMetadata/PackageInfo/2007/11">PackageInfo.xml</Metadata>
  <Metadata MetadataID="http://schemas.microsoft.com/windows/2010/05/DeviceMetadata/ServiceInfo">ServiceInformation</Metadata>
  <Metadata MetadataID="http://schemas.microsoft.com/windows/DeviceMetadata/WindowsInfo/2007/11/">WindowsInformation</Metadata>
  <Metadata MetadataID="http://schemas.microsoft.com/windows/2010/08/DeviceMetadata/SoftwareInfo">SoftwareInformation</Metadata>
</PackageStructure>
```

ソフトウェア情報フォルダーとサービスメタデータパッケージは、Windows 7 を実行しているデバイスではサポートされていません。

このメタデータ要素で名前が設定されていれば、各フォルダー名を任意の名前に変更できます。 次の例は、"WindowsInfo" をフォルダー名として使用する方法を示しています。

``` syntax
<Metadata MetadataID="http://schemas.microsoft.com/windows/DeviceMetadata/WindowsInfo/2007/11/">WindowsInfo</Metadata>
```

 

 






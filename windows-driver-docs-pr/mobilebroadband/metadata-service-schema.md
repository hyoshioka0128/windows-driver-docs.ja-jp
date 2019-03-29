---
title: メタデータ
description: メタデータ
ms.assetid: bab7803c-df1f-4282-a9d7-5536d30d00dc
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3fdd31bab9ea198ec707da98bcc99868f7646e66
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56581440"
---
# <a name="metadata"></a>メタデータ

[!include[MBAE deprecation warning](mbae-deprecation-warning.md)]

メタデータ要素は、サービス メタデータ パッケージで参照される XML スキーマの名前空間を指定します。

## <a name="span-idusagespanspan-idusagespanspan-idusagespanusage"></a><span id="Usage"></span><span id="usage"></span><span id="USAGE"></span>使用状況


``` syntax
<Metadata
  MetadataID = "xs:anyURI">
  text
</Metadata>
```

## <a name="span-idattributesspanspan-idattributesspanspan-idattributesspanattributes"></a><span id="Attributes"></span><span id="attributes"></span><span id="ATTRIBUTES"></span>属性


<table>
<colgroup>
<col width="25%" />
<col width="25%" />
<col width="25%" />
<col width="25%" />
</colgroup>
<thead>
<tr class="header">
<th>属性</th>
<th>型</th>
<th>必須</th>
<th>説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>MetadataID</p></td>
<td><p>xs:anyURI</p></td>
<td><p>はい</p></td>
<td><p>サービス メタデータ パッケージ内で参照されている XML スキーマの名前空間を指定します。</p></td>
</tr>
</tbody>
</table>

 

## <a name="span-idtextvaluespanspan-idtextvaluespanspan-idtextvaluespantext-value"></a><span id="Text_value"></span><span id="text_value"></span><span id="TEXT_VALUE"></span>テキスト値


(URI) のサービス メタデータの XML スキーマの名前空間。 XML スキーマには、サービス メタデータ パッケージ内で参照されるスキーマのいずれかを指定する必要があります。

## <a name="span-idchildelementsspanspan-idchildelementsspanspan-idchildelementsspanchild-elements"></a><span id="Child_elements"></span><span id="child_elements"></span><span id="CHILD_ELEMENTS"></span>子要素


子要素はありません。

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
<td><p><a href="packagestructure.md" data-raw-source="[PackageStructure](packagestructure.md)">PackageStructure</a></p></td>
<td><p><a href="packagestructure.md" data-raw-source="[PackageStructure](packagestructure.md)">PackageStructure</a>要素は、サービス メタデータ パッケージによって参照される XML スキーマを指定します。</p></td>
</tr>
</tbody>
</table>

 

## <a name="span-idxsdspanspan-idxsdspanxsd"></a><span id="XSD"></span><span id="xsd"></span>XSD


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


[PackageInfo](packageinfo.md)要素では、2 つの要素を指定する必要がありますメタデータ インスタンスの最小値。 各インスタンスは、サービス メタデータ パッケージの作成に使用される次の必要な XML スキーマのいずれかの名前空間を指定する必要があります。

-   [PackageInfo の XML スキーマ](packageinfo-xml-schema.md)

-   [ServiceInfo XML スキーマ](serviceinfo-xml-schema.md)

-   [WindowsInfo XML スキーマ](windowsinfo-xml-schema.md)

-   [SoftwareInfo XML スキーマ](softwareinfo-xml-schema.md)

最も簡単な方法では、Packageinfo.xml ファイルに次の例をコピーします。 サービス メタデータ パッケージに含まれていない上記で指定したフォルダーのいずれかの場合は、メタデータ要素を削除することを確認してください、 [PackageStructure](packagestructure.md)要素。

``` syntax
<PackageStructure>
  <Metadata MetadataID="http://schemas.microsoft.com/windows/DeviceMetadata/PackageInfo/2007/11">PackageInfo.xml</Metadata>
  <Metadata MetadataID="http://schemas.microsoft.com/windows/2010/05/DeviceMetadata/ServiceInfo">ServiceInformation</Metadata>
  <Metadata MetadataID="http://schemas.microsoft.com/windows/DeviceMetadata/WindowsInfo/2007/11/">WindowsInformation</Metadata>
  <Metadata MetadataID="http://schemas.microsoft.com/windows/2010/08/DeviceMetadata/SoftwareInfo">SoftwareInformation</Metadata>
</PackageStructure>
```

SoftwareInformation フォルダーとサービス メタデータ パッケージは、Windows 7 を実行するデバイスではサポートされません。

各フォルダー名は、このメタデータ要素の名前が設定されている限り、任意の名前に変更できます。 次の例では、フォルダー名として"WindowsInfo"を使用する方法を示します。

``` syntax
<Metadata MetadataID="http://schemas.microsoft.com/windows/DeviceMetadata/WindowsInfo/2007/11/">WindowsInfo</Metadata>
```

 

 






---
title: ServiceInfo
description: ServiceInfo
ms.assetid: 0dab9e5b-122c-4fe4-9314-97a0531af4aa
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: dd4647a85856ed7d60cc5b6ae70348c9fe598cfb
ms.sourcegitcommit: f017184b00f59b088df87a5bd85fec51b7aed8b2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/15/2019
ms.locfileid: "72323719"
---
# <a name="serviceinfo"></a>ServiceInfo

[!include[MBAE deprecation warning](mbae-deprecation-warning.md)]

ServiceInfo 要素は、 [SERVICEINFO XML スキーマ](serviceinfo-xml-schema.md)の親要素です。

## <a name="span-idusagespanspan-idusagespanspan-idusagespanusage"></a><span id="Usage"></span><span id="usage"></span><span id="USAGE"></span>ユーセジリンク


``` syntax
<ServiceInfo>
  child elements
</ServiceInfo>
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
<td><p><a href="servicecategorylist.md" data-raw-source="[ServiceCategoryList](servicecategorylist.md)">ServiceCategoryList</a></p></td>
<td><p>サービスに適用される1つ以上の機能カテゴリを指定します。</p></td>
</tr>
<tr class="even">
<td><p><a href="servicename.md" data-raw-source="[ServiceName](servicename.md)">ServiceName</a></p></td>
<td><p>使用しません。</p></td>
</tr>
<tr class="odd">
<td><p><a href="servicedescription1.md" data-raw-source="[ServiceDescription1](servicedescription1.md)">ServiceDescription1</a></p></td>
<td><p>サービスに関する説明情報を指定します。 これは、ワイヤレスワイドエリアネットワーク (WWAN) 接続プロファイルの [説明] フィールドに適用されます。 エンドユーザーへのユーザーインターフェイスには表示されません。</p></td>
</tr>
<tr class="even">
<td><p><a href="servicedescription2.md" data-raw-source="[ServiceDescription2](servicedescription2.md)">ServiceDescription2</a></p></td>
<td><p>使用しません。</p></td>
</tr>
<tr class="odd">
<td><p><a href="servicenumber.md" data-raw-source="[ServiceNumber](servicenumber.md)">ServiceNumber</a></p></td>
<td><p>これは、このパッケージを送信しているオペレーターを識別する、自己生成された GUID です。</p></td>
</tr>
<tr class="even">
<td><p><a href="serviceprovider.md" data-raw-source="[ServiceProvider](serviceprovider.md)">ServiceProvider</a></p></td>
<td><p>これは、Windows 接続マネージャーにホームネットワークの表示名として表示されます。</p></td>
</tr>
<tr class="odd">
<td><p><a href="serviceiconfile.md" data-raw-source="[ServiceIconFile](serviceiconfile.md)">ServiceIconFile</a></p></td>
<td><p>サービスメタデータパッケージ内のサービスアイコンファイルの名前を指定します。</p>
<div class="alert">
<strong>注:</strong><br/><p>スキーマでは、省略可能として表示されます。 ただし、パッケージが Windows デベロッパーセンターのダッシュボードに送信されたときに検証を成功させるために必要です。</p>
</div>
<div>

</div></td>
</tr>
<tr class="even">
<td><p><a href="servicespecificextension.md" data-raw-source="[ServiceSpecificExtension](servicespecificextension.md)">ServiceSpecificExtension</a></p></td>
<td><p>この ServiceCategory に固有のファイルの場所を参照します。 Windows 8、Windows 8.1、または Windows 10 for desktop edition (Home、Pro、Enterprise、および教育) のサービスメタデータパッケージの場合、これは MobileBroadbandInfo の場所です。</p></td>
</tr>
</tbody>
</table>



## <a name="span-idparent_elementsspanspan-idparent_elementsspanspan-idparent_elementsspanparent-elements"></a><span id="Parent_elements"></span><span id="parent_elements"></span><span id="PARENT_ELEMENTS"></span>親要素


親要素はありません。

## <a name="span-idxsdspanspan-idxsdspanxsd"></a><span id="XSD"></span><span id="xsd"></span>XSD.EXE


``` syntax
<xs:element name="ServiceInfo" type="tns:ServiceInfoType" />

<xs:complexType name="ServiceInfoType">
  <xs:sequence>
    <xs:element name="ServiceCategoryList" type="tns:ServiceCategoryListType" />
    <xs:element name="ServiceName" type="tns:ServiceNameType" minOccurs="0" />
    <xs:element name="ServiceDescription1" type="tns:ServiceDescriptionType" minOccurs="0" />
    <xs:element name="ServiceDescription2" type="tns:ServiceDescriptionType" minOccurs="0" />
    <xs:element name="ServiceNumber" type ="tns:ServiceNumberType" />
    <xs:element name="ServiceProvider" type="tns:ProviderNameType" />
    <xs:element name="ServiceIconFile" type="tns:ServiceIconFileType" minOccurs="0" />
    <xs:element name="ServiceSpecificExtension" type="tns:ServiceSpecificExtensionType" minOccurs="0" />
    <xs:any namespace="##other" processContents="lax" minOccurs="0" maxOccurs="unbounded" />
  </xs:sequence>
</xs:complexType>
```

## <a name="span-idremarksspanspan-idremarksspanspan-idremarksspanremarks"></a><span id="Remarks"></span><span id="remarks"></span><span id="REMARKS"></span>注釈


ServiceInfo 要素には、 [ServiceCategoryList](servicecategorylist.md)、 [ServiceNumber](servicenumber.md)、 [ServiceProvider](serviceprovider.md)、および[ServiceSpecificExtension](servicespecificextension.md)の各要素のインスタンスが1つ含まれている必要があります。

ServiceInfo 要素が必要です。










---
title: MobileBroadbandInfo
description: MobileBroadbandInfo
ms.assetid: 02279e23-becd-49ef-8981-6afb8e5aab91
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9ccc1f6d2f6a5ea11161dcdbc82e5e1d57b4ae8e
ms.sourcegitcommit: f017184b00f59b088df87a5bd85fec51b7aed8b2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/15/2019
ms.locfileid: "72323667"
---
# <a name="mobilebroadbandinfo"></a>MobileBroadbandInfo

[!include[MBAE deprecation warning](mbae-deprecation-warning.md)]

MobileBroadbandInfo 要素は、 [MOBILEBROADBANDINFO XML スキーマ](mobilebroadbandinfo-xml-schema.md)の親要素です。

## <a name="span-idusagespanspan-idusagespanspan-idusagespanusage"></a><span id="Usage"></span><span id="usage"></span><span id="USAGE"></span>ユーセジリンク


``` syntax
<MobileBroadbandInfo>
  child elements
</MobileBroadbandInfo>
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
<td><p><a href="networkconfiguration.md" data-raw-source="[NetworkConfiguration](networkconfiguration.md)">NetworkConfiguration</a></p></td>
<td><p><a href="networkconfiguration.md" data-raw-source="[NetworkConfiguration](networkconfiguration.md)">NetworkConfiguration</a>要素は、使用する購入およびインターネットモバイルブロードバンドプロファイルを指定します。</p></td>
</tr>
<tr class="even">
<td><p><a href="provisioningengine.md" data-raw-source="[ProvisioningEngine](provisioningengine.md)">プロビジョニングエンジン</a></p></td>
<td><p><a href="provisioningengine.md" data-raw-source="[ProvisioningEngine](provisioningengine.md)">プロビジョニングエンジン</a>要素は、サブジェクト名と発行者名に対して信頼された証明書の値を指定します。</p></td>
</tr>
</tbody>
</table>

 

## <a name="span-idparent_elementsspanspan-idparent_elementsspanspan-idparent_elementsspanparent-elements"></a><span id="Parent_elements"></span><span id="parent_elements"></span><span id="PARENT_ELEMENTS"></span>親要素


親要素はありません。

## <a name="span-idxsdspanspan-idxsdspanxsd"></a><span id="XSD"></span><span id="xsd"></span>XSD.EXE


``` syntax
<xs:element name="MobileBroadbandInfo" type="tns:MobileBroadbandInfoType" />

<xs:complexType name="MobileBroadbandInfoType">
  <xs:sequence>
    <xs:element name="NetworkConfiguration" type="tns:NetworkConfigType" minOccurs="0" />
    <xs:element name="ProvisioningEngine" type="tns:ProvisioningEngineType" minOccurs="0" />
    <xs:any namespace="##other" processContents="lax" minOccurs="0" maxOccurs="unbounded" />
  </xs:sequence>
</xs:complexType>
```

## <a name="span-idremarksspanspan-idremarksspanspan-idremarksspanremarks"></a><span id="Remarks"></span><span id="remarks"></span><span id="REMARKS"></span>注釈


MobileBroadbandInfo 要素が必要です。

 

 






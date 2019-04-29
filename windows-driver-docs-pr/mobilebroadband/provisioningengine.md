---
title: ProvisioningEngine
description: ProvisioningEngine
ms.assetid: b6b10145-d554-43be-8682-1355145b3241
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 49ce5c65436e9da9d14496c32ec90b32b007bbcd
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63335272"
---
# <a name="provisioningengine"></a>ProvisioningEngine

[!include[MBAE deprecation warning](mbae-deprecation-warning.md)]

ProvisioningEngine 要素には、信頼された証明書を指定します。 これにより、信頼された証明書で署名されているパッケージを使用した PC をプロビジョニングします。

プロビジョニングの詳細については、次を参照してください。[アカウント プロビジョニング](account-provisioning.md)します。

## <a name="span-idusagespanspan-idusagespanspan-idusagespanusage"></a><span id="Usage"></span><span id="usage"></span><span id="USAGE"></span>使用状況


``` syntax
<ProvisioningEngine>
  child element
</ProvisioningEngine>
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
<td><p><a href="trustedcertificates.md" data-raw-source="[TrustedCertificates](trustedcertificates.md)">TrustedCertificates</a></p></td>
<td><p>信頼された証明書を指定します。</p></td>
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
<td><p><a href="mobilebroadbandinfo.md" data-raw-source="[MobileBroadbandInfo](mobilebroadbandinfo.md)">MobileBroadbandInfo</a></p></td>
<td><p><a href="mobilebroadbandinfo.md" data-raw-source="[MobileBroadbandInfo](mobilebroadbandinfo.md)">MobileBroadbandInfo</a>要素は、親要素の<a href="mobilebroadbandinfo-xml-schema.md" data-raw-source="[MobileBroadbandInfo XML schema](mobilebroadbandinfo-xml-schema.md)">MobileBroadbandInfo XML スキーマ</a>します。</p></td>
</tr>
</tbody>
</table>

 

## <a name="span-idxsdspanspan-idxsdspanxsd"></a><span id="XSD"></span><span id="xsd"></span>XSD


``` syntax
<xs:element name="ProvisioningEngine" type="tns:ProvisioningEngineType" minOccurs="0" />

<xs:complexType name="ProvisioningEngineType">
  <xs:sequence>
    <xs:element name="TrustedCertificates" type="tns:TrustedCertificateListType" minOccurs="0" />
    <xs:any namespace="##other" processContents="lax" minOccurs="0" maxOccurs="unbounded" />
  </xs:sequence>
</xs:complexType>
```

## <a name="span-idremarksspanspan-idremarksspanspan-idremarksspanremarks"></a><span id="Remarks"></span><span id="remarks"></span><span id="REMARKS"></span>注釈


-   Windows 8、Windows 8.1、および Windows 10 は、プロビジョニング パッケージと呼ばれる、ユーザーのモバイル ブロード バンド ネットワーク設定を更新するパッケージを提供するモバイル ネットワーク オペレーターを許可します。

-   プロビジョニング パッケージがモバイル ネットワーク オペレーターから取得して、Windows では、プロビジョニング パッケージの署名に使用される証明書からサブジェクト名と発行者の名前と一致するサービス メタデータ パッケージに記載されている内容を確認します。

ProvisioningEngine 要素は省略可能です。

 

 






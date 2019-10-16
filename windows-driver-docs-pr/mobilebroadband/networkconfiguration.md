---
title: NetworkConfiguration
description: NetworkConfiguration
ms.assetid: 4a52b185-1bfb-4626-99fb-6be364e88e85
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: cb69630c124c238fa920e45d1d87f1e4fc2cd687
ms.sourcegitcommit: f017184b00f59b088df87a5bd85fec51b7aed8b2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/15/2019
ms.locfileid: "72323695"
---
# <a name="networkconfiguration"></a>NetworkConfiguration

[!include[MBAE deprecation warning](mbae-deprecation-warning.md)]

NetworkConfiguration 要素は、使用する購入およびインターネットモバイルブロードバンドプロファイルを指定します。 この要素で参照されるファイルは、 **Serviceinformation**ディレクトリに含まれる必要があります。 これらのファイルは、ユーザーをオペレーターのネットワークに接続する際に役立ちます。 また、標準ユーザーがモバイルブロードバンド SIMs で PIN のロック解除操作を実行できるようにするかどうかも指定します。

## <a name="span-idusagespanspan-idusagespanspan-idusagespanusage"></a><span id="Usage"></span><span id="usage"></span><span id="USAGE"></span>ユーセジリンク


``` syntax
<NetworkConfiguration>
  child elements
</NetworkConfiguration>
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
<td><p><a href="mobilebroadbandprofiles.md" data-raw-source="[MobileBroadbandProfiles](mobilebroadbandprofiles.md)">MobileBroadbandProfiles</a></p></td>
<td><p>使用する購入およびインターネットモバイルブロードバンドプロファイルを指定します。</p></td>
</tr>
<tr class="even">
<td><p><a href="allowstandarduserpinunlock.md" data-raw-source="[AllowStandardUserPinUnlock](allowstandarduserpinunlock.md)">AllowStandardUserPinUnlock</a></p></td>
<td><p>標準ユーザーがモバイルブロードバンド SIMs で PIN のロック解除操作を実行できるようにするかどうかを指定します。</p></td>
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
<td><p><a href="mobilebroadbandinfo.md" data-raw-source="[MobileBroadbandInfo](mobilebroadbandinfo.md)">MobileBroadbandInfo</a></p></td>
<td><p><a href="mobilebroadbandinfo.md" data-raw-source="[MobileBroadbandInfo](mobilebroadbandinfo.md)">MobileBroadbandInfo</a>要素は、 <a href="mobilebroadbandinfo-xml-schema.md" data-raw-source="[MobileBroadbandInfo XML schema](mobilebroadbandinfo-xml-schema.md)">MobileBroadbandInfo XML スキーマ</a>の親要素です。</p></td>
</tr>
</tbody>
</table>

 

## <a name="span-idxsdspanspan-idxsdspanxsd"></a><span id="XSD"></span><span id="xsd"></span>XSD.EXE


``` syntax
<xs:element name="NetworkConfiguration" type="tns:NetworkConfigType" minOccurs="0" />

<xs:complexType name="NetworkConfigType">
  <xs:sequence>
    <xs:element name="MobileBroadbandProfiles" type="tns:MobileBroadbandProfilesType" minOccurs="0" />
    <xs:element name="AllowStandardUserPinUnlock" type="xs:boolean" minOccurs="0" />
    <xs:any namespace="##other" processContents="lax" minOccurs="0" maxOccurs="unbounded" />
  </xs:sequence>
</xs:complexType>
```

## <a name="span-idremarksspanspan-idremarksspanspan-idremarksspanremarks"></a><span id="Remarks"></span><span id="remarks"></span><span id="REMARKS"></span>注釈


-   プランの購入 APN またはインターネット接続 APN を設定するには、モバイルネットワークオペレーター (MNO) が、この要素の一部としてこれらの状態に対応する XML プロファイルを指定する必要があります。

-   この要素の子要素は省略可能です。 これらが指定されていない場合は、Windows に含まれている APN データベースからの APN 値が、ユーザーの接続を支援するために使用されます。

-   通常、モバイルブロードバンド SIMs で PIN のロック解除操作を実行できるのは、Administrators セキュリティグループのユーザーだけです。 ただし、 [Allowstandarduserpinunlock](allowstandarduserpinunlock.md)要素を true に設定すると、モバイルオペレーターは、標準ユーザーがこの機能を実行できるかどうかを指定できます。

 

 






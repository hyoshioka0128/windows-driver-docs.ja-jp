---
title: NetworkConfiguration
description: NetworkConfiguration
ms.assetid: 4a52b185-1bfb-4626-99fb-6be364e88e85
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: cb69630c124c238fa920e45d1d87f1e4fc2cd687
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56580593"
---
# <a name="networkconfiguration"></a>NetworkConfiguration

[!include[MBAE deprecation warning](mbae-deprecation-warning.md)]

NetworkConfiguration 要素は、購入および使用する、インターネット モバイル ブロード バンドのプロファイルを指定します。 この要素で参照されるファイルに含めるか、 **ServiceInformation**ディレクトリ。 これらのファイルは、オペレーターのネットワークに接続しているユーザーの取得に役立ちます。 また、PIN、モバイル ブロード バンド Sim に対する操作のロックを解除標準ユーザーによって実行できるかどうかを指定します。

## <a name="span-idusagespanspan-idusagespanspan-idusagespanusage"></a><span id="Usage"></span><span id="usage"></span><span id="USAGE"></span>使用状況


``` syntax
<NetworkConfiguration>
  child elements
</NetworkConfiguration>
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
<td><p><a href="mobilebroadbandprofiles.md" data-raw-source="[MobileBroadbandProfiles](mobilebroadbandprofiles.md)">MobileBroadbandProfiles</a></p></td>
<td><p>購入および使用する、インターネット モバイル ブロード バンドのプロファイルを指定します。</p></td>
</tr>
<tr class="even">
<td><p><a href="allowstandarduserpinunlock.md" data-raw-source="[AllowStandardUserPinUnlock](allowstandarduserpinunlock.md)">AllowStandardUserPinUnlock</a></p></td>
<td><p>暗証番号 (pin)、モバイル ブロード バンド Sim に対する操作のロックを解除標準ユーザーによって実行できるかどうかを指定します。</p></td>
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


-   プランの購入を設定するために APN またはインターネット接続 APN、モバイル ネットワーク オペレーター (MNO) する必要があります指定この要素の一部としてこれらの状態に対応する XML プロファイルします。

-   この要素の子要素は省略可能です。 これらが指定されていない場合に含まれる Windows APN データベースから APN 値は、ユーザーが接続するために使用されます。

-   通常、暗証番号 (pin) を実行するセキュリティ グループが許可されている管理者のユーザーのみがモバイル ブロード バンド Sim に対する操作のロックを解除します。 ただし、設定、 [AllowStandardUserPinUnlock](allowstandarduserpinunlock.md)を true に要素が標準ユーザーがこの機能を実行できるかどうかを指定する携帯電話会社を使用します。

 

 






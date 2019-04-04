---
title: ModelIDList
description: ModelIDList
ms.assetid: b7c6a100-95bf-421c-9a84-71623c0276fe
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a560e4137f11615fed5a529ce0fcbf9f5dd50b5b
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56574568"
---
# <a name="modelidlist"></a>ModelIDList

[!include[MBAE deprecation warning](mbae-deprecation-warning.md)]

ModelIDList 要素には、1 つまたは複数の Guid を指定します。 使用して各 GUID を指定する[ModelID](modelid.md)要素、デバイス メタデータ パッケージ内で指定された物理デバイスを識別します。

**注意**   、ModelIDList と[ModelID](modelid.md)サービス メタデータ パッケージの要素はサポートされていません。 使用する必要があります、 [HardwareIDList](hardwareidlist.md)と[HardwareID](hardwareid.md)要素代わりにします。

 

## <a name="span-idusagespanspan-idusagespanspan-idusagespanusage"></a><span id="Usage"></span><span id="usage"></span><span id="USAGE"></span>使用状況


``` syntax
<ModelIDList>
  child elements
</ModelIDList>
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
<td><p><a href="modelid.md" data-raw-source="[ModelID](modelid.md)">ModelID</a></p></td>
<td><p><a href="modelid.md" data-raw-source="[ModelID](modelid.md)">ModelID</a>要素は、物理デバイスの GUID を指定します。</p></td>
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
<td><p><a href="metadatakey.md" data-raw-source="[MetadataKey](metadatakey.md)">MetadataKey</a></p></td>
<td><p><a href="metadatakey.md" data-raw-source="[MetadataKey](metadatakey.md)">MetadataKey</a>要素は、デバイス メタデータ パッケージの属性を指定します。 これには次のものがあります。</p>
<ul>
<li><p>デバイスでサポートされている各ハードウェア関数の識別子。</p></li>
<li><p>言語固有のロケールをパッケージ内のテキスト文字列。</p></li>
</ul></td>
</tr>
</tbody>
</table>

 

## <a name="span-idxsdspanspan-idxsdspanxsd"></a><span id="XSD"></span><span id="xsd"></span>XSD


``` syntax
<xs:element name="ModelIDList" type="tns:ModelIDListType" minOccurs="0" />

<xs:complexType name="ModelIDListType">
  <xs:sequence>
    <xs:element name="ModelID" type="tns:GUIDType" maxOccurs="unbounded" />
  </xs:sequence>
</xs:complexType>
```

## <a name="span-idremarksspanspan-idremarksspanspan-idremarksspanremarks"></a><span id="Remarks"></span><span id="remarks"></span><span id="REMARKS"></span>注釈


ModelIDList 要素は必要な場合にのみ、 [HardwareIDList](hardwareidlist.md)で要素が指定されていない、 [MetadataKey](metadatakey.md)要素。 ModelIDList 要素が 1 つ以上含める必要があります指定されている場合[ModelID](modelid.md)要素。 デバイス メタデータ パッケージは、複数のデバイス モデルやモデル Id をサポートする場合は、各デバイス モデルの ModelID 要素を指定できます。

**注意**   、ModelIDList と[ModelID](modelid.md)サービス メタデータ パッケージの要素はサポートされていません。 使用する必要があります、 [HardwareIDList](hardwareidlist.md)と[HardwareID](hardwareid.md)要素代わりにします。

 

PackageInfo の XML データには、両方が含まれている場合、 [HardwareIDList](hardwareidlist.md) ModelIDList 要素では、オペレーティング システムを使用して、次の規則のデバイスがデバイス メタデータ パッケージで指定されたかどうかを決定する場合。

-   デバイスにモデル ID がある場合は、オペレーティング システムが内の一致を検索しません、 [HardwareIDList](hardwareidlist.md)要素。 モデル Id の詳細については、[ModelID](modelid.md)を参照してください。

-   オペレーティング システムをそれ以外の場合、検索、 [HardwareIDList](hardwareidlist.md)デバイスのハードウェア ID と一致する要素

 

 






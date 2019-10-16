---
title: ModelIDList
description: ModelIDList
ms.assetid: b7c6a100-95bf-421c-9a84-71623c0276fe
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a560e4137f11615fed5a529ce0fcbf9f5dd50b5b
ms.sourcegitcommit: f017184b00f59b088df87a5bd85fec51b7aed8b2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/15/2019
ms.locfileid: "72323663"
---
# <a name="modelidlist"></a>ModelIDList

[!include[MBAE deprecation warning](mbae-deprecation-warning.md)]

ModelIDList 要素は、1つまたは複数の Guid を指定します。 各 GUID は、 [Modelid](modelid.md)要素によって指定され、デバイスメタデータパッケージ内で指定された物理デバイスを識別します。

**注意**   ModelIDList と[modelid](modelid.md)の要素は、サービスメタデータパッケージではサポートされていません。 代わりに、[ハードウェア Id リスト](hardwareidlist.md)と[HardwareID](hardwareid.md)要素を使用する必要があります。

 

## <a name="span-idusagespanspan-idusagespanspan-idusagespanusage"></a><span id="Usage"></span><span id="usage"></span><span id="USAGE"></span>ユーセジリンク


``` syntax
<ModelIDList>
  child elements
</ModelIDList>
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
<td><p><a href="modelid.md" data-raw-source="[ModelID](modelid.md)">ModelID</a></p></td>
<td><p><a href="modelid.md" data-raw-source="[ModelID](modelid.md)">Modelid</a>要素は、物理デバイスの GUID を指定します。</p></td>
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
<td><p><a href="metadatakey.md" data-raw-source="[MetadataKey](metadatakey.md)">MetadataKey</a></p></td>
<td><p><a href="metadatakey.md" data-raw-source="[MetadataKey](metadatakey.md)">Metadatakey</a>要素は、デバイスメタデータパッケージの属性を指定します。 これには次のものがあります。</p>
<ul>
<li><p>デバイスでサポートされている各ハードウェア機能の識別子。</p></li>
<li><p>パッケージ内のテキスト文字列の言語固有のロケール。</p></li>
</ul></td>
</tr>
</tbody>
</table>

 

## <a name="span-idxsdspanspan-idxsdspanxsd"></a><span id="XSD"></span><span id="xsd"></span>XSD.EXE


``` syntax
<xs:element name="ModelIDList" type="tns:ModelIDListType" minOccurs="0" />

<xs:complexType name="ModelIDListType">
  <xs:sequence>
    <xs:element name="ModelID" type="tns:GUIDType" maxOccurs="unbounded" />
  </xs:sequence>
</xs:complexType>
```

## <a name="span-idremarksspanspan-idremarksspanspan-idremarksspanremarks"></a><span id="Remarks"></span><span id="remarks"></span><span id="REMARKS"></span>注釈


ModelIDList 要素は、 [Metadatakey](metadatakey.md)要素では、[ハードウェア id リスト](hardwareidlist.md)要素が指定されていない場合にのみ必要です。 指定されている場合、ModelIDList 要素には1つ以上の[Modelid](modelid.md)要素が含まれている必要があります。 デバイスメタデータパッケージで複数のデバイスモデルまたはモデル Id がサポートされている場合は、各デバイスモデルに対して ModelID 要素を指定できます。

**注意**   ModelIDList と[modelid](modelid.md)の要素は、サービスメタデータパッケージではサポートされていません。 代わりに、[ハードウェア Id リスト](hardwareidlist.md)と[HardwareID](hardwareid.md)要素を使用する必要があります。

 

PackageInfo XML データ[に、デバイス](hardwareidlist.md)メタデータパッケージによってデバイスが指定されているかどうかを判断するときに、オペレーティングシステムは次の規則を使用します。

-   デバイスにモデル ID がある場合、オペレーティングシステムは、[ハードウェア Id リスト](hardwareidlist.md)の要素で一致を検索しません。 モデル Id の詳細については、「 [Modelid](modelid.md)」を参照してください。

-   それ以外の場合、オペレーティングでは、デバイスのハードウェア ID と一致するように、hardware [Idlist](hardwareidlist.md)要素が検索されます。

 

 






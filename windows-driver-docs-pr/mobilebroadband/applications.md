---
title: アプリケーション
description: アプリケーション
ms.assetid: 40d73650-556e-4221-a679-0b8e9ead4df5
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 780423013170b3ef1bf28e4a654ce5d0bc651e18
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56528323"
---
# <a name="applications"></a>アプリケーション

[!include[MBAE deprecation warning](mbae-deprecation-warning.md)]

アプリケーションの要素には、モバイル ブロード バンド ハードウェア デバイスに関連付けられているアプリを指定します。

## <a name="span-idusagespanspan-idusagespanspan-idusagespanusage"></a><span id="Usage"></span><span id="usage"></span><span id="USAGE"></span>使用状況


``` syntax
<Applications>
  Child element
</Applications>
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
<td><p><a href="application-softwareinfo-schema.md" data-raw-source="[Application](application-softwareinfo-schema.md)">アプリケーション</a></p></td>
<td><p>PC のオペレーターのモバイル ブロード バンド ハードウェアが検出されたときにダウンロードされるアプリを指定します。</p></td>
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
<td><p><a href="package.md" data-raw-source="[Package](package.md)">パッケージ</a></p></td>
<td><p>PC のオペレーターのモバイル ブロード バンド ハードウェアが検出されたときにダウンロードされるアプリを指定します。</p></td>
</tr>
</tbody>
</table>

 

## <a name="span-idxsdspanspan-idxsdspanxsd"></a><span id="XSD"></span><span id="xsd"></span>XSD


``` syntax
<xs:element name="Applications" type="tns:ApplicationsType" />

  <xs:complexType name="ApplicationsType">
    <xs:sequence>
      <xs:element name="Application" type="tns:ApplicationType" />
      <xs:any namespace="##other" processContents="lax" minOccurs="0" maxOccurs="unbounded" />
    </xs:sequence>
  </xs:complexType>
```

## <a name="span-idremarksspanspan-idremarksspanspan-idremarksspanremarks"></a><span id="Remarks"></span><span id="remarks"></span><span id="REMARKS"></span>「解説」


アプリケーションの要素は省略可能です。

 

 






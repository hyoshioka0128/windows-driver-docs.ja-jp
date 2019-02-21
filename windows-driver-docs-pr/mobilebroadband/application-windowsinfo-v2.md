---
title: アプリケーション (WindowsInfo)
description: アプリケーション (WindowsInfo)
ms.assetid: e76ede51-e494-47b4-b30a-e354799f66e7
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 180c28b9fb3717d6cbb2a1371146cb2adeb48b02
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56548590"
---
# <a name="application-windowsinfo"></a>アプリケーション (WindowsInfo)

[!include[MBAE deprecation warning](mbae-deprecation-warning.md)]

アプリケーションの要素には、アプリのアプリケーション ID を指定します。

## <a name="span-idusagespanspan-idusagespanspan-idusagespanusage"></a><span id="Usage"></span><span id="usage"></span><span id="USAGE"></span>使用状況


``` syntax
<Application Id=”tns:ApplicationIdType” />
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
<th>種類</th>
<th>必須</th>
<th>説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>ID</p></td>
<td><p>tns:ApplicationIdType</p></td>
<td><p>〇</p></td>
<td><p>アプリケーション id。 「解説」の説明に従って、アプリ マニフェストからこの値ををコピー.</p></td>
</tr>
</tbody>
</table>

 

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
<td><p><a href="autoplayhandler.md" data-raw-source="[AutoplayHandler](autoplayhandler.md)">AutoplayHandler</a></p></td>
<td><p>ユーザーはデバイスをプラグインと、推奨される自動再生操作として表示される UWP デバイス アプリを指定します。</p></td>
</tr>
</tbody>
</table>

 

## <a name="span-idxsdspanspan-idxsdspanxsd"></a><span id="XSD"></span><span id="xsd"></span>XSD


``` syntax
<xs:element name="Application" type="tns:ApplicationType" />

<xs:complexType name="ApplicationType">
  <xs:attribute name="Id" type="tns:ApplicationIdType" use="required"/>
</xs:complexType>

<xs:simpleType name="ApplicationIdType">
  <xs:restriction base="tns:AsciiWindowsIdType">
    <xs:maxLength value="64"/>
  </xs:restriction>
</xs:simpleType>
```

## <a name="span-idremarksspanspan-idremarksspanspan-idremarksspanremarks"></a><span id="Remarks"></span><span id="remarks"></span><span id="REMARKS"></span>「解説」


Application 要素の構造の構造に対応して、&lt;アプリケーション&gt;アプリ マニフェスト内の要素。 アプリ マニフェストの Id 属性から Id 値の値をコピーします。

方法の例を次に示します&lt;アプリケーション&gt;要素は、アプリケーション マニフェスト内で構造化する可能性があります。

``` syntax
<Applications>
  <Application Id="DeviceAppForPrinters" Executable="$targetnametoken$.exe" EntryPoint="DeviceAppForPrinters.App">
</Application>
</Applications>
```

アプリケーションの要素は省略可能です。

 

 






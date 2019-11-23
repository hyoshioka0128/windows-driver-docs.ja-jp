---
title: アプリケーション (WindowsInfo)
description: アプリケーション (WindowsInfo)
ms.assetid: e76ede51-e494-47b4-b30a-e354799f66e7
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 180c28b9fb3717d6cbb2a1371146cb2adeb48b02
ms.sourcegitcommit: f017184b00f59b088df87a5bd85fec51b7aed8b2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/15/2019
ms.locfileid: "72323639"
---
# <a name="application-windowsinfo"></a>アプリケーション (WindowsInfo)

[!include[MBAE deprecation warning](mbae-deprecation-warning.md)]

Application 要素は、アプリのアプリケーション ID を指定します。

## <a name="span-idusagespanspan-idusagespanspan-idusagespanusage"></a><span id="Usage"></span><span id="usage"></span><span id="USAGE"></span>ユーセジリンク


``` syntax
<Application Id=”tns:ApplicationIdType” />
```

## <a name="span-idattributesspanspan-idattributesspanspan-idattributesspanattributes"></a><span id="Attributes"></span><span id="attributes"></span><span id="ATTRIBUTES"></span>アトリビュート


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
<td><p>tns: ApplicationIdType</p></td>
<td><p>〇</p></td>
<td><p>アプリケーション ID。 「解説」で説明されているように、アプリケーションマニフェストからこの値をコピーします。</p></td>
</tr>
</tbody>
</table>

 

## <a name="span-idchild_elementsspanspan-idchild_elementsspanspan-idchild_elementsspanchild-elements"></a><span id="Child_elements"></span><span id="child_elements"></span><span id="CHILD_ELEMENTS"></span>子要素


子要素はありません。

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
<td><p><a href="autoplayhandler.md" data-raw-source="[AutoplayHandler](autoplayhandler.md)">AutoplayHandler</a></p></td>
<td><p>ユーザーがデバイスに接続するときに推奨される自動再生操作として表示する UWP デバイスアプリを指定します。</p></td>
</tr>
</tbody>
</table>

 

## <a name="span-idxsdspanspan-idxsdspanxsd"></a><span id="XSD"></span><span id="xsd"></span>XSD.EXE


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

## <a name="span-idremarksspanspan-idremarksspanspan-idremarksspanremarks"></a><span id="Remarks"></span><span id="remarks"></span><span id="REMARKS"></span>注釈


アプリケーション要素の構造体は、アプリケーションマニフェスト内の &lt;アプリケーション&gt; 要素の構造に対応します。 アプリマニフェストの Id 属性から Id 値の値をコピーします。

アプリマニフェスト内で &lt;Applications&gt; 要素を構造化する方法の例を次に示します。

``` syntax
<Applications>
  <Application Id="DeviceAppForPrinters" Executable="$targetnametoken$.exe" EntryPoint="DeviceAppForPrinters.App">
</Application>
</Applications>
```

Application 要素は省略可能です。

 

 






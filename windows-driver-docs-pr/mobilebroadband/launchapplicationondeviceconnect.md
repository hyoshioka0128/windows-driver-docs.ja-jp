---
title: LaunchApplicationOnDeviceConnect
description: LaunchApplicationOnDeviceConnect
ms.assetid: d8a5f20a-bd88-4279-9e15-4f20287edfd4
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: bc87de4188efa8cf52467c232c223ca80ed33c66
ms.sourcegitcommit: f017184b00f59b088df87a5bd85fec51b7aed8b2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/15/2019
ms.locfileid: "72323717"
---
# <a name="launchapplicationondeviceconnect"></a>LaunchApplicationOnDeviceConnect

[!include[MBAE deprecation warning](mbae-deprecation-warning.md)]

LaunchApplicationOnDeviceConnect 要素は、ユーザーがデバイスに接続したときに推奨される自動再生アクションとして表示されるアプリを指定します。

## <a name="span-idusagespanspan-idusagespanspan-idusagespanusage"></a><span id="Usage"></span><span id="usage"></span><span id="USAGE"></span>ユーセジリンク


``` syntax
<LaunchApplicationOnDeviceConnect>
  child elements
</LaunchApplicationOnDeviceConnect>
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
<td><p><a href="autoplayhandler.md" data-raw-source="[AutoplayHandler](autoplayhandler.md)">AutoplayHandler</a></p></td>
<td><p>ユーザーがデバイスに接続するときに推奨される自動再生操作として表示する UWP デバイスアプリを指定します。</p></td>
</tr>
<tr class="even">
<td><p><a href="desktopautoplayhandler.md" data-raw-source="[DesktopAutoplayHandler](desktopautoplayhandler.md)">DesktopAutoplayHandler</a></p></td>
<td><p>ユーザーがデバイスに接続したときに推奨される自動再生操作として表示するデスクトップアプリを指定します。</p></td>
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
<td><p><a href="windowsinfo.md" data-raw-source="[WindowsInfo](windowsinfo.md)">WindowsInfo</a></p></td>
<td><p><a href="windowsinfo-xml-schema.md" data-raw-source="[WindowsInfo XML schema](windowsinfo-xml-schema.md)">Windowsinfo XML スキーマ</a>の親要素。</p></td>
</tr>
</tbody>
</table>

 

## <a name="span-idxsdspanspan-idxsdspanxsd"></a><span id="XSD"></span><span id="xsd"></span>XSD.EXE


``` syntax
<xs:element name="LaunchApplicationOnDeviceConnect" type ="tns:LaunchApplicationOnDeviceConnectType" />

<xs:complexType name="LaunchApplicationOnDeviceConnectType">
    <xs:choice>
      <xs:element name="AutoplayHandler" type="tns:AutoplayHandlerType" />
      <xs:element name="DesktopAutoplayHandler" type="xs:string" />
      <xs:any namespace="##other" processContents="lax" />
    </xs:choice>
  </xs:complexType>
```

## <a name="span-idremarksspanspan-idremarksspanspan-idremarksspanremarks"></a><span id="Remarks"></span><span id="remarks"></span><span id="REMARKS"></span>注釈


UWP デバイスアプリまたはデスクトップアプリのいずれかを指定する必要があります。 UWP デバイスアプリを指定する場合は[Autoplayhandler](autoplayhandler.md)を使用し、デスクトップアプリケーションを指定する場合は[Desktopautoplayhandler](desktopautoplayhandler.md)を使用します。

LaunchApplicationOnDeviceConnect 要素は省略可能です。

 

 






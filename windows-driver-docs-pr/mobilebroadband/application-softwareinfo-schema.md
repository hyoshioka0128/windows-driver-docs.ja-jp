---
title: アプリケーション (ソフトウェア情報)
description: アプリケーション (ソフトウェア情報)
ms.assetid: 1f16a690-4453-4563-a4b1-44bbd5d02f47
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a95bae273f1e80f50d9b235a5aecf5282fced669
ms.sourcegitcommit: f017184b00f59b088df87a5bd85fec51b7aed8b2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/15/2019
ms.locfileid: "72323642"
---
# <a name="application-softwareinfo"></a>アプリケーション (ソフトウェア情報)

[!include[MBAE deprecation warning](mbae-deprecation-warning.md)]

Application 要素は、関連付けられているデバイス通知ハンドラーを指定します。

## <a name="span-idusagespanspan-idusagespanspan-idusagespanusage"></a><span id="Usage"></span><span id="usage"></span><span id="USAGE"></span>ユーセジリンク


``` syntax
<Application Id=”tns:ApplicationIdType”>
  Child element
</Application>
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
<th>備わっている</th>
<th>タスクバーの検索ボックスに</th>
<th>必須かどうか</th>
<th>説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Id</p></td>
<td><p>tns: ApplicationIdType</p></td>
<td><p>[はい]</p></td>
<td><p>アプリケーションの ID。</p></td>
</tr>
</tbody>
</table>

 

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
<td><p><a href="devicenotificationhandlers.md" data-raw-source="[DeviceNotificationHandlers](devicenotificationhandlers.md)">DeviceNotificationHandlers</a></p></td>
<td><p>デバイス通知ハンドラーのリストを指定します。</p></td>
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
<td><p><a href="applications.md" data-raw-source="[Applications](applications.md)">プログラム</a></p></td>
<td><p>PC でオペレーターのモバイルブロードバンドハードウェアが検出されたときにダウンロードされるアプリを指定します。</p></td>
</tr>
</tbody>
</table>

 

## <a name="span-idxsdspanspan-idxsdspanxsd"></a><span id="XSD"></span><span id="xsd"></span>XSD.EXE


``` syntax
<xs:element name="Application" type="tns:ApplicationType"/>

<xs:complexType name="ApplicationType">
  <xs:sequence>
    <xs:element name="DeviceNotificationHandlers" type="tns:DeviceNotificationHandlersType" minOccurs="0" />
    <xs:any namespace="##other" processContents="lax" minOccurs="0" maxOccurs="unbounded" />
  </xs:sequence>
  <xs:attribute name="Id" type="tns:ApplicationIdType" use="required"/>
</xs:complexType>
```

## <a name="span-idremarksspanspan-idremarksspanspan-idremarksspanremarks"></a><span id="Remarks"></span><span id="remarks"></span><span id="REMARKS"></span>注釈


Application 要素は省略可能です。

 

 






---
title: ConnectionInfo
description: ConnectionInfo
ms.assetid: bbdba286-4d28-46b6-bafa-83cbddd883ae
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 464350735044c190486fe9b18d9b944d59fb957d
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56573549"
---
# <a name="connectioninfo"></a>ConnectionInfo


ConnectionInfo 要素には、指定したオペレーターの接続の一覧を指定します。

## <a name="span-idusagespanspan-idusagespanspan-idusagespanusage"></a><span id="Usage"></span><span id="usage"></span><span id="USAGE"></span>使用状況


``` syntax
<ConnectionInfoList AccessString=”xs:string” Username=”xs:string” Password=”xs:string” FriendlyName=”xs:string” Purchase=”xs:Boolean” Internet=”xs:Boolean” AutoConnectOrder=”xs:positiveinteger” Compression=”xs:token” AutoProtocol=”xs:token”>
</ConnectionInfoList>
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
<th>型</th>
<th>必須</th>
<th>説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>AccessString</p></td>
<td><p>xs:string</p></td>
<td><p>いいえ</p></td>
<td><p>名前と演算子の国/地域。</p>
<p>例:Contoso (アルゼンチン)</p></td>
</tr>
<tr class="even">
<td><p>Username</p></td>
<td><p>xs:string</p></td>
<td><p>いいえ</p></td>
<td><p>ユーザー名は、インターネットへの接続に使用されます。</p></td>
</tr>
<tr class="odd">
<td><p>パスワード</p></td>
<td><p>xs:string</p></td>
<td><p>いいえ</p></td>
<td><p>インターネットに接続するために使用するパスワード。</p></td>
</tr>
<tr class="even">
<td><p>FriendlyName</p></td>
<td><p>xs:string</p></td>
<td><p>いいえ</p></td>
<td><p>接続マネージャーで Windows APN のドロップダウン ボックスで表示される値。</p></td>
</tr>
<tr class="odd">
<td><p>購入</p></td>
<td><p>xs:boolean</p></td>
<td><p>はい</p></td>
<td><p>購入またはインターネット アクセス文字列を使用するかどうかを示します。</p></td>
</tr>
<tr class="even">
<td><p>Test1</p></td>
<td><p>xs:boolean</p></td>
<td><p>はい</p></td>
<td><p>購入またはインターネット アクセス文字列を使用するかどうかを示します。</p></td>
</tr>
<tr class="odd">
<td><p>AutoConnectOrder</p></td>
<td><p>xs:positiveinteger</p></td>
<td><p>いいえ</p></td>
<td><p>APNs のそれぞれへの接続に Windows がしようとする順序を指定します、 <a href="connectioninfolist.md" data-raw-source="[ConnectionInfoList](connectioninfolist.md)">ConnectionInfoList</a>要素。</p></td>
</tr>
<tr class="even">
<td><p>圧縮</p></td>
<td><p>xs:token</p></td>
<td><p>いいえ</p></td>
<td><p>ヘッダーとデータ転送の圧縮を使用データ リンクではかどうかを指定します。</p>
<p>値:有効または無効にします。</p></td>
</tr>
<tr class="odd">
<td><p>AuthProtocol</p></td>
<td><p>xs:token</p></td>
<td><p>いいえ</p></td>
<td><p>PDP コンテキストをアクティブ化するために使用される認証プロトコルを指定します。</p>
<p>値:NONE、PAP、CHAP、または MsCHAPv2</p></td>
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
<td><p><a href="connectioninfolist.md" data-raw-source="[ConnectionInfoList](connectioninfolist.md)">ConnectionInfoList</a></p></td>
<td><p>APN データベース内の演算子の詳細を指定します。</p></td>
</tr>
</tbody>
</table>

 

## <a name="span-idxsdspanspan-idxsdspanxsd"></a><span id="XSD"></span><span id="xsd"></span>XSD


``` syntax
<xs:element ref="ConnectionInfo" maxOccurs="unbounded"/>

<xs:element name="ConnectionInfo">
  <xs:complexType>
    <xs:attribute name="AccessString" use="optional">
      <!--The AccessString element identifies the APN or dial string to be used to establish a data connection -->
      <xs:simpleType>
        <xs:restriction base="xs:string">
          <xs:minLength value="0"/>
          <xs:maxLength value="100"/>
        </xs:restriction>
      </xs:simpleType>
    </xs:attribute>
    <xs:attribute name="Username" use="optional">
      <!--The UserName element specifies the user name for logon -->
      <xs:simpleType>
        <xs:restriction base="xs:string">
          <xs:minLength value="0"/>
          <xs:maxLength value="255"/>
          <xs:whiteSpace value="collapse"/>
        </xs:restriction>
      </xs:simpleType>
    </xs:attribute>
    <xs:attribute name="Password" use="optional">
      <xs:simpleType>
        <xs:restriction base="xs:string">
          <xs:minLength value="0"/>
          <xs:maxLength value="255"/>
          <xs:whiteSpace value="collapse"/>
        </xs:restriction>
      </xs:simpleType>
    </xs:attribute>
    <xs:attribute name="FriendlyName" use="optional">
      <xs:simpleType>
        <xs:restriction base="xs:string">
          <xs:minLength value="0"/>
          <xs:maxLength value="255"/>
          <xs:whiteSpace value="collapse"/>
        </xs:restriction>
      </xs:simpleType>
    </xs:attribute>
    <xs:attribute name="Purchase" type="xs:boolean" use="required"/>
    <xs:attribute name="Internet" type="xs:boolean" use="required"/>
    <xs:attribute name="AutoConnectOrder" type="xs:positiveInteger" use="optional"/>
    <xs:attribute name="Compression" use="optional">
      <xs:simpleType>
        <xs:restriction base="xs:token">
          <xs:enumeration value="DISABLE"/>
          <xs:enumeration value="ENABLE"/>
        </xs:restriction>
      </xs:simpleType>
    </xs:attribute>
    <xs:attribute name="AuthProtocol" use="optional">
      <xs:simpleType>
        <xs:restriction base="xs:token">
          <xs:enumeration value="NONE"/>
          <xs:enumeration value="PAP"/>
          <xs:enumeration value="CHAP"/>
          <xs:enumeration value="MsCHAPv2"/>
        </xs:restriction>
      </xs:simpleType>
    </xs:attribute>
  </xs:complexType>
</xs:element>
```

## <a name="span-idremarksspanspan-idremarksspanspan-idremarksspanremarks"></a><span id="Remarks"></span><span id="remarks"></span><span id="REMARKS"></span>注釈


ConnectionInfo 要素が必要です。

 

 






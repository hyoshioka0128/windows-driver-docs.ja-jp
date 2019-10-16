---
title: HardwareId (PackageInfo)
description: HardwareId (PackageInfo)
ms.assetid: edd05106-1bbc-45da-80cc-792d7fcce192
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: fb456db9e7a36c8aa891a3532d42588e2bc1b461
ms.sourcegitcommit: f017184b00f59b088df87a5bd85fec51b7aed8b2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/15/2019
ms.locfileid: "72323699"
---
# <a name="hardwareid-packageinfo"></a>HardwareId (PackageInfo)

[!include[MBAE deprecation warning](mbae-deprecation-warning.md)]

サービスメタデータパッケージの場合、HardwareID 値は、次の形式でモバイルネットワークオペレーターを表します。

-   GSM ネットワーク: IMSI 値

-   GSM ネットワーク: ICCID 値

-   CDMA ネットワーク: プロバイダー名の値

-   CDMA ネットワーク: プロバイダー ID 値 (SID とも呼ばれます)

## <a name="span-idusagespanspan-idusagespanspan-idusagespanusage"></a><span id="Usage"></span><span id="usage"></span><span id="USAGE"></span>ユーセジリンク


``` syntax
<HardwareID>
  text
</HardwareID>
```

## <a name="span-idattributesspanspan-idattributesspanspan-idattributesspanattributes"></a><span id="Attributes"></span><span id="attributes"></span><span id="ATTRIBUTES"></span>アトリビュート


属性はありません。

## <a name="span-idtext_valuespanspan-idtext_valuespanspan-idtext_valuespantext-value"></a><span id="Text_value"></span><span id="text_value"></span><span id="TEXT_VALUE"></span>テキスト値


メタデータの作成の一環として適切なハードウェア ID 値を生成するには、複雑なアルゴリズムが必要です。 Windows Driver Kit (WDK) に含まれている MBIDGenerator を使用して、ハードウェア ID 値を生成する必要があります。

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
<td><p><a href="hardwareidlist.md" data-raw-source="[HardwareIDList](hardwareidlist.md)">ハードウェア Id リスト</a></p></td>
<td><p>Hardware <a href="hardwareidlist.md" data-raw-source="[HardwareIDList](hardwareidlist.md)">Idlist</a>要素は、サービスメタデータパッケージの1つ以上のハードウェア id 文字列を指定します。</p></td>
</tr>
</tbody>
</table>

 

## <a name="span-idxsdspanspan-idxsdspanxsd"></a><span id="XSD"></span><span id="xsd"></span>XSD.EXE


``` syntax
<xs:element name="HardwareID" type="tns:HardwareIDType" maxOccurs="unbounded" />

<xs:simpleType name="HardwareIDType">
  <xs:restriction base="xs:string">
    <xs:minLength value="1" />
    <xs:maxLength value="207" />
    <xs:pattern value="^([a-zA-Z0-9!#$%&()*+\-./:;&lt;=&gt;?@[\\\]^_`{|}~])*$" /> 
  </xs:restriction>
</xs:simpleType>
```

## <a name="span-idremarksspanspan-idremarksspanspan-idremarksspanremarks"></a><span id="Remarks"></span><span id="remarks"></span><span id="REMARKS"></span>注釈


-   PackageInfo .xml に含まれるハードウェア Id には、"DOID:" プレフィックスが追加されている必要があります。 例: DOID: MBAE: 0:*hashednumber1*

-   サービスを指定するために、複数の HardwareID 要素を使用できます。

-   GSM IMSI または ICCID 範囲の場合、開始範囲の値は00で終わり、終了範囲の値は99で終わる必要があります。 プライバシー上の理由から、IMSI と ICCID の値については、100のブロックで照合が行われます。

HardwareID 要素が必要です。

 

 






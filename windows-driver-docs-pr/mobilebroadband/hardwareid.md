---
title: HardwareId (PackageInfo)
description: HardwareId (PackageInfo)
ms.assetid: edd05106-1bbc-45da-80cc-792d7fcce192
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: fb456db9e7a36c8aa891a3532d42588e2bc1b461
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56580604"
---
# <a name="hardwareid-packageinfo"></a>HardwareId (PackageInfo)

[!include[MBAE deprecation warning](mbae-deprecation-warning.md)]

サービス メタデータ パッケージの場合は、HardwareID の値は、次の形式でのモバイル ネットワーク オペレーターを表します。

-   GSM ネットワーク:IMSI 値

-   GSM ネットワーク:ICCID 値

-   CDMA ネットワーク:プロバイダー名の値

-   CDMA ネットワーク:プロバイダー ID の値 (SID とも呼ばれます)

## <a name="span-idusagespanspan-idusagespanspan-idusagespanusage"></a><span id="Usage"></span><span id="usage"></span><span id="USAGE"></span>使用状況


``` syntax
<HardwareID>
  text
</HardwareID>
```

## <a name="span-idattributesspanspan-idattributesspanspan-idattributesspanattributes"></a><span id="Attributes"></span><span id="attributes"></span><span id="ATTRIBUTES"></span>属性


属性はありません。

## <a name="span-idtextvaluespanspan-idtextvaluespanspan-idtextvaluespantext-value"></a><span id="Text_value"></span><span id="text_value"></span><span id="TEXT_VALUE"></span>テキスト値


メタデータ作成の一環として、適切なハードウェアの ID 値を生成するには、複雑なアルゴリズムが含まれます。 Windows Driver Kit (WDK) で含まれている MBIDGenerator.exe を使用して、ハードウェア ID の値を生成する必要があります。

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
<td><p><a href="hardwareidlist.md" data-raw-source="[HardwareIDList](hardwareidlist.md)">HardwareIDList</a></p></td>
<td><p><a href="hardwareidlist.md" data-raw-source="[HardwareIDList](hardwareidlist.md)">HardwareIDList</a>要素は、サービス メタデータ パッケージの 1 つまたは複数のハードウェアの識別文字列を指定します。</p></td>
</tr>
</tbody>
</table>

 

## <a name="span-idxsdspanspan-idxsdspanxsd"></a><span id="XSD"></span><span id="xsd"></span>XSD


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


-   ハードウェア Id PackageInfo.xml に含まれている必要がありますが、"DOID:"プレフィックスを追加することです。 以下に例を示します。DOID:MBAE:0:*hashednumber1*

-   HardwareID の 1 つ以上の要素は、サービスを指定して使用できます。

-   GSM IMSI または ICCID の範囲の開始範囲の値が 00 で終わる必要があり、終了範囲の値は 99 で終了する必要があります。 プライバシー上の理由から、一致する IMSI と ICCID 値 100 ブロック単位で行われます。

HardwareID 要素が必要です。

 

 






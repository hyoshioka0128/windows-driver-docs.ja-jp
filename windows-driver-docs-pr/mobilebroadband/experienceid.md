---
title: ExperienceID
description: ExperienceID
ms.assetid: 550527ae-fef9-46c6-816b-d842fe472b68
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3effd9c4f887a7e8c44d8488d49ffdcf7097eb92
ms.sourcegitcommit: f017184b00f59b088df87a5bd85fec51b7aed8b2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/15/2019
ms.locfileid: "72323613"
---
# <a name="experienceid"></a>ExperienceID

[!include[MBAE deprecation warning](mbae-deprecation-warning.md)]

ExperienceID 要素は、デバイスエクスペリエンスを表す GUID を指定します。 この GUID は、パッケージのロケールに関係なく、同じデバイス識別子に対して1つ以上のメタデータパッケージをグループ化するために使用されます。

Windows 8、Windows 8.1、および Windows 10 では、デバイスが最初に接続されたときに自動的に取得できるデバイスアプリにデバイスのメタデータをリンクするためにも使用されます。 デバイスアプリは、アプリ送信パッケージの StoreManifest ファイル内の1つ以上の ExperienceID 要素を指定します。 これらの各 ExperienceID Guid は、デバイスメタデータパッケージの ExperienceID 要素に対応しています。 StoreManifest ファイルが送信された後、デバイスのメタデータの ExperienceID がデバイスアプリの StoreManifest ファイルでも指定されている場合、デバイスアプリを1つ以上のデバイスモデルに配布できます。

## <a name="span-idusagespanspan-idusagespanspan-idusagespanusage"></a><span id="Usage"></span><span id="usage"></span><span id="USAGE"></span>ユーセジリンク


``` syntax
<ExperienceID>
  text
</ExperienceID>
```

## <a name="span-idattributesspanspan-idattributesspanspan-idattributesspanattributes"></a><span id="Attributes"></span><span id="attributes"></span><span id="ATTRIBUTES"></span>アトリビュート


属性はありません。

## <a name="span-idtext_valuespanspan-idtext_valuespanspan-idtext_valuespantext-value"></a><span id="Text_value"></span><span id="text_value"></span><span id="TEXT_VALUE"></span>テキスト値


[Guidtype](guidtype-packageinfo.md) XML 単純型として書式設定された値。

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
<td><p><a href="relationships.md" data-raw-source="[Relationships](relationships.md)">リレーションシップ</a></p></td>
<td><p><a href="relationships.md" data-raw-source="[Relationships](relationships.md)">リレーションシップ</a>要素は、デバイスメタデータキャッシュ内のデバイスメタデータパッケージを追跡するために使用されるデータを指定します。</p></td>
</tr>
</tbody>
</table>

 

## <a name="span-idxsdspanspan-idxsdspanxsd"></a><span id="XSD"></span><span id="xsd"></span>XSD.EXE


``` syntax
<xs:element name="ExperienceID" type="tns:GUIDType" minOccurs="0" />
```

## <a name="span-idremarksspanspan-idremarksspanspan-idremarksspanremarks"></a><span id="Remarks"></span><span id="remarks"></span><span id="REMARKS"></span>注釈


Windows 8.1 と Windows 10 では、ExperienceID は Windows デベロッパーセンターダッシュボードのサービスメタデータウィザードによって作成されます。

Windows 8 では、サービスメタデータ開発者が ExperienceID を指定するか、[デバイスメタデータ作成ウィザード](https://go.microsoft.com/fwlink/?linkid=620032)を使用して自動的に生成し、サービスメタデータに追加することができます。 サービスメタデータパッケージで ExperienceID が指定されていない場合、Windows デベロッパーセンターダッシュボードは GUID を作成し、モバイルネットワークオペレーターまたはモバイル仮想ネットワークオペレーターがサービスメタデータパッケージ。

 

 






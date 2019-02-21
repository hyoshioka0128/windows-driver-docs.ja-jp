---
title: ExperienceID
description: ExperienceID
ms.assetid: 550527ae-fef9-46c6-816b-d842fe472b68
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3effd9c4f887a7e8c44d8488d49ffdcf7097eb92
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56532496"
---
# <a name="experienceid"></a>ExperienceID

[!include[MBAE deprecation warning](mbae-deprecation-warning.md)]

ExperienceID 要素には、デバイス エクスペリエンスを表す GUID を指定します。 この GUID は、パッケージのロケールに依存しない同じデバイス識別子の 1 つまたは複数のメタデータ パッケージをグループ化に使用されます。

Windows 8、Windows 8.1、および Windows 10 デバイスのメタデータをデバイスが最初に接続されているときに自動的に取得できるデバイスのアプリにリンクすることも使用されます。 デバイス アプリでは、アプリの提出パッケージで StoreManifest.XML ファイルで 1 つまたは複数の ExperienceID 要素を指定します。 これらの ExperienceID Guid は、デバイス メタデータ パッケージの ExperienceID 要素に対応します。 StoreManifest.xml ファイルが送信された後、デバイス アプリしに配布できる 1 つまたは複数のデバイス モデルでは、デバイスのメタデータで ExperienceID も、デバイス アプリ StoreManifest ファイルで指定した場合。

## <a name="span-idusagespanspan-idusagespanspan-idusagespanusage"></a><span id="Usage"></span><span id="usage"></span><span id="USAGE"></span>使用状況


``` syntax
<ExperienceID>
  text
</ExperienceID>
```

## <a name="span-idattributesspanspan-idattributesspanspan-idattributesspanattributes"></a><span id="Attributes"></span><span id="attributes"></span><span id="ATTRIBUTES"></span>属性


属性はありません。

## <a name="span-idtextvaluespanspan-idtextvaluespanspan-idtextvaluespantext-value"></a><span id="Text_value"></span><span id="text_value"></span><span id="TEXT_VALUE"></span>テキスト値


値として書式設定、 [GUIDType](guidtype-packageinfo.md) XML 単純型。

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
<td><p><a href="relationships.md" data-raw-source="[Relationships](relationships.md)">リレーションシップ</a></p></td>
<td><p><a href="relationships.md" data-raw-source="[Relationships](relationships.md)">リレーションシップ</a>要素は、デバイスのメタデータ キャッシュ内のデバイス メタデータ パッケージを追跡するために使用されるデータを指定します。</p></td>
</tr>
</tbody>
</table>

 

## <a name="span-idxsdspanspan-idxsdspanxsd"></a><span id="XSD"></span><span id="xsd"></span>XSD


``` syntax
<xs:element name="ExperienceID" type="tns:GUIDType" minOccurs="0" />
```

## <a name="span-idremarksspanspan-idremarksspanspan-idremarksspanremarks"></a><span id="Remarks"></span><span id="remarks"></span><span id="REMARKS"></span>「解説」


Windows 8.1 および Windows 10、Windows デベロッパー センター ダッシュ ボードで、サービス メタデータのウィザードによって、ExperienceID が作成されます。

Windows 8 では、ExperienceID メタデータ、サービス開発者によって指定されたまたは自動的に生成された追加できサービスのメタデータを使用する、[デバイス メタデータの作成ウィザード](https://go.microsoft.com/fwlink/?linkid=620032)します。 Windows デベロッパー センター ダッシュ ボードが GUID を作成し、モバイル ネットワーク オペレーターまたはモバイルの仮想ネットワーク オペレーターに送信するときに、メタデータ パッケージ内で ExperienceID 要素を更新、ExperienceID がサービス メタデータ パッケージに指定されていない場合、サービス メタデータ パッケージ。

 

 






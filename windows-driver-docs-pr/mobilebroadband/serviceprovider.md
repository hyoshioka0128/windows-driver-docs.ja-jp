---
title: サービス プロバイダー
description: サービス プロバイダー
ms.assetid: 6fa22f4d-9be9-4d02-b610-e20bed4958e9
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d170aa38f54eaf91340aa8d9c02ffc6765eae6b4
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56528156"
---
# <a name="serviceprovider"></a>サービス プロバイダー

[!include[MBAE deprecation warning](mbae-deprecation-warning.md)]

> [!IMPORTANT]
> Windows 10 バージョン 1709 以降では、このフィールドは COSA を通じてブランドで置き換えられました。 ブランド化の COSA 内のフィールドが説明されている[計画デスクトップ COSA/APN データベース提出](planning-your-desktop-cosa-apn-database-submission.md)します。 Windows 10 バージョン 1709 では、前に Windows のバージョンを対象としている場合、このセクションで説明したようにメタデータ パッケージを作成も。 COSA の詳細については、[COSA 概要](cosa-overview.md)を参照してください。 

ServiceProvider 要素には、サービス プロバイダーの名前を指定します。 ホーム プロバイダー ネットワークの名前を表示する Windows 接続マネージャー で表示されます。 ユーザーがローミング ネットワーク上にある場合は、ローミングのネットワーク名が表示されます。

## <a name="span-idusagespanspan-idusagespanspan-idusagespanusage"></a><span id="Usage"></span><span id="usage"></span><span id="USAGE"></span>使用状況


``` syntax
<ServiceProvider>
  text
</ServiceProvider>
```

## <a name="span-idattributesspanspan-idattributesspanspan-idattributesspanattributes"></a><span id="Attributes"></span><span id="attributes"></span><span id="ATTRIBUTES"></span>属性


属性はありません。

## <a name="span-idtextvaluespanspan-idtextvaluespanspan-idtextvaluespantext-value"></a><span id="Text_value"></span><span id="text_value"></span><span id="TEXT_VALUE"></span>テキスト値


印刷可能な最大 20 個の文字の文字列。

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
<td><p><a href="serviceinfo.md" data-raw-source="[ServiceInfo](serviceinfo.md)">ServiceInfo</a></p></td>
<td><p><a href="serviceinfo.md" data-raw-source="[ServiceInfo](serviceinfo.md)">ServiceInfo</a>要素は、親要素の<a href="serviceinfo-xml-schema.md" data-raw-source="[ServiceInfo XML schema](serviceinfo-xml-schema.md)">ServiceInfo XML スキーマ</a>します。</p></td>
</tr>
</tbody>
</table>

 

## <a name="span-idxsdspanspan-idxsdspanxsd"></a><span id="XSD"></span><span id="xsd"></span>XSD


``` syntax
<xs:element name="ServiceProvider" type="tns:ProviderNameType"/>

<xs:simpleType name="ProviderNameType">
  <xs:restriction base="xs:string">
    <xs:minLength value="1" />
    <xs:maxLength value="20" />
  </xs:restriction>
</xs:simpleType>
```

## <a name="span-idremarksspanspan-idremarksspanspan-idremarksspanremarks"></a><span id="Remarks"></span><span id="remarks"></span><span id="REMARKS"></span>「解説」


ServiceProvider 要素では、ユーザーがローミング時に Windows 接続マネージャーでは表示されません。

ServiceProvider 要素が必要です。

 

 






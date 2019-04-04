---
title: ServiceIconFile
description: ServiceIconFile
ms.assetid: a35a121d-66a8-485e-ac12-adc653db3572
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 891e257bdac542c3eeee5bcbd6ee7d567db13db8
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56535890"
---
# <a name="serviceiconfile"></a>ServiceIconFile

[!include[MBAE deprecation warning](mbae-deprecation-warning.md)]

> [!IMPORTANT]
> Windows 10 バージョン 1709 以降では、このフィールドは COSA を通じてブランドで置き換えられました。 ブランド化の COSA 内のフィールドが説明されている[計画デスクトップ COSA/APN データベース提出](planning-your-desktop-cosa-apn-database-submission.md)します。 Windows 10、バージョン 1709 より前に、の Windows のバージョンを対象としている場合でも、このセクションで説明したメタデータ パッケージを作成します。 COSA の詳細については、[COSA 概要](cosa-overview.md)を参照してください。 

ServiceIconFile 要素は、サービス メタデータ パッケージで、サービスのアイコン ファイルの名前を指定します。 Windows 接続マネージャーで、モバイル ネットワーク オペレーター (MNO) またはモバイルの仮想ネットワーク オペレーター (MVNO) のロゴを表示するサービスのアイコン ファイルが使用されます。

## <a name="span-idusagespanspan-idusagespanspan-idusagespanusage"></a><span id="Usage"></span><span id="usage"></span><span id="USAGE"></span>使用状況


``` syntax
<ServiceProvider>
  text
</ServiceProvider>
```

## <a name="span-idattributesspanspan-idattributesspanspan-idattributesspanattributes"></a><span id="Attributes"></span><span id="attributes"></span><span id="ATTRIBUTES"></span>属性


属性はありません。

## <a name="span-idtextvaluespanspan-idtextvaluespanspan-idtextvaluespantext-value"></a><span id="Text_value"></span><span id="text_value"></span><span id="TEXT_VALUE"></span>テキスト値


アイコン ファイルの名前をします。ICO 拡張機能。

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
<xs:element name="ServiceIconFile" type="tns:ServiceIconFileType" minOccurs="0"/>

<xs:simpleType name="ServiceIconFileType">
  <xs:restriction base="xs:string">
    <xs:pattern value=".+\.ico"/>
  </xs:restriction>
</xs:simpleType>
```

## <a name="span-idremarksspanspan-idremarksspanspan-idremarksspanremarks"></a><span id="Remarks"></span><span id="remarks"></span><span id="REMARKS"></span>「解説」


必要なアイコン ファイルのサイズは次のとおりです。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>256x256: 32 ビット + アルファ (圧縮)</p></td>
<td><p>24x24: 32 ビット + アルファ</p></td>
</tr>
<tr class="even">
<td><p>48 ｘ 48: 32 ビット + アルファ</p></td>
<td><p>24 ｘ 24: 8 ビット 256 色</p></td>
</tr>
<tr class="odd">
<td><p>48 ｘ 48: 8 ビット 256 色</p></td>
<td><p>24 ｘ 24: 4 ビット 16 色</p></td>
</tr>
<tr class="even">
<td><p>48 ｘ 48: 4 ビット 16 色</p></td>
<td><p>16 ｘ 16: 32 ビット + アルファ</p></td>
</tr>
<tr class="odd">
<td><p>32 ｘ 32: 32 ビット + アルファ</p></td>
<td><p>16x16: 8 ビット 256 色</p></td>
</tr>
<tr class="even">
<td><p>32x32: 8 ビット 256 色</p></td>
<td><p>16x16: 4 ビット 16 色</p></td>
</tr>
<tr class="odd">
<td><p>32x32: 4 ビット 16 色</p></td>
<td><p></p></td>
</tr>
</tbody>
</table>

 

ServiceIconFile 要素は、スキーマでは省略可能としてマークされます。 ただし、ServiceIconFile 要素を持たない Windows デベロッパー センター ダッシュ ボードに送信されるサービス メタデータ パッケージは拒否されます。

 

 






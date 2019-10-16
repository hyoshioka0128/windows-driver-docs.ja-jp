---
title: ServiceIconFile
description: ServiceIconFile
ms.assetid: a35a121d-66a8-485e-ac12-adc653db3572
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 891e257bdac542c3eeee5bcbd6ee7d567db13db8
ms.sourcegitcommit: f017184b00f59b088df87a5bd85fec51b7aed8b2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/15/2019
ms.locfileid: "72323727"
---
# <a name="serviceiconfile"></a>ServiceIconFile

[!include[MBAE deprecation warning](mbae-deprecation-warning.md)]

> [!IMPORTANT]
> Windows 10 バージョン1709以降では、このフィールドは COSA によってブランド化されています。 ブランド化のための COSA のフィールドについては[、「デスクトップ cosa/APN データベースの送信を計画](planning-your-desktop-cosa-apn-database-submission.md)する」を参照してください。 Windows 10 バージョン1709よりも前のバージョンの Windows を対象としている場合は、このセクションで説明するようにメタデータパッケージを作成します。 COSA の詳細については、 [Cosa の概要](cosa-overview.md)に関するトピックを参照してください。 

ServiceIconFile 要素は、サービスメタデータパッケージ内のサービスアイコンファイルの名前を指定します。 サービスアイコンファイルは、Windows 接続マネージャーでモバイルネットワークオペレーター (MNO) またはモバイル仮想ネットワークオペレーター (MVNO) のロゴを表示するために使用されます。

## <a name="span-idusagespanspan-idusagespanspan-idusagespanusage"></a><span id="Usage"></span><span id="usage"></span><span id="USAGE"></span>ユーセジリンク


``` syntax
<ServiceProvider>
  text
</ServiceProvider>
```

## <a name="span-idattributesspanspan-idattributesspanspan-idattributesspanattributes"></a><span id="Attributes"></span><span id="attributes"></span><span id="ATTRIBUTES"></span>アトリビュート


属性はありません。

## <a name="span-idtext_valuespanspan-idtext_valuespanspan-idtext_valuespantext-value"></a><span id="Text_value"></span><span id="text_value"></span><span id="TEXT_VALUE"></span>テキスト値


を持つアイコンファイルの名前.ICO 拡張機能。

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
<td><p><a href="serviceinfo.md" data-raw-source="[ServiceInfo](serviceinfo.md)">ServiceInfo</a></p></td>
<td><p><a href="serviceinfo.md" data-raw-source="[ServiceInfo](serviceinfo.md)">Serviceinfo</a>要素は、 <a href="serviceinfo-xml-schema.md" data-raw-source="[ServiceInfo XML schema](serviceinfo-xml-schema.md)">serviceinfo XML スキーマ</a>の親要素です。</p></td>
</tr>
</tbody>
</table>

 

## <a name="span-idxsdspanspan-idxsdspanxsd"></a><span id="XSD"></span><span id="xsd"></span>XSD.EXE


``` syntax
<xs:element name="ServiceIconFile" type="tns:ServiceIconFileType" minOccurs="0"/>

<xs:simpleType name="ServiceIconFileType">
  <xs:restriction base="xs:string">
    <xs:pattern value=".+\.ico"/>
  </xs:restriction>
</xs:simpleType>
```

## <a name="span-idremarksspanspan-idremarksspanspan-idremarksspanremarks"></a><span id="Remarks"></span><span id="remarks"></span><span id="REMARKS"></span>注釈


必要なアイコンファイルのサイズは次のとおりです。

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

 

ServiceIconFile 要素は、スキーマでオプションとしてマークされています。 ただし、ServiceIconFile 要素を指定せずに Windows デベロッパーセンターダッシュボードに送信されるサービスメタデータパッケージは拒否されます。

 

 






---
title: Format 要素
description: 省略可能な形式の要素では、スキャナーでサポートされている 1 つのファイル形式と圧縮の種類を示します。
ms.assetid: aa15607b-780b-48cb-b63f-b16476f69f70
keywords:
- Format 要素イメージング デバイス
topic_type:
- apiref
api_name:
- wscn Format wscn Override "" wscn UsedDefault ""
api_type:
- Schema
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: c17cf3b9a3179d6509a1f6e7f54e5d14ce699e7f
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63362201"
---
# <a name="format-element"></a>Format 要素


省略可能な**形式**要素が 1 つのファイル形式と圧縮の種類が、スキャナーでサポートされていることを示します。

<a name="usage"></a>使用方法
-----

```xml
<wscn:Format wscn:Override="" wscn:UsedDefault=""
  
      Override
      = "xs:string"
  
      UsedDefault
      = "xs:string">
  text
</wscn:Format wscn:Override="" wscn:UsedDefault="">
```

<a name="attributes"></a>属性
----------

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
<th>種類</th>
<th>必須</th>
<th>説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>上書き</strong></p></td>
<td><p>xs:string</p></td>
<td><p>X</p></td>
<td><p></p>
<p>任意。 ブール値を 0 にする必要がある<strong>false</strong>、1、または<strong>true</strong>します。</p></td>
</tr>
<tr class="even">
<td><p><strong>UsedDefault</strong></p></td>
<td><p>xs:string</p></td>
<td><p>X</p></td>
<td><p></p>
<p>任意。 ブール値を 0 にする必要がある<strong>false</strong>、1、または<strong>true</strong>します。</p></td>
</tr>
</tbody>
</table>

<a name="text-value"></a>テキスト値
----------

必須。 次のいずれかの値です。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>用語</th>
<th>説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><span id="dib"></span><span id="DIB"></span>Dib</p></td>
<td><p>Windows デバイスに依存しないビットマップ。</p></td>
</tr>
<tr class="even">
<td><p><span id="exif"></span><span id="EXIF"></span>exif</p></td>
<td><p>Exchangeable Image ファイル形式のバージョン 2.x。</p></td>
</tr>
<tr class="odd">
<td><p><span id="jbig"></span><span id="JBIG"></span>jbig</p></td>
<td><p>ISO/IEC 11544:1993 Standard - コード化された形式の画像とオーディオの情報段階的な bi-level 画像圧縮します。</p></td>
</tr>
<tr class="even">
<td><p><span id="jfif"></span><span id="JFIF"></span>jfif</p></td>
<td><p>JPEG File Interchange Format 1.x.</p></td>
</tr>
<tr class="odd">
<td><p><span id="jpeg2k"></span><span id="JPEG2K"></span>jpeg2k</p></td>
<td><p>JPEG 2000 standard ベースのファイル形式と圧縮します。</p></td>
</tr>
<tr class="even">
<td><p><span id="pdf-a"></span><span id="PDF-A"></span>pdf、</p></td>
<td><p>PDF の形式 (標準が ISO/CD 19005-1) に基づいています。</p></td>
</tr>
<tr class="odd">
<td><p><span id="png"></span><span id="PNG"></span>png</p></td>
<td><p>ポータブル ネットワーク グラフィックス (PNG) 形式です。 この形式は PNG 圧縮の種類のみをサポートします。</p></td>
</tr>
<tr class="even">
<td><p><span id="tiff-single-uncompressed"></span><span id="TIFF-SINGLE-UNCOMPRESSED"></span>tiff 1 つ非圧縮</p></td>
<td><p>1 つページ TIFF ファイル圧縮の種類がありません。</p></td>
</tr>
<tr class="odd">
<td><p><span id="tiff-single-g4"></span><span id="TIFF-SINGLE-G4"></span>tiff の単一の g4</p></td>
<td><p>G4 圧縮の種類の 1 つのページ TIFF ファイル。</p></td>
</tr>
<tr class="even">
<td><p><span id="tiff-single-g3mh"></span><span id="TIFF-SINGLE-G3MH"></span>tiff の単一の g3mh</p></td>
<td><p>G3mh 圧縮の種類の 1 つのページ TIFF ファイル。</p></td>
</tr>
<tr class="odd">
<td><p><span id="tiff-single-jpeg-tn2"></span><span id="TIFF-SINGLE-JPEG-TN2"></span>tiff-single-jpeg-tn2</p></td>
<td><p>テクニカル ノート 2:」の説明に従って JPEG 圧縮の種類で単一ページの TIFF ファイル。</p></td>
</tr>
<tr class="even">
<td><p><span id="tiff-multi-uncompressed"></span><span id="TIFF-MULTI-UNCOMPRESSED"></span>tiff マルチ非圧縮</p></td>
<td><p>複数ページ TIFF ファイル圧縮の種類がありません。</p></td>
</tr>
<tr class="odd">
<td><p><span id="tiff-multi-g4"></span><span id="TIFF-MULTI-G4"></span>tiff マルチ第 4 世代</p></td>
<td><p>G4 圧縮の種類で複数ページの TIFF ファイル。</p></td>
</tr>
<tr class="even">
<td><p><span id="tiff-multi-g3mh"></span><span id="TIFF-MULTI-G3MH"></span>tiff-マルチ-g3mh</p></td>
<td><p>G3mh 圧縮の種類で複数ページの TIFF ファイル。</p></td>
</tr>
<tr class="odd">
<td><p><span id="tiff-multi-jpeg-tn2"></span><span id="TIFF-MULTI-JPEG-TN2"></span>tiff-multi-jpeg-tn2</p></td>
<td><p>テクニカル ノート 2:」の説明に従って JPEG 圧縮の種類で複数ページの TIFF ファイル。</p></td>
</tr>
<tr class="even">
<td><p><span id="xps"></span><span id="XPS"></span>xps</p></td>
<td><p>XML Paper Specification</p></td>
</tr>
<tr class="odd">
<td><p><span id="Any_vendor-defined_values"></span><span id="any_vendor-defined_values"></span><span id="ANY_VENDOR-DEFINED_VALUES"></span>任意のベンダー定義の値</p></td>
<td></td>
</tr>
</tbody>
</table>

 

## <a name="child-elements"></a>子要素


子要素はありません。

## <a name="parent-elements"></a>親要素


<table>
<colgroup>
<col width="100%" />
</colgroup>
<thead>
<tr class="header">
<th>要素</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><a href="documentfinalparameters.md" data-raw-source="[&lt;strong&gt;DocumentFinalParameters&lt;/strong&gt;](documentfinalparameters.md)"><strong>DocumentFinalParameters</strong></a></p></td>
</tr>
<tr class="even">
<td><p><a href="documentparameters.md" data-raw-source="[&lt;strong&gt;DocumentParameters&lt;/strong&gt;](documentparameters.md)"><strong>DocumentParameters</strong></a></p></td>
</tr>
</tbody>
</table>

<a name="remarks"></a>注釈
-------

場合、イメージ**形式**要素はサポートされませんし、スキャナーの要求を拒否し、返す必要があります、 **ClientErrorDocumentFormatNotSupported**エラー コード。

スキャナーを送信するときに、 **ClientErrorDocumentFormatNotSupported** WSD スキャナーのドライバーでは、形式を検索する次の順序で他のイメージ形式を選択してください、し、エラー コード、イメージ形式をサポートしないためですスキャナーをサポートしています。

1. PNG (W3C PNG) 形式を選択すると、スキャナーはサポートされている場合。

2. EXIF 形式を選択した場合は、スキャナーがサポートされているおよび RGB (24 bpp) または (8pp) のグレースケール カラー モードが一致します。

3. G4 シングル ページ TIFF (tiff 単一 g4) 形式を選択した場合は、スキャナーがサポートされている、カラー モードは白黒 (1bpp)。

4. スキャナーはサポートされている場合、圧縮されていない単一ページ TIFF (tiff-単一の非圧縮) 形式が選択されます。

Windows 7 以降、WIA は、スキャンの自動構成をサポートします。 DIB 形式でスキャンを自動構成を要求すると、スキャナー、DIB 形式をサポートしていない場合は、WSD スキャナー ドライバー アルゴリズムを使用して、同じ前の手順で示すように、スキャナーをサポートするイメージ形式を選択します。

**注**  色のモードは自動構成されるスキャン用に選択可能ではありません。

 

WSD スキャン サービスを指定できます、省略可能な**オーバーライド**と**UsedDefault**属性の場合にのみ、**形式**要素に含まれる、 **DocumentFinalParameters**階層。 詳細については**オーバーライド**と**UsedDefault**とその用途を参照してください[ **DocumentFinalParameters**](documentfinalparameters.md)します。

拡張し、この要素に使用できる値のサブセットを作成します。

WSD スキャン サービス JBIG ファイル形式 (ISO/IEC 11544:1993) サポートしていますが、これは現在サポートされていません JBIG2 (ISO/IEC 14492:2001)。

## <a name="see-also"></a>関連項目


[**DocumentFinalParameters**](documentfinalparameters.md)

[**DocumentParameters**](documentparameters.md)

[**FormatValue**](formatvalue.md)

 

 







---
title: FormatValue 要素
description: 必要な FormatValue 要素には、1 つのサポートされているファイル形式と圧縮の種類を指定します。
ms.assetid: 0331f44d-6343-45f7-85a7-303733f3ee75
keywords:
- FormatValue 要素イメージング デバイス
topic_type:
- apiref
api_name:
- wscn FormatValue
api_type:
- Schema
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2dec49892f928256ff19657741f17f16b6b2eb4e
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63353342"
---
# <a name="formatvalue-element"></a>FormatValue 要素


必要な**FormatValue**要素が 1 つのサポートされているファイル形式と圧縮の種類を指定します。

<a name="usage"></a>使用方法
-----

```xml
<wscn:FormatValue>
  text
</wscn:FormatValue>
```

<a name="attributes"></a>属性
----------

属性はありません。

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
<td><p><span id="dib_"></span><span id="DIB_"></span>Dib</p></td>
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
<td><p>テクニカル ノート 2:」の説明に従って jpeg 圧縮の種類で単一ページの TIFF ファイル。</p></td>
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
<td><p>テクニカル ノート 2:」の説明に従って jpeg 圧縮の種類で複数ページの TIFF ファイル。</p></td>
</tr>
<tr class="even">
<td><p><span id="xps"></span><span id="XPS"></span>xps</p></td>
<td><p>XML Paper Specification します。</p></td>
</tr>
<tr class="odd">
<td><p><span id="Any_vendor-defined_values."></span><span id="any_vendor-defined_values."></span><span id="ANY_VENDOR-DEFINED_VALUES."></span>ベンダ定義の値。</p></td>
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
<td><p><a href="formatssupported.md" data-raw-source="[&lt;strong&gt;FormatsSupported&lt;/strong&gt;](formatssupported.md)"><strong>FormatsSupported</strong></a></p></td>
</tr>
</tbody>
</table>

<a name="remarks"></a>注釈
-------

両方を拡張して一部この要素に使用できる値。

これは、WSD スキャン サービス JBIG ファイル形式 (ISO/IEC 11544:1993) サポートしていますが、*いない*JBIG2 を現在サポート (ISO/IEC 14492:2001)。

## <a name="see-also"></a>関連項目


[**FormatsSupported**](formatssupported.md)

 

 







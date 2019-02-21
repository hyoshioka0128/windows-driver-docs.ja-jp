---
title: ADFColor 要素
description: 必要な ADFColor 要素には、自動ドキュメント フィーダー (ADF) の前または後ろの側でサポートされる機能を処理する色の一覧が含まれています。
ms.assetid: b336c72e-9095-456e-8cb4-4018e72e29fa
keywords:
- ADFColor 要素イメージング デバイス
topic_type:
- apiref
api_name:
- wscn ADFColor
api_type:
- Schema
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: c583d30d4b3a84d2afeea16676dd26e32073da8a
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56549259"
---
# <a name="adfcolor-element"></a>ADFColor 要素


必要な**ADFColor**要素に自動ドキュメント フィーダー (ADF) の前または後ろの側でサポートされる機能を処理する色の一覧が含まれています。

<a name="usage"></a>使用方法
-----

```xml
<wscn:ADFColor>
  child elements
</wscn:ADFColor>
```

<a name="attributes"></a>属性
----------

属性はありません。

## <a name="child-elements"></a>子要素


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
<td><p><a href="colorentry.md" data-raw-source="[&lt;strong&gt;ColorEntry&lt;/strong&gt;](colorentry.md)"><strong>ColorEntry</strong></a></p></td>
</tr>
</tbody>
</table>

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
<td><p><a href="adfback.md" data-raw-source="[&lt;strong&gt;ADFBack&lt;/strong&gt;](adfback.md)"><strong>ADFBack</strong></a></p></td>
</tr>
<tr class="even">
<td><p><a href="adffront.md" data-raw-source="[&lt;strong&gt;ADFFront&lt;/strong&gt;](adffront.md)"><strong>ADFFront</strong></a></p></td>
</tr>
</tbody>
</table>

<a name="remarks"></a>注釈
-------

**ADFColor**要素には色の処理と取得、スキャナーの ADF をサポートする種類を決定するための情報が含まれています。 親要素がある場合[ **ADFFront**](adffront.md)、ADF の正面に指定された色の情報が適用されます親要素は、それ以外の場合、 [ **ADFBack**。](adfback.md)色の情報が、ADF の背面に適用されます。

各ピクセルの記述に必要な情報の量が特定の依存[ **ColorEntry** ](colorentry.md)キーワード。 白と黒のイメージでは、グレースケールおよびカラーの画像がはるかに多くの情報が必要ですが、1 つのビット/ピクセル (bpp) のみが必要です。 正確な情報量は、色空間とスキャン デバイスの技術的な能力によって決まります。

スキャンが返されるデータのもう 1 つの重要な側面では、取得したデータのメトリックスです。 スキャン デバイスを返すすべてのイメージ データは、白、黒が 0 で表され、空白が 1 で表される場所の上に黒にする必要があります。

## <a name="see-also"></a>関連項目


[**ADFBack**](adfback.md)

[**ADFFront**](adffront.md)

[**ColorEntry**](colorentry.md)

 

 







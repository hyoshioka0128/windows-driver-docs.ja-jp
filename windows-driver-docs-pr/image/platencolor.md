---
title: PlatenColor 要素
description: 必要な PlatenColor 要素には、処理機能からプラテン上の色を記述した ColorEntry 要素の一覧が含まれています。
ms.assetid: 97fd9926-e49d-4b4f-95aa-eb4142c353a3
keywords:
- PlatenColor 要素イメージング デバイス
topic_type:
- apiref
api_name:
- wscn PlatenColor
api_type:
- Schema
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8e53812c0462a87a249d087387f762bbb90dcc1a
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56530993"
---
# <a name="platencolor-element"></a>PlatenColor 要素


必要な**PlatenColor**要素の一覧を含む[ **ColorEntry** ](colorentry.md)からプラテン上の機能を処理する色を記述する要素。

<a name="usage"></a>使用方法
-----

```xml
<wscn:PlatenColor>
  child elements
</wscn:PlatenColor>
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
<td><p><a href="platen.md" data-raw-source="[&lt;strong&gt;Platen&lt;/strong&gt;](platen.md)"><strong>プラテン</strong></a></p></td>
</tr>
</tbody>
</table>

<a name="remarks"></a>注釈
-------

**PlatenColor**要素には色の処理と取得ベッドからプラテン上をサポートする種類を決定するための情報が含まれています。 各ピクセルの記述に必要な情報の量が特定の依存[ **ColorEntry** ](colorentry.md)キーワード。 白と黒のイメージでは、グレースケールおよびカラーの画像がはるかに多くの情報が必要ですが、1 つのビット/ピクセル (bpp) のみが必要です。 正確な情報量は、色空間とスキャン デバイスの技術的な能力によって決まります。

スキャンが返されるデータのもう 1 つの重要な側面では、取得したデータのメトリックスです。 スキャン デバイスを返すすべてのイメージ データは、白、黒が 0 で表され、空白が 1 で表される場所の上に黒にする必要があります。

## <a name="see-also"></a>関連項目


[**ColorEntry**](colorentry.md)

[**プラテン**](platen.md)

 

 







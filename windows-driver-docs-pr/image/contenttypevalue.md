---
title: ContentTypeValue 要素
description: 必要な ContentTypeValue 要素には、デバイスのスキャンをサポートする 1 つのドキュメントのコンテンツ タイプを指定します。
ms.assetid: 04d29626-cc14-4db3-88ec-cfb1cc9cd1cd
keywords:
- ContentTypeValue 要素イメージング デバイス
topic_type:
- apiref
api_name:
- wscn ContentTypeValue
api_type:
- Schema
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 11e8190515e51182546dda1c6013d0b551940fb3
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56530847"
---
# <a name="contenttypevalue-element"></a>ContentTypeValue 要素


必要な**ContentTypeValue**要素は、デバイスのスキャンをサポートする 1 つのドキュメントのコンテンツ タイプを指定します。

<a name="usage"></a>使用方法
-----

```xml
<wscn:ContentTypeValue>
  text
</wscn:ContentTypeValue>
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
<td><p><span id="Auto_"></span><span id="auto_"></span><span id="AUTO_"></span>自動</p></td>
<td><p>デバイスでは、元のドキュメントの種類を自動的に検出されます。</p></td>
</tr>
<tr class="even">
<td><p><span id="Text_"></span><span id="text_"></span><span id="TEXT_"></span>テキスト</p></td>
<td><p>元のドキュメントは主に、バック グラウンドで厳密には対照的です。 個別のテキストで構成されます。</p></td>
</tr>
<tr class="odd">
<td><p><span id="Photo_"></span><span id="photo_"></span><span id="PHOTO_"></span>写真</p></td>
<td><p>元のドキュメントは主に、写真の画像、階調が段階的に変更して、エッジは個別ではない場所で構成されます。</p></td>
</tr>
<tr class="even">
<td><p><span id="Halftone_"></span><span id="halftone_"></span><span id="HALFTONE_"></span>ハーフトーン</p></td>
<td><p>元は主に、ハーフトーン イメージで構成されます。</p></td>
</tr>
<tr class="odd">
<td><p><span id="Mixed_"></span><span id="mixed_"></span><span id="MIXED_"></span>混合</p></td>
<td><p>元のドキュメントは、1 つ以上の特定のドキュメントのコンテンツ タイプの特性を持つマルチページ ドキュメントです。</p></td>
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
<td><p><a href="contenttypessupported.md" data-raw-source="[&lt;strong&gt;ContentTypesSupported&lt;/strong&gt;](contenttypessupported.md)"><strong>ContentTypesSupported</strong></a></p></td>
</tr>
</tbody>
</table>

<a name="remarks"></a>注釈
-------

両方を拡張して一部この要素に使用できる値。

## <a name="see-also"></a>関連項目


[**ContentTypesSupported**](contenttypessupported.md)

 

 







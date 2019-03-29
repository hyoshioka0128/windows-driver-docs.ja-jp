---
title: FormatsSupported 要素
description: 必要な FormatsSupported 要素は、スキャナーをサポートするドキュメントのファイル形式を一覧表示する要素のコレクションです。
ms.assetid: bb4b6630-f865-4ec7-b7d1-8be424eea345
keywords:
- FormatsSupported 要素イメージング デバイス
topic_type:
- apiref
api_name:
- wscn FormatsSupported
api_type:
- Schema
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2bad45d7596eaa74b301cac0ee71f9cde250329a
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56579041"
---
# <a name="formatssupported-element"></a>FormatsSupported 要素


必要な**FormatsSupported**要素は、スキャナーをサポートするドキュメントのファイル形式を一覧表示する要素のコレクション。

<a name="usage"></a>使用方法
-----

```xml
<wscn:FormatsSupported>
  child elements
</wscn:FormatsSupported>
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
<td><p><a href="formatvalue.md" data-raw-source="[&lt;strong&gt;FormatValue&lt;/strong&gt;](formatvalue.md)"><strong>FormatValue</strong></a></p></td>
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
<td><p><a href="devicesettings.md" data-raw-source="[&lt;strong&gt;DeviceSettings&lt;/strong&gt;](devicesettings.md)"><strong>DeviceSettings</strong></a></p></td>
</tr>
</tbody>
</table>

<a name="remarks"></a>コメント
-------

各[ **FormatValue** ](formatvalue.md)要素は、ファイルの種類と圧縮の種類を記述するファイル形式を指定します。

## <a name="see-also"></a>関連項目


[**DeviceSettings**](devicesettings.md)

[**FormatValue**](formatvalue.md)

 

 







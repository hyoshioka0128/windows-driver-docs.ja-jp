---
title: DocumentSizeAutoDetect 要素
description: 省略可能な DocumentSizeAutoDetect 要素では、デバイスのスキャンが自動的にスキャンの元のメディアのサイズを決定かどうかを指定します。
ms.assetid: 509e96d8-c99b-4d6e-9117-b9aed199da2c
keywords:
- DocumentSizeAutoDetect 要素イメージング デバイス
topic_type:
- apiref
api_name:
- wscn DocumentSizeAutoDetect
api_type:
- Schema
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: d93d6da03e3a1904a1e905e63ce223ef3500ea99
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56572724"
---
# <a name="documentsizeautodetect-element"></a>DocumentSizeAutoDetect 要素


省略可能な**DocumentSizeAutoDetect**要素は、デバイスのスキャンが自動的にスキャンの元のメディアのサイズを決定かどうかを指定します。

<a name="usage"></a>使用方法
-----

```xml
<wscn:DocumentSizeAutoDetect>
  text
</wscn:DocumentSizeAutoDetect>
```

<a name="attributes"></a>属性
----------

属性はありません。

<a name="text-value"></a>テキスト値
----------

必須。 ブール値 false、0 にする必要がある、1 または true です。**falsetrue**

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
<td><p><a href="inputsize.md" data-raw-source="[&lt;strong&gt;InputSize&lt;/strong&gt;](inputsize.md)"><strong>InputSize</strong></a></p></td>
</tr>
</tbody>
</table>

<a name="remarks"></a>コメント
-------

指定したテキスト値が 1 の場合、または**true**デバイスのスキャンが自動的にスキャンの元のメディアのサイズを決定します。 場合、 **DocumentSizeAutoDetect**と共に要素が指定されて、 [ **ScanRegion** ](scanregion.md)要素の外側にある場合、スキャンのリージョンは無視されます、メディアのサイズをデバイスが検出されました。

## <a name="see-also"></a>関連項目


[**ScanRegion**](scanregion.md)

[**InputSize**](inputsize.md)

 

 







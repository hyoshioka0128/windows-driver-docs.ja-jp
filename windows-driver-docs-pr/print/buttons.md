---
title: buttons 要素
description: 必須ボタン要素は、クライアントコンピューターのイベント通知メッセージボックスに表示される1つ以上のボタンを指定します。
ms.assetid: bf3718c0-37d9-4b73-a015-8a5a95535381
keywords:
- ボタン要素の印刷デバイス
topic_type:
- apiref
api_name:
- buttons
api_type:
- Schema
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 109dbaff5b4ed89287c4370378fa004ed3fb89fb
ms.sourcegitcommit: ee1fc949d1ae5eb14df4530758f767702a886e36
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/20/2019
ms.locfileid: "71164796"
---
# <a name="buttons-element"></a>buttons 要素


必須**ボタン**要素は、クライアントコンピューターのイベント通知メッセージボックスに表示される1つ以上のボタンを指定します。

**ボタン**で要素が定義されている、 *asyncui*この URI に、名前空間: http://schemas.microsoft.com/2003/print/asyncui/v1/request します。 (このリソースは、一部の言語および国では使用できません。)

<a name="usage"></a>使用方法
-----

```xml
<buttons>
  child elements
</buttons>
```

<a name="attributes"></a>属性
----------

属性はありません。

## <a name="child-elements"></a>子要素


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
<td><p><a href="button.md" data-raw-source="[&lt;strong&gt;button&lt;/strong&gt;](button.md)"><strong>;</strong></a></p></td>
<td><p></p>
<p>クライアントコンピューターに表示される、メッセージボックス内のボタンの特性を指定する必須の要素。</p></td>
</tr>
</tbody>
</table>

## <a name="parent-elements"></a>親要素


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
<td><p><a href="messageboxui.md" data-raw-source="[&lt;strong&gt;messageBoxUI&lt;/strong&gt;](messageboxui.md)"><strong>messageBoxUI</strong></a></p></td>
<td><p></p>
<p>クライアントコンピューターにメッセージボックスを表示するために使用される省略可能な要素。</p></td>
</tr>
</tbody>
</table>

<a name="remarks"></a>コメント
-------

**ボタン要素を**使用して、 **[OK]** と **[キャンセル**] ボタンを表示する2つの**ボタン**要素を囲む方法を示すコード例については、「[**ボタン**](button.md)」を参照してください。

## <a name="see-also"></a>関連項目

[;](button.md)

[messageBoxUI](messageboxui.md)

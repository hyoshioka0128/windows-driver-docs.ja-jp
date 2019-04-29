---
title: Buttons 要素
description: 必須ボタン要素では、クライアント コンピューターは 1 つまたは複数のボタンに通知のメッセージ ボックス表示イベントを指定します。
ms.assetid: bf3718c0-37d9-4b73-a015-8a5a95535381
keywords:
- buttons 要素印刷デバイス
topic_type:
- apiref
api_name:
- buttons
api_type:
- Schema
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: a7e40fb775bd3f68c4de1e5d5821f1610981483d
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63330453"
---
# <a name="buttons-element"></a>Buttons 要素


必要な**ボタン**要素は、クライアント コンピューターは 1 つまたは複数のボタンに通知のメッセージ ボックス表示イベントを指定します。

**ボタン**で要素が定義されている、 *asyncui*この URI に、名前空間:http://schemas.microsoft.com/2003/print/asyncui/v1/requestします。 (このリソースできない場合がありますのいくつかの言語および国。)

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
<td><p><a href="button.md" data-raw-source="[&lt;strong&gt;button&lt;/strong&gt;](button.md)"><strong>ボタン</strong></a></p></td>
<td><p></p>
<p>クライアント コンピューターに表示されるメッセージ ボックスのボタンの特性を指定する必須の要素。</p></td>
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
<p>クライアント コンピューターのメッセージ ボックスを表示するために使用する省略可能な要素です。</p></td>
</tr>
</tbody>
</table>

<a name="remarks"></a>注釈
-------

参照してください[**ボタン**](button.md)を使用する方法を示すコード exapmle、**ボタン**要素に 2 つ**ボタン**を表示する要素 **[Ok]** と**キャンセル**ボタンをクリックします。

## <a name="see-also"></a>関連項目

[ボタン](button.md)

[messageBoxUI](messageboxui.md)

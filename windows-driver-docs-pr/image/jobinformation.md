---
title: JobInformation 要素
description: 省略可能な JobInformation 要素には、ジョブの使用目的について説明します。
ms.assetid: 0e5d41a0-49df-43db-a2e6-3639e60d2378
keywords:
- JobInformation 要素イメージング デバイス
topic_type:
- apiref
api_name:
- wscn JobInformation
api_type:
- Schema
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 698fd1680e7b21b69f4a952b6178565c1a837bf6
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63348809"
---
# <a name="jobinformation-element"></a>JobInformation 要素


省略可能な**JobInformation**要素が、ジョブの使用目的について説明します。

<a name="usage"></a>使用方法
-----

```xml
<wscn:JobInformation>
  text
</wscn:JobInformation>
```

<a name="attributes"></a>属性
----------

属性はありません。

<a name="text-value"></a>テキスト値
----------

必須。 任意の有効な文字の文字列。

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
<td><p><a href="jobdescription.md" data-raw-source="[&lt;strong&gt;JobDescription&lt;/strong&gt;](jobdescription.md)"><strong>JobDescription</strong></a></p></td>
</tr>
</tbody>
</table>

<a name="remarks"></a>注釈
-------

**JobInformation**値は、クライアントは、ジョブの作成に使用されるスキャンのチケットを再利用するときに役立ちます。

## <a name="see-also"></a>関連項目


[**JobDescription**](jobdescription.md)

 

 







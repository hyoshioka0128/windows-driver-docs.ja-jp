---
title: JobCompletedTime 要素
description: 省略可能な JobCompletedTime 要素には、スキャン ジョブが完了した時刻を指定します。
ms.assetid: f29449bd-c618-400f-b37c-3df7d955936b
keywords:
- JobCompletedTime 要素イメージング デバイス
topic_type:
- apiref
api_name:
- wscn JobCompletedTime
api_type:
- Schema
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9079cfc72c1736aaa82e0a8ccc5f390cc33f64e1
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56556787"
---
# <a name="jobcompletedtime-element"></a>JobCompletedTime 要素


省略可能な**JobCompletedTime**要素がスキャン ジョブが完了した時刻を指定します。

<a name="usage"></a>使用方法
-----

```xml
<wscn:JobCompletedTime>
  text
</wscn:JobCompletedTime>
```

<a name="attributes"></a>属性
----------

属性はありません。

<a name="text-value"></a>テキスト値
----------

必須。 DateTime 型の任意の有効な値。 DateTime の詳細については、XML Schema Part 2 を参照してください。Datatypes Second Edition。**dateTimedateTime**

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
<td><p><a href="jobendstate.md" data-raw-source="[&lt;strong&gt;JobEndState&lt;/strong&gt;](jobendstate.md)"><strong>JobEndState</strong></a></p></td>
</tr>
<tr class="even">
<td><p><a href="jobstatus.md" data-raw-source="[&lt;strong&gt;JobStatus&lt;/strong&gt;](jobstatus.md)"><strong>JobStatus</strong></a></p></td>
</tr>
</tbody>
</table>

<a name="remarks"></a>注釈
-------

スキャン ジョブが*完了*すべての処理が完了すると、スキャンおよびドキュメントの転送が正常に完了しましたので、または致命的なエラーが発生したためです。

指定した時間は、スキャン デバイスの内部時計は参照し、するリアルタイム クロックがある必要はありません。

## <a name="see-also"></a>関連項目


[**JobEndState**](jobendstate.md)

[**JobStatus**](jobstatus.md)

 

 







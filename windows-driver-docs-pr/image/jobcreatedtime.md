---
title: JobCreatedTime 要素
description: 省略可能な JobCreatedTime 要素には、ジョブが作成された時刻を指定します。
ms.assetid: 34107c3a-d02a-4b86-be1e-cd91e2887479
keywords:
- JobCreatedTime 要素イメージング デバイス
topic_type:
- apiref
api_name:
- wscn JobCreatedTime
api_type:
- Schema
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 230892171a1f54640a0a0994bb45ab27b449795d
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56529991"
---
# <a name="jobcreatedtime-element"></a>JobCreatedTime 要素


省略可能な**JobCreatedTime**要素は、ジョブが作成された時刻を指定します。

<a name="usage"></a>使用方法
-----

```xml
<wscn:JobCreatedTime>
  text
</wscn:JobCreatedTime>
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
<td><p><a href="jobstatus.md" data-raw-source="[&lt;strong&gt;JobStatus&lt;/strong&gt;](jobstatus.md)"><strong>JobStatus</strong></a></p></td>
</tr>
</tbody>
</table>

<a name="remarks"></a>注釈
-------

ジョブが*作成*システムにジョブを送信する場合。

指定した時間は、スキャン デバイスの内部時計は参照し、するリアルタイム クロックがある必要はありません。

## <a name="see-also"></a>関連項目


[**JobStatus**](jobstatus.md)

 

 







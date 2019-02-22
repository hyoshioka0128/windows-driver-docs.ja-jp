---
title: Time 要素
description: 必要な時間要素には、条件が発生した時刻を指定します。
ms.assetid: 1a10f6b4-1fcd-4697-9eb4-d58cca9c4a23
keywords:
- Time 要素イメージング デバイス
topic_type:
- apiref
api_name:
- wscn Time
api_type:
- Schema
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: faa632366a8f5496e896493d6866f450dd93fa94
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56528205"
---
# <a name="time-element"></a>Time 要素


必要な**時間**要素は、条件が発生した時刻を指定します。

<a name="usage"></a>使用方法
-----

```xml
<wscn:Time>
  text
</wscn:Time>
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
<td><p><a href="conditionhistoryentry.md" data-raw-source="[&lt;strong&gt;ConditionHistoryEntry&lt;/strong&gt;](conditionhistoryentry.md)"><strong>ConditionHistoryEntry</strong></a></p></td>
</tr>
<tr class="even">
<td><p><a href="devicecondition.md" data-raw-source="[&lt;strong&gt;DeviceCondition&lt;/strong&gt;](devicecondition.md)"><strong>DeviceCondition</strong></a></p></td>
</tr>
</tbody>
</table>

<a name="remarks"></a>注釈
-------

指定した**時間**スキャナーの内部時計に照らしたの。

## <a name="see-also"></a>関連項目


[**ConditionHistoryEntry**](conditionhistoryentry.md)

[**DeviceCondition**](devicecondition.md)

 

 







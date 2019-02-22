---
title: ClearTime 要素
description: 必要な ClearTime 要素は、条件がクリアされました時間を指定します。
ms.assetid: 9b5fe054-f3fa-402a-8337-8fd181679080
keywords:
- ClearTime 要素イメージング デバイス
topic_type:
- apiref
api_name:
- wscn ClearTime
api_type:
- Schema
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: e746ab7ee87f023eeb3ad4c3b42308c776cb8680
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56548614"
---
# <a name="cleartime-element"></a>ClearTime 要素


必要な**ClearTime**要素の条件がクリアされました時間を指定します。

<a name="usage"></a>使用方法
-----

```xml
<wscn:ClearTime>
  text
</wscn:ClearTime>
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
</tbody>
</table>

<a name="remarks"></a>注釈
-------

指定した時間は、スキャナーの内部時計に照らしたの。

## <a name="see-also"></a>関連項目


[**ConditionHistoryEntry**](conditionhistoryentry.md)

 

 







---
title: JobCompletedState 要素
description: 必要な JobCompletedState 要素には、ジョブの最後のジョブの状態を指定します。
ms.assetid: 41dc029b-2315-465a-8490-1f4e50db0188
keywords:
- JobCompletedState 要素イメージング デバイス
topic_type:
- apiref
api_name:
- wscn JobCompletedState
api_type:
- Schema
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: a3fe870e85fe31bd6689ae712e9732c11324cb17
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56579817"
---
# <a name="jobcompletedstate-element"></a>JobCompletedState 要素


必要な**JobCompletedState**要素は、ジョブの最後のジョブの状態を指定します。

<a name="usage"></a>使用方法
-----

```xml
<wscn:JobCompletedState>
  text
</wscn:JobCompletedState>
```

<a name="attributes"></a>属性
----------

属性はありません。

<a name="text-value"></a>テキスト値
----------

必須。 次のいずれかの値、 [ **JobState** ](jobstate.md)要素。

-   中止されました
-   Canceled
-   完了
-   終了しています

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
</tbody>
</table>

<a name="remarks"></a>コメント
-------

WSD スキャン サービスに送信する**JobCompletedState**要素内でクライアントを[ **JobEndStateEvent** ](jobendstateevent.md)イベント要素。

## <a name="see-also"></a>関連項目


[**JobEndState**](jobendstate.md)

[**JobEndStateEvent**](jobendstateevent.md)

[**JobState**](jobstate.md)

 

 







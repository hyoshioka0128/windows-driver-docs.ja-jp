---
title: JobCompletedStateReasons 要素
description: 必要な JobCompletedStateReasons 要素は、スキャン ジョブが完了する方法と理由に関する追加情報をすべてのコレクションです。
ms.assetid: 678384b4-a023-4c79-a68a-4a2cc3a04a0e
keywords:
- JobCompletedStateReasons 要素イメージング デバイス
topic_type:
- apiref
api_name:
- wscn JobCompletedStateReasons
api_type:
- Schema
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0e1c9c8bc56daa957ae99bb762e863bd2ad16c24
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56571192"
---
# <a name="jobcompletedstatereasons-element"></a>JobCompletedStateReasons 要素


必要な**JobCompletedStateReasons**要素は、スキャン ジョブが完了する方法と理由に関する追加情報をすべてのコレクション。

<a name="usage"></a>使用方法
-----

```xml
<wscn:JobCompletedStateReasons>
  child elements
</wscn:JobCompletedStateReasons>
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
<td><p><a href="jobstatereason.md" data-raw-source="[&lt;strong&gt;JobStateReason&lt;/strong&gt;](jobstatereason.md)"><strong>JobStateReason</strong></a></p></td>
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
<td><p><a href="jobendstate.md" data-raw-source="[&lt;strong&gt;JobEndState&lt;/strong&gt;](jobendstate.md)"><strong>JobEndState</strong></a></p></td>
</tr>
</tbody>
</table>

<a name="remarks"></a>コメント
-------

**JobCompletedStateReasons**要素は、0 個以上含まれています。 [ **JobStateReason** ](jobstatereason.md)スキャン ジョブが完了する方法や理由の理由を含む要素。 WSD スキャン サービスの送信、 **JobCompletedStateReasons**要素を使用してクライアントを[ **JobEndStateEvent** ](jobendstateevent.md)イベント要素。

## <a name="see-also"></a>関連項目


[**JobEndState**](jobendstate.md)

[**JobEndStateEvent**](jobendstateevent.md)

[**JobStateReason**](jobstatereason.md)

 

 







---
title: JobEndState 要素
description: 必要な JobEndState 要素には、現在のスキャン ジョブの最終状態について説明します。
ms.assetid: c69b5988-ca0d-441f-9b65-e5692a17ccb3
keywords:
- JobEndState 要素イメージング デバイス
topic_type:
- apiref
api_name:
- wscn JobEndState
api_type:
- Schema
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1137667a5f0640aad6510bd540ea05545f278bfe
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63348836"
---
# <a name="jobendstate-element"></a>JobEndState 要素


必要な**JobEndState**要素には、現在のスキャン ジョブの最終状態がについて説明します。

<a name="usage"></a>使用方法
-----

```xml
<wscn:JobEndState>
  child elements
</wscn:JobEndState>
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
<td><p><a href="jobcompletedstate.md" data-raw-source="[&lt;strong&gt;JobCompletedState&lt;/strong&gt;](jobcompletedstate.md)"><strong>JobCompletedState</strong></a></p></td>
</tr>
<tr class="even">
<td><p><a href="jobcompletedstatereasons.md" data-raw-source="[&lt;strong&gt;JobCompletedStateReasons&lt;/strong&gt;](jobcompletedstatereasons.md)"><strong>JobCompletedStateReasons</strong></a></p></td>
</tr>
<tr class="odd">
<td><p><a href="jobcompletedtime.md" data-raw-source="[&lt;strong&gt;JobCompletedTime&lt;/strong&gt;](jobcompletedtime.md)"><strong>JobCompletedTime</strong></a></p></td>
</tr>
<tr class="even">
<td><p><a href="jobid.md" data-raw-source="[&lt;strong&gt;JobId&lt;/strong&gt;](jobid.md)"><strong>JobId</strong></a></p></td>
</tr>
<tr class="odd">
<td><p><a href="jobname.md" data-raw-source="[&lt;strong&gt;JobName&lt;/strong&gt;](jobname.md)"><strong>JobName</strong></a></p></td>
</tr>
<tr class="even">
<td><p><a href="joboriginatingusername.md" data-raw-source="[&lt;strong&gt;JobOriginatingUserName&lt;/strong&gt;](joboriginatingusername.md)"><strong>JobOriginatingUserName</strong></a></p></td>
</tr>
<tr class="odd">
<td><p><a href="scanscompleted.md" data-raw-source="[&lt;strong&gt;ScansCompleted&lt;/strong&gt;](scanscompleted.md)"><strong>ScansCompleted</strong></a></p></td>
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
<td><p><a href="jobendstateevent.md" data-raw-source="[&lt;strong&gt;JobEndStateEvent&lt;/strong&gt;](jobendstateevent.md)"><strong>JobEndStateEvent</strong></a></p></td>
</tr>
</tbody>
</table>

<a name="remarks"></a>注釈
-------

**JobEndState**要素には、スキャン ジョブの終了の状態に関するさまざまな側面を記述する子要素が含まれています。 WSD スキャン サービスに送信する**JobEndState**要素を使用して、クライアントを[ **JobEndStateEvent** ](jobendstateevent.md)要素。

## <a name="see-also"></a>関連項目


[**JobCompletedState**](jobcompletedstate.md)

[**JobCompletedStateReasons**](jobcompletedstatereasons.md)

[**JobCompletedTime**](jobcompletedtime.md)

[**JobEndStateEvent**](jobendstateevent.md)

[**JobId**](jobid.md)

[**JobName**](jobname.md)

[**JobOriginatingUserName**](joboriginatingusername.md)

[**ScansCompleted**](scanscompleted.md)

 

 







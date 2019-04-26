---
title: JobStatus 要素
description: 必要な JobStatus 要素には、現在のスキャン ジョブの状態に関するすべての情報が含まれています。
ms.assetid: e3eb2cc7-70a4-4ae0-8569-4a91f2b42228
keywords:
- JobStatus 要素イメージング デバイス
topic_type:
- apiref
api_name:
- wscn JobStatus
api_type:
- Schema
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: f35d316dce2ee7103f6cb74432ce6acaa772c6b1
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63348768"
---
# <a name="jobstatus-element"></a>JobStatus 要素


必要な**JobStatus**要素には、現在のスキャン ジョブの状態に関するすべての情報が含まれています。

<a name="usage"></a>使用方法
-----

```xml
<wscn:JobStatus>
  child elements
</wscn:JobStatus>
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
<td><p><a href="jobcompletedtime.md" data-raw-source="[&lt;strong&gt;JobCompletedTime&lt;/strong&gt;](jobcompletedtime.md)"><strong>JobCompletedTime</strong></a></p></td>
</tr>
<tr class="even">
<td><p><a href="jobcreatedtime.md" data-raw-source="[&lt;strong&gt;JobCreatedTime&lt;/strong&gt;](jobcreatedtime.md)"><strong>JobCreatedTime</strong></a></p></td>
</tr>
<tr class="odd">
<td><p><a href="jobid.md" data-raw-source="[&lt;strong&gt;JobId&lt;/strong&gt;](jobid.md)"><strong>JobId</strong></a></p></td>
</tr>
<tr class="even">
<td><p><a href="jobstate.md" data-raw-source="[&lt;strong&gt;JobState&lt;/strong&gt;](jobstate.md)"><strong>JobState</strong></a></p></td>
</tr>
<tr class="odd">
<td><p><a href="jobstatereasons.md" data-raw-source="[&lt;strong&gt;JobStateReasons&lt;/strong&gt;](jobstatereasons.md)"><strong>JobStateReasons</strong></a></p></td>
</tr>
<tr class="even">
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
<td><p><a href="job.md" data-raw-source="[&lt;strong&gt;Job&lt;/strong&gt;](job.md)"><strong>ジョブ</strong></a></p></td>
</tr>
</tbody>
</table>

<a name="remarks"></a>注釈
-------

**JobStatus**オートマトンを介して子要素が保持されます。 WSD スキャン サービスを更新する必要があります**JobStatus**要素、ジョブを処理する際に、それに応じて。 クライアントの操作など[ **CancelJobRequest**](canceljobrequest.md)ジョブの状態は直接影響します。

WSD スキャン サービスを介して、ジョブの状態の変更点についてクライアントに通知を[ **JobStatusEvent** ](jobstatusevent.md)イベント要素。 WSD スキャン サービスは、生成、 **JobStatusEvent**要素すべてに対するすべての変更の**JobStatus**子要素。

クライアントからジョブの状態を照会できます、 [ **GetJobElementsRequest** ](getjobelementsrequest.md)操作。

## <a name="see-also"></a>関連項目


[**CancelJobRequest**](canceljobrequest.md)

[**GetJobElementsRequest**](getjobelementsrequest.md)

[**ジョブ**](job.md)

[**JobCompletedTime**](jobcompletedtime.md)

[**JobCreatedTime**](jobcreatedtime.md)

[**JobId**](jobid.md)

[**JobState**](jobstate.md)

[**JobStateReasons**](jobstatereasons.md)

[**JobStatusEvent**](jobstatusevent.md)

[**ScansCompleted**](scanscompleted.md)

 

 







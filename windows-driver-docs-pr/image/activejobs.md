---
title: ActiveJobs 要素
description: 必要な ActiveJobs 要素には、すべてのスキャンが現在アクティブなジョブの一覧が含まれています。
ms.assetid: 90acd196-60d3-43e5-9346-a8514bcf0bb8
keywords:
- ActiveJobs 要素イメージング デバイス
topic_type:
- apiref
api_name:
- wscn ActiveJobs
api_type:
- Schema
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 699d78e8a7223a1bb6c1d3bd5c52b3045430ccbc
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56549587"
---
# <a name="activejobs-element"></a>ActiveJobs 要素


必要な**ActiveJobs**要素には、すべてのスキャンが現在アクティブなジョブの一覧が含まれています。

<a name="usage"></a>使用方法
-----

```xml
<wscn:ActiveJobs>
  child elements
</wscn:ActiveJobs>
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
<td><p><a href="job.md" data-raw-source="[&lt;strong&gt;Job&lt;/strong&gt;](job.md)"><strong>ジョブ</strong></a></p></td>
</tr>
<tr class="even">
<td><p><a href="jobsummary.md" data-raw-source="[&lt;strong&gt;JobSummary&lt;/strong&gt;](jobsummary.md)"><strong>JobSummary</strong></a></p></td>
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
<td><p><a href="getactivejobsresponse.md" data-raw-source="[&lt;strong&gt;GetActiveJobsResponse&lt;/strong&gt;](getactivejobsresponse.md)"><strong>GetActiveJobsResponse</strong></a></p></td>
</tr>
<tr class="even">
<td><p><a href="jobtable.md" data-raw-source="[&lt;strong&gt;JobTable&lt;/strong&gt;](jobtable.md)"><strong>JobTable</strong></a></p></td>
</tr>
</tbody>
</table>

<a name="remarks"></a>注釈
-------

**ActiveJobs**要素には、処理が完了していないすべてのジョブが含まれています。 アクティブなジョブの状態をスキャンすることが、保留中、または停止します。 **ActiveJobs**が空の場合、現在アクティブなジョブはありません。

クライアントからのアクティブなジョブの一覧を求める、 [ **GetActiveJobsRequest** ](getactivejobsrequest.md)操作。 WSD スキャン サービスの一覧を返します、 [ **GetActiveJobsResponse** ](getactivejobsresponse.md)操作の要素。

## <a name="see-also"></a>関連項目


[**GetActiveJobsRequest**](getactivejobsrequest.md)

[**GetActiveJobsResponse**](getactivejobsresponse.md)

[**ジョブ**](job.md)

[**JobSummary**](jobsummary.md)

[**JobTable**](jobtable.md)

 

 







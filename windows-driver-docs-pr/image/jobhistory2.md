---
title: JobHistory 要素
description: 省略可能な JobHistory 要素には、処理が完了して最近スキャン ジョブに関する情報が含まれています。
ms.assetid: 7f46044e-ac34-4181-9a35-62dea5ec8c82
keywords:
- JobHistory 要素イメージング デバイス
topic_type:
- apiref
api_name:
- wscn JobHistory
api_type:
- Schema
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: aa969d68f4f86dfbd07ac6019cb34977826f3b3c
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63377598"
---
# <a name="jobhistory-element"></a>JobHistory 要素


省略可能な**JobHistory**要素には、処理が完了して最近スキャン ジョブに関する情報が含まれています。

<a name="usage"></a>使用方法
-----

```xml
<wscn:JobHistory>
  child elements
</wscn:JobHistory>
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
<td><p><a href="getjobhistoryresponse.md" data-raw-source="[&lt;strong&gt;GetJobHistoryResponse&lt;/strong&gt;](getjobhistoryresponse.md)"><strong>GetJobHistoryResponse</strong></a></p></td>
</tr>
<tr class="even">
<td><p><a href="jobtable.md" data-raw-source="[&lt;strong&gt;JobTable&lt;/strong&gt;](jobtable.md)"><strong>JobTable</strong></a></p></td>
</tr>
</tbody>
</table>

<a name="remarks"></a>注釈
-------

**JobHistory**要素には、処理が完了したら、最新のジョブのサブセットが含まれています。 これらのジョブでしたスキャン、中止、またはされたその他の理由で失敗しました。 この一覧内のジョブの最大数は、デバイスに依存します。

クライアントからのジョブ履歴を求める、 [ **GetJobHistoryRequest** ](getjobhistoryrequest.md)操作の要素。 WSD スキャン サービスでは、この履歴を返します、 [ **GetJobHistoryResponse** ](getjobhistoryresponse.md)操作の要素。

## <a name="see-also"></a>関連項目


[**GetJobHistoryRequest**](getjobhistoryrequest.md)

[**GetJobHistoryResponse**](getjobhistoryresponse.md)

[**ジョブ**](job.md)

[**JobSummary**](jobsummary.md)

[**JobTable**](jobtable.md)

 

 







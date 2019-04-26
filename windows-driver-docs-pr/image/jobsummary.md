---
title: JobSummary 要素
description: 省略可能な JobSummary 要素には、スキャン ジョブに関する概要が含まれています。
ms.assetid: db81cad5-d157-403c-b3a4-1e5f91f858da
keywords:
- JobSummary 要素イメージング デバイス
topic_type:
- apiref
api_name:
- wscn JobSummary
api_type:
- Schema
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: b3fcd642a6fc31146f9f0d7abb4b5c2cbf1ce60a
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63348757"
---
# <a name="jobsummary-element"></a>JobSummary 要素


省略可能な**JobSummary**要素には、スキャン ジョブに関する概要が含まれています。

<a name="usage"></a>使用方法
-----

```xml
<wscn:JobSummary>
  child elements
</wscn:JobSummary>
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
<td><p><a href="jobid.md" data-raw-source="[&lt;strong&gt;JobId&lt;/strong&gt;](jobid.md)"><strong>JobId</strong></a></p></td>
</tr>
<tr class="even">
<td><p><a href="jobname.md" data-raw-source="[&lt;strong&gt;JobName&lt;/strong&gt;](jobname.md)"><strong>JobName</strong></a></p></td>
</tr>
<tr class="odd">
<td><p><a href="joboriginatingusername.md" data-raw-source="[&lt;strong&gt;JobOriginatingUserName&lt;/strong&gt;](joboriginatingusername.md)"><strong>JobOriginatingUserName</strong></a></p></td>
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
<td><p><a href="activejobs.md" data-raw-source="[&lt;strong&gt;ActiveJobs&lt;/strong&gt;](activejobs.md)"><strong>ActiveJobs</strong></a></p></td>
</tr>
<tr class="even">
<td><p><a href="jobhistory.md" data-raw-source="[&lt;strong&gt;JobHistory&lt;/strong&gt;](jobhistory.md)"><strong>JobHistory</strong></a></p></td>
</tr>
</tbody>
</table>

<a name="remarks"></a>注釈
-------

場合の親要素、 **JobSummary**要素は[ **ActiveJobs**](activejobs.md)、 **JobSummary** 1 つのジョブに関する情報の要約を含むスキャン デバイス内で現在アクティブなです。

親要素がある場合[ **JobHistory**](jobhistory.md)、 **JobSummary**スキャン デバイス内の 1 つ、最近完了したジョブに関する情報の概要が含まれています。

## <a name="see-also"></a>関連項目


[**ActiveJobs**](activejobs.md)

[**JobHistory**](jobhistory.md)

[**JobId**](jobid.md)

[**JobName**](jobname.md)

[**JobOriginatingUserName**](joboriginatingusername.md)

[**JobState**](jobstate.md)

[**JobStateReasons**](jobstatereasons.md)

[**ScansCompleted**](scanscompleted.md)

 

 







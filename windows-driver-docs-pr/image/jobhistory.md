---
title: JobHistory 要素
description: 必要な JobHistory 要素には、デバイスのスキャンで最近完了したジョブを記述した JobSummary 要素の一覧が含まれています。
ms.assetid: d1439e56-b2fe-4db8-b063-56537a3346c6
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
ms.openlocfilehash: 95af97b65234292312176e43e56c3edcae44db36
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63377608"
---
# <a name="jobhistory-element"></a>JobHistory 要素


必要な**JobHistory**要素の一覧を含む[ **JobSummary** ](jobsummary.md)最後を記述する要素がデバイスのスキャンでのジョブを完了します。

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
</tbody>
</table>

<a name="remarks"></a>注釈
-------

**JobHistory**要素が含まれています、 [ **JobSummary** ](jobsummary.md)スキャナーが最近完了したジョブのすべての要素。 **JobHistory** WSD スキャン サービスには、最近完了したジョブのレコードがあるない場合は空です。 スキャン サービスからこの一覧を返します[ **GetJobHistoryResponse**](getjobhistoryresponse.md)します。

WSD スキャン サービスを格納して返すジョブの履歴の量は、実装に固有です。

## <a name="see-also"></a>関連項目


[**GetJobHistoryResponse**](getjobhistoryresponse.md)

[**JobSummary**](jobsummary.md)

 

 







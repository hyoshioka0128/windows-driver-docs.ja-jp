---
title: ジョブ要素
description: ジョブの必須の要素には、スキャン ジョブに関連付けられているすべての要素が含まれています。
ms.assetid: c5622ea6-c57a-4c80-a6ef-e6b9014b2b59
keywords:
- ジョブ要素イメージング デバイス
topic_type:
- apiref
api_name:
- wscn Job
api_type:
- Schema
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: c1608d20448afa736b8c0f69f965776e423810ab
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63381644"
---
# <a name="job-element"></a>ジョブ要素


必要な**ジョブ**要素には、スキャン ジョブに関連付けられているすべての要素が含まれています。

<a name="usage"></a>使用方法
-----

```xml
<wscn:Job>
  child elements
</wscn:Job>
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
<td><p><a href="documents.md" data-raw-source="[&lt;strong&gt;Documents&lt;/strong&gt;](documents.md)"><strong>ドキュメント</strong></a></p></td>
</tr>
<tr class="even">
<td><p><a href="jobstatus.md" data-raw-source="[&lt;strong&gt;JobStatus&lt;/strong&gt;](jobstatus.md)"><strong>JobStatus</strong></a></p></td>
</tr>
<tr class="odd">
<td><p><a href="scanticket.md" data-raw-source="[&lt;strong&gt;ScanTicket&lt;/strong&gt;](scanticket.md)"><strong>ScanTicket</strong></a></p></td>
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
</tbody>
</table>

<a name="remarks"></a>注釈
-------

スキャン ジョブ (この、**ジョブ**要素を表します) 1 つまたは複数のドキュメントを含めることができます。 両方の WSD スキャン サービスの処理手順については、ジョブとそのドキュメントで実行される、**ジョブ**レベル。

## <a name="see-also"></a>関連項目


[**ActiveJobs**](activejobs.md)

[**ドキュメント**](documents.md)

[**JobStatus**](jobstatus.md)

[**ScanTicket**](scanticket.md)

 

 







---
title: JobStateReasons 要素
description: 必要な JobStateReasons 要素には、ジョブが現在の状態の理由に関するすべての追加情報が含まれています。
ms.assetid: 52d6519e-2392-4fa4-bac0-f1bf60eccc99
keywords:
- JobStateReasons 要素イメージング デバイス
topic_type:
- apiref
api_name:
- wscn JobStateReasons
api_type:
- Schema
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9b469b2b198fa6cc45a62f7a2a41f1072985a794
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63363060"
---
# <a name="jobstatereasons-element"></a>JobStateReasons 要素


必要な**JobStateReasons**要素には、ジョブが現在の状態の理由に関するすべての追加情報が含まれています。

<a name="usage"></a>使用方法
-----

```xml
<wscn:JobStateReasons>
  child elements
</wscn:JobStateReasons>
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
<td><p><a href="jobstatus.md" data-raw-source="[&lt;strong&gt;JobStatus&lt;/strong&gt;](jobstatus.md)"><strong>JobStatus</strong></a></p></td>
</tr>
<tr class="even">
<td><p><a href="jobsummary.md" data-raw-source="[&lt;strong&gt;JobSummary&lt;/strong&gt;](jobsummary.md)"><strong>JobSummary</strong></a></p></td>
</tr>
</tbody>
</table>

<a name="remarks"></a>注釈
-------

**JobStateReasons**要素の一覧を含む[ **JobStateReason** ](jobstatereason.md)要素は、それぞれのジョブが現在の状態である理由の 1 つを指定します。

## <a name="see-also"></a>関連項目


[**JobStateReason**](jobstatereason.md)

[**JobStatus**](jobstatus.md)

[**JobSummary**](jobsummary.md)

 

 







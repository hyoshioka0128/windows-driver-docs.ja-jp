---
title: JobTable 要素
description: 必要な JobTable 要素には、スキャン ジョブに関する現在および過去の情報が含まれています。
ms.assetid: 349ca443-5296-4200-884d-91fcdb222be4
keywords:
- JobTable 要素イメージング デバイス
topic_type:
- apiref
api_name:
- wscn JobTable
api_type:
- Schema
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0464a2aab8fed830f5fb0fc65efc987274b729bf
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63373910"
---
# <a name="jobtable-element"></a>JobTable 要素


必要な**JobTable**要素には、スキャン ジョブに関する現在および過去の情報が含まれています。

<a name="usage"></a>使用方法
-----

```xml
<wscn:JobTable>
  child elements
</wscn:JobTable>
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
<td><p><a href="activejobs.md" data-raw-source="[&lt;strong&gt;ActiveJobs&lt;/strong&gt;](activejobs.md)"><strong>ActiveJobs</strong></a></p></td>
</tr>
<tr class="even">
<td><p><a href="jobhistory2.md" data-raw-source="[&lt;strong&gt;JobHistory&lt;/strong&gt;](jobhistory2.md)"><strong>JobHistory</strong></a></p></td>
</tr>
</tbody>
</table>

## <a name="parent-elements"></a>親要素


親要素はありません。

<a name="remarks"></a>注釈
-------

WSD スキャン サービスを使用して、 **JobTable** WSD スキャン サービスに送信されるすべてのスキャンの現在と完了したジョブを追跡する要素。 追跡されます現在のジョブ、 [ **ActiveJobs** ](activejobs.md)の子要素で完了したジョブが追跡されます必要に応じて、 [ **JobHistory** ](jobhistory2.md)子。要素。

## <a name="see-also"></a>関連項目


[**ActiveJobs**](activejobs.md)

[**JobHistory**](jobhistory2.md)

 

 







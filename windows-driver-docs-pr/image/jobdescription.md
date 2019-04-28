---
title: JobDescription 要素
description: 必要な JobDescription 要素には、識別された現在のジョブについて基本的な作成にはが含まれています。
ms.assetid: 78b77a9b-2fe9-4261-996b-970e97c4c0a9
keywords:
- JobDescription 要素イメージング デバイス
topic_type:
- apiref
api_name:
- wscn JobDescription
api_type:
- Schema
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: e7acf05250ae0afebce5d3fbc54e486079b74b31
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63363354"
---
# <a name="jobdescription-element"></a>JobDescription 要素


必要な**JobDescription**要素には、識別された現在のジョブの基本的な作成情報が含まれています。

<a name="usage"></a>使用方法
-----

```xml
<wscn:JobDescription>
  child elements
</wscn:JobDescription>
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
<td><p><a href="jobinformation.md" data-raw-source="[&lt;strong&gt;JobInformation&lt;/strong&gt;](jobinformation.md)"><strong>JobInformation</strong></a></p></td>
</tr>
<tr class="even">
<td><p><a href="jobname.md" data-raw-source="[&lt;strong&gt;JobName&lt;/strong&gt;](jobname.md)"><strong>JobName</strong></a></p></td>
</tr>
<tr class="odd">
<td><p><a href="joboriginatingusername.md" data-raw-source="[&lt;strong&gt;JobOriginatingUserName&lt;/strong&gt;](joboriginatingusername.md)"><strong>JobOriginatingUserName</strong></a></p></td>
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
<td><p><a href="defaultscanticket.md" data-raw-source="[&lt;strong&gt;DefaultScanTicket&lt;/strong&gt;](defaultscanticket.md)"><strong>DefaultScanTicket</strong></a></p></td>
</tr>
<tr class="even">
<td><p><a href="scanticket.md" data-raw-source="[&lt;strong&gt;ScanTicket&lt;/strong&gt;](scanticket.md)"><strong>ScanTicket</strong></a></p></td>
</tr>
</tbody>
</table>

<a name="remarks"></a>注釈
-------

クライアントは、すべての値を設定**JobDescription**子要素に送信して、 [ **CreateScanJobRequest** ](createscanjobrequest.md)操作。

## <a name="see-also"></a>関連項目


[**CreateScanJobRequest**](createscanjobrequest.md)

[**DefaultScanTicket**](defaultscanticket.md)

[**JobInformation**](jobinformation.md)

[**JobName**](jobname.md)

[**JobOriginatingUserName**](joboriginatingusername.md)

[**ScanTicket**](scanticket.md)

 

 







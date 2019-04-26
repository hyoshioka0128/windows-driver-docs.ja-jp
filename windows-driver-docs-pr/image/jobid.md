---
title: JobId 要素
description: 必要な JobId 要素は、スキャナー内でのジョブを一意に識別します。
ms.assetid: ae9199c1-c45a-4147-b4f0-f37a9a0f1b22
keywords:
- JobId 要素イメージング デバイス
topic_type:
- apiref
api_name:
- wscn JobId
api_type:
- Schema
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: c69e5f27152036cf8d1a220205228b9d37802d91
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63348821"
---
# <a name="jobid-element"></a>JobId 要素


必要な**JobId**要素は、スキャナー内でのジョブを一意に識別します。

<a name="usage"></a>使用方法
-----

```xml
<wscn:JobId>
  text
</wscn:JobId>
```

<a name="attributes"></a>属性
----------

属性はありません。

<a name="text-value"></a>テキスト値
----------

必須。 1 ~ 2147483648 の整数値。

## <a name="child-elements"></a>子要素


子要素はありません。

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
<td><p><a href="canceljobrequest.md" data-raw-source="[&lt;strong&gt;CancelJobRequest&lt;/strong&gt;](canceljobrequest.md)"><strong>CancelJobRequest</strong></a></p></td>
</tr>
<tr class="even">
<td><p><a href="createscanjobresponse.md" data-raw-source="[&lt;strong&gt;CreateScanJobResponse&lt;/strong&gt;](createscanjobresponse.md)"><strong>CreateScanJobResponse</strong></a></p></td>
</tr>
<tr class="odd">
<td><p><a href="getjobelementsrequest.md" data-raw-source="[&lt;strong&gt;GetJobElementsRequest&lt;/strong&gt;](getjobelementsrequest.md)"><strong>GetJobElementsRequest</strong></a></p></td>
</tr>
<tr class="even">
<td><p><a href="jobendstate.md" data-raw-source="[&lt;strong&gt;JobEndState&lt;/strong&gt;](jobendstate.md)"><strong>JobEndState</strong></a></p></td>
</tr>
<tr class="odd">
<td><p><a href="jobstatus.md" data-raw-source="[&lt;strong&gt;JobStatus&lt;/strong&gt;](jobstatus.md)"><strong>JobStatus</strong></a></p></td>
</tr>
<tr class="even">
<td><p><a href="jobsummary.md" data-raw-source="[&lt;strong&gt;JobSummary&lt;/strong&gt;](jobsummary.md)"><strong>JobSummary</strong></a></p></td>
</tr>
<tr class="odd">
<td><p><a href="retrieveimagerequest.md" data-raw-source="[&lt;strong&gt;RetrieveImageRequest&lt;/strong&gt;](retrieveimagerequest.md)"><strong>RetrieveImageRequest</strong></a></p></td>
</tr>
</tbody>
</table>

<a name="remarks"></a>注釈
-------

スキャン サービスは WSD を**JobId**要素を使用して、クライアントを[ **CreateScanJobResponse** ](createscanjobresponse.md)操作の要素。 クライアントを使用して、返された**JobId**を通してスキャン要求を開始するときに、 [ **RetrieveImageRequest** ](retrieveimagerequest.md)操作の要素。

**JobId**全体で一意にする必要はありません。 WSD スキャン サービスには、クライアントが以前のジョブに現在のスキャン ジョブと混同しないように、最近割り当てられた値が再利用しない必要があります。

許可される値を拡張することはできません、 **JobId**要素。

## <a name="see-also"></a>関連項目


[**CancelJobRequest**](canceljobrequest.md)

[**CreateScanJobResponse**](createscanjobresponse.md)

[**GetJobElementsRequest**](getjobelementsrequest.md)

[**JobEndState**](jobendstate.md)

[**JobStatus**](jobstatus.md)

[**JobSummary**](jobsummary.md)

[**RetrieveImageRequest**](retrieveimagerequest.md)

 

 







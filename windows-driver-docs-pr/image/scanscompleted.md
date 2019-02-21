---
title: ScansCompleted 要素
description: 必要な ScansCompleted 要素は、スキャンされるイメージの数を指定します。
ms.assetid: 71634b6b-1c61-46a0-8cde-01a975c09270
keywords:
- ScansCompleted 要素イメージング デバイス
topic_type:
- apiref
api_name:
- wscn ScansCompleted
api_type:
- Schema
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 81013fd6a543b9bfbccb98665afadb346d9cdb18
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56538510"
---
# <a name="scanscompleted-element"></a>ScansCompleted 要素


必要な**ScansCompleted**要素は、スキャンされるイメージの数を指定します。

<a name="usage"></a>使用方法
-----

```xml
<wscn:ScansCompleted>
  text
</wscn:ScansCompleted>
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
<td><p><a href="jobendstate.md" data-raw-source="[&lt;strong&gt;JobEndState&lt;/strong&gt;](jobendstate.md)"><strong>JobEndState</strong></a></p></td>
</tr>
<tr class="even">
<td><p><a href="jobstatus.md" data-raw-source="[&lt;strong&gt;JobStatus&lt;/strong&gt;](jobstatus.md)"><strong>JobStatus</strong></a></p></td>
</tr>
<tr class="odd">
<td><p><a href="jobsummary.md" data-raw-source="[&lt;strong&gt;JobSummary&lt;/strong&gt;](jobsummary.md)"><strong>JobSummary</strong></a></p></td>
</tr>
</tbody>
</table>

<a name="remarks"></a>注釈
-------

メディアのシートには、複数回がスキャンされ場合、WSD スキャン サービスをインクリメントする必要があります、 **ScansCompleted**たびにカウントします。 2 つのスキャンを生成する、二重モードでメディアのシートの各側がスキャン、 **ScansCompleted**数。

**ScansCompleted**スキャナーのジョブの処理が完了するまで、カウントを認識しない場合があります。 WSD スキャン サービスを更新する必要があります、 **ScansCompleted**要素の詳細情報が正確な場合に使用できます。

## <a name="see-also"></a>関連項目


[**JobEndState**](jobendstate.md)

[**JobStatus**](jobstatus.md)

[**JobSummary**](jobsummary.md)

 

 







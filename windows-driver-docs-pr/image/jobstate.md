---
title: JobState 要素
description: 必須の JobState 要素には、ジョブの現在の状態を指定します。
ms.assetid: 7198feea-ce6c-4827-a3b4-c248c6f62e37
keywords:
- デバイスのイメージングの JobState 要素
topic_type:
- apiref
api_name:
- wscn JobState
api_type:
- Schema
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0e3b0ffa831de96553bfd3067c1edb65a71f5b1f
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56532467"
---
# <a name="jobstate-element"></a>JobState 要素


必要な**JobState**要素は、ジョブの現在の状態を指定します。

<a name="usage"></a>使用方法
-----

```xml
<wscn:JobState>
  text
</wscn:JobState>
```

<a name="attributes"></a>属性
----------

属性はありません。

<a name="text-value"></a>テキスト値
----------

必須。 次のいずれかの値です。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>用語</th>
<th>説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><span id="Aborted"></span><span id="aborted"></span><span id="ABORTED"></span>中止されました</p></td>
<td><p>システムでは、ジョブが中止されました。</p></td>
</tr>
<tr class="even">
<td><p><span id="Canceled"></span><span id="canceled"></span><span id="CANCELED"></span>取り消されました</p></td>
<td><p>CancelJobRequest 操作を使用しているクライアントまたは WSD スキャン サービスの範囲外の方法で、ジョブが取り消されました。</p></td>
</tr>
<tr class="odd">
<td><p><span id="Completed"></span><span id="completed"></span><span id="COMPLETED"></span>完了しました</p></td>
<td><p>ジョブは、処理が完了しましたとすべてのデータがクライアントに送信されたイメージです。</p></td>
</tr>
<tr class="even">
<td><p><span id="Creating"></span><span id="creating"></span><span id="CREATING"></span>作成します。</p></td>
<td><p>ジョブを初期化しています。</p></td>
</tr>
<tr class="odd">
<td><p><span id="Held"></span><span id="held"></span><span id="HELD"></span>保持されています。</p></td>
<td><p>ジョブは、処理を待機していますが、スケジュールに使用ではありません。 ジョブは、この状態を WSD スキャン サービスのスコープ外のメソッドによってのみアクセスできます。</p></td>
</tr>
<tr class="even">
<td><p><span id="Pending"></span><span id="pending"></span><span id="PENDING"></span>保留中</p></td>
<td><p>ジョブが初期化されて、処理を待機しています。</p></td>
</tr>
<tr class="odd">
<td><p><span id="Processing"></span><span id="processing"></span><span id="PROCESSING"></span>処理</p></td>
<td><p>ジョブ データがデジタル化中、変換された、または転送します。</p></td>
</tr>
<tr class="even">
<td><p><span id="Started"></span><span id="started"></span><span id="STARTED"></span>開始</p></td>
<td><p>デバイスのスキャンでは、ジョブの処理が開始します。 この状態は、一時的な状態し、通常 JobStatusEvent イベントでのみ表示されます。</p></td>
</tr>
<tr class="odd">
<td><p><span id="Terminating"></span><span id="terminating"></span><span id="TERMINATING"></span>終了しています</p></td>
<td><p>ジョブがいずれかをクライアントが開始した CancelJobRequest 操作によって取り消されましたか WSD スキャン サービスの範囲外の方法で中止されました。</p></td>
</tr>
</tbody>
</table>

 

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
<td><p><a href="jobstatus.md" data-raw-source="[&lt;strong&gt;JobStatus&lt;/strong&gt;](jobstatus.md)"><strong>JobStatus</strong></a></p></td>
</tr>
<tr class="even">
<td><p><a href="jobsummary.md" data-raw-source="[&lt;strong&gt;JobSummary&lt;/strong&gt;](jobsummary.md)"><strong>JobSummary</strong></a></p></td>
</tr>
</tbody>
</table>

<a name="remarks"></a>注釈
-------

ときに、 **JobState**に要素が含まれる、 [ **JobEndStateEvent** ](jobendstateevent.md)イベントまたは[ **JobHistory** ](jobhistory2.md)要素、 **JobState**ジョブの完了の状態を表します。 それ以外の場合、 **JobState**ジョブの現在の状態を指定します。

両方を拡張して一部この要素に使用できる値。

## <a name="see-also"></a>関連項目


[**CancelJobRequest**](canceljobrequest.md)

[**JobEndStateEvent**](jobendstateevent.md)

[**JobHistory**](jobhistory2.md)

[**JobStatus**](jobstatus.md)

[**JobStatusEvent**](jobstatusevent.md)

[**JobSummary**](jobsummary.md)

 

 







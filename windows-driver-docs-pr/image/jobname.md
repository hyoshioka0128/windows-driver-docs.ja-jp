---
title: JobName 要素
description: 必要な JobName 要素には、スキャン ジョブのクライアントが提供するわかりやすい名前を指定します。
ms.assetid: b6d2baba-6a2e-4971-880b-9a4df66dc1ae
keywords:
- JobName 要素イメージング デバイス
topic_type:
- apiref
api_name:
- wscn JobName
api_type:
- Schema
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0160e44812155cac4ac16a1ef4f3c2b97f8775a3
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56530782"
---
# <a name="jobname-element"></a>JobName 要素


必要な**JobName**要素は、スキャン ジョブのクライアントが提供するわかりやすい名前を指定します。

<a name="usage"></a>使用方法
-----

```xml
<wscn:JobName>
  text
</wscn:JobName>
```

<a name="attributes"></a>属性
----------

属性はありません。

<a name="text-value"></a>テキスト値
----------

必須。 任意の有効な文字の文字列。

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
<td><p><a href="jobdescription.md" data-raw-source="[&lt;strong&gt;JobDescription&lt;/strong&gt;](jobdescription.md)"><strong>JobDescription</strong></a></p></td>
</tr>
<tr class="even">
<td><p><a href="jobendstate.md" data-raw-source="[&lt;strong&gt;JobEndState&lt;/strong&gt;](jobendstate.md)"><strong>JobEndState</strong></a></p></td>
</tr>
<tr class="odd">
<td><p><a href="jobsummary.md" data-raw-source="[&lt;strong&gt;JobSummary&lt;/strong&gt;](jobsummary.md)"><strong>JobSummary</strong></a></p></td>
</tr>
</tbody>
</table>

<a name="remarks"></a>注釈
-------

クライアントは、自分が送信したジョブを簡単に区別するユーザーを支援する値を指定する必要があります。

WSD スキャン サービスは、既定値を提供できます**JobName**内の名前、 [ **DefaultScanTicket** ](defaultscanticket.md)要素。 この名前は、実装に固有の方法で設定できます。

ジョブを送信したユーザーの名前が指定された、 [ **JobOriginatingUserName** ](joboriginatingusername.md)要素。

## <a name="see-also"></a>関連項目


[**DefaultScanTicket**](defaultscanticket.md)

[**JobDescription**](jobdescription.md)

[**JobEndState**](jobendstate.md)

[**JobOriginatingUserName**](joboriginatingusername.md)

[**JobSummary**](jobsummary.md)

 

 







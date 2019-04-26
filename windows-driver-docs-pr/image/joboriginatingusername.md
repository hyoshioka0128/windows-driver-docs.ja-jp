---
title: JobOriginatingUserName 要素
description: 必要な JobOriginatingUserName 要素には、スキャン ジョブを送信したユーザーの名前を指定します。
ms.assetid: ba2dd472-1ac0-40bd-816c-02abc093b6ed
keywords:
- JobOriginatingUserName 要素イメージング デバイス
topic_type:
- apiref
api_name:
- wscn JobOriginatingUserName
api_type:
- Schema
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: a0158fdb766871484a1d408d28460340b71c8a1a
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63348794"
---
# <a name="joboriginatingusername-element"></a>JobOriginatingUserName 要素


必要な**JobOriginatingUserName**要素は、スキャン ジョブを送信したユーザーの名前を指定します。

<a name="usage"></a>使用方法
-----

```xml
<wscn:JobOriginatingUserName>
  text
</wscn:JobOriginatingUserName>
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

存在する場合は、クライアントや、セキュリティ インフラストラクチャ、 **JobOriginatingUserName**要素。 クライアントは、ユーザーが、自分が送信したジョブと他のユーザーが送信されたジョブを簡単に区別する値を指定する必要があります。

WSD スキャン サービスは、既定値を提供できます**JobOriginatingUserName**内の名前、 [ **DefaultScanTicket** ](defaultscanticket.md)要素。 この名前は、実装に固有の方法で設定できます。

ジョブの名前が指定された、 [ **JobName** ](jobname.md)要素。

## <a name="see-also"></a>関連項目


[**DefaultScanTicket**](defaultscanticket.md)

[**JobDescription**](jobdescription.md)

[**JobEndState**](jobendstate.md)

[**JobName**](jobname.md)

[**JobSummary**](jobsummary.md)

 

 







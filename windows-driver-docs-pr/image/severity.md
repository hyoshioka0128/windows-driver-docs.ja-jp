---
title: 重大度要素
description: 必要な重要度の要素には、現在 DeviceCondition または ConditionHistoryEntry 要素の重大度レベルを指定します。
ms.assetid: 51c08a50-0c2b-40d9-883e-32460c2024ad
keywords:
- 重大度要素イメージング デバイス
topic_type:
- apiref
api_name:
- wscn Severity
api_type:
- Schema
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 151f43ce4cd552d1bed5d31a49fd29700d79451c
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56536414"
---
# <a name="severity-element"></a>重大度要素


必要な**重大度**要素を現在の重大度レベルを指定します[ **DeviceCondition** ](devicecondition.md)または[ **ConditionHistoryEntry** ](conditionhistoryentry.md)要素。

<a name="usage"></a>使用方法
-----

```xml
<wscn:Severity>
  text
</wscn:Severity>
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
<td><p><span id="Informational"></span><span id="informational"></span><span id="INFORMATIONAL"></span>情報</p></td>
<td><p>この状態は、純粋なユーザー情報は、イメージの取得プロセスで顕著な影響を与えません。</p></td>
</tr>
<tr class="even">
<td><p><span id="Warning"></span><span id="warning"></span><span id="WARNING"></span>警告</p></td>
<td><p>この条件は、処理に現在影響していませんが、条件になる状況が出席しない場合は、"重大"です。</p></td>
</tr>
<tr class="odd">
<td><p><span id="Critical"></span><span id="critical"></span><span id="CRITICAL"></span>重要です</p></td>
<td><p>デバイスは、この条件が解決されるまでの処理を続行できません。</p></td>
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
<td><p><a href="conditionhistoryentry.md" data-raw-source="[&lt;strong&gt;ConditionHistoryEntry&lt;/strong&gt;](conditionhistoryentry.md)"><strong>ConditionHistoryEntry</strong></a></p></td>
</tr>
<tr class="even">
<td><p><a href="devicecondition.md" data-raw-source="[&lt;strong&gt;DeviceCondition&lt;/strong&gt;](devicecondition.md)"><strong>DeviceCondition</strong></a></p></td>
</tr>
</tbody>
</table>

<a name="remarks"></a>注釈
-------

WSD スキャン サービスによって決定、**重大度**各エラー条件に割り当てられているレベル。

両方を拡張して一部この要素に使用できる値。

## <a name="see-also"></a>関連項目


[**ConditionHistoryEntry**](conditionhistoryentry.md)

[**DeviceCondition**](devicecondition.md)

 

 







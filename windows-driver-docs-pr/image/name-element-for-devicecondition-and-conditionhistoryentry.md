---
title: DeviceCondition と ConditionHistoryEntry 要素の name 要素
description: 必須の Name 要素の名前、DeviceCondition または ConditionHistoryEntry 要素で指定されている現在のエラー条件。
ms.assetid: 1ac530ed-dc31-4af0-a89b-0860a36bbfeb
keywords:
- デバイスのイメージング DeviceCondition ConditionHistoryEntry 要素の name 要素
topic_type:
- apiref
api_name:
- wscn Name
api_type:
- Schema
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 56b1a0f33954c40a54e4db398b3a98533d244316
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63379662"
---
# <a name="name-element-for-devicecondition-and-conditionhistoryentry-element"></a>DeviceCondition と ConditionHistoryEntry 要素の name 要素


必要な**名前**要素名で指定されている現在のエラー条件、 [ **DeviceCondition** ](devicecondition.md)または[ **ConditionHistoryEntry** ](conditionhistoryentry.md)要素。

<a name="usage"></a>使用方法
-----

```xml
<wscn:Name>
  text
</wscn:Name>
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
<td><p><span id="Calibrating"></span><span id="calibrating"></span><span id="CALIBRATING"></span>調整</p></td>
<td><p>デバイスのスキャンがその内部コンポーネントにイメージを取得するための準備を調整します。</p></td>
</tr>
<tr class="even">
<td><p><span id="CoverOpen"></span><span id="coveropen"></span><span id="COVEROPEN"></span>CoverOpen</p></td>
<td><p>デバイスのスキャンの詳細のカバーのいずれかの方法は、開いています。</p></td>
</tr>
<tr class="odd">
<td><p><span id="InputTrayEmpty"></span><span id="inputtrayempty"></span><span id="INPUTTRAYEMPTY"></span>InputTrayEmpty</p></td>
<td><p>自動ドキュメント フィーダー付き (ADF) の入力には、メディアがありません。</p></td>
</tr>
<tr class="even">
<td><p><span id="InterlockOpen"></span><span id="interlockopen"></span><span id="INTERLOCKOPEN"></span>InterlockOpen</p></td>
<td><p>ダブル インター ロック プリアクションは開いています。</p></td>
</tr>
<tr class="odd">
<td><p><span id="InternalStorageFull"></span><span id="internalstoragefull"></span><span id="INTERNALSTORAGEFULL"></span>InternalStorageFull</p></td>
<td><p>書き込まれた現在の内部記憶域コンポーネントがいっぱいです。</p></td>
</tr>
<tr class="even">
<td><p><span id="LampError"></span><span id="lamperror"></span><span id="LAMPERROR"></span>LampError</p></td>
<td><p>スキャナーのランプが失敗していると、イメージの取得を続行できません。</p></td>
</tr>
<tr class="odd">
<td><p><span id="LampWarming"></span><span id="lampwarming"></span><span id="LAMPWARMING"></span>LampWarming</p></td>
<td><p>スキャナーのランプはイメージを取得するための準備に準です。</p></td>
</tr>
<tr class="even">
<td><p><span id="MediaJam"></span><span id="mediajam"></span><span id="MEDIAJAM"></span>MediaJam</p></td>
<td><p>イメージの取得に失敗しましたので、入力のソースのいずれかでメディアが詰まります。</p></td>
</tr>
<tr class="odd">
<td><p><span id="MultipleFeedError"></span><span id="multiplefeederror"></span><span id="MULTIPLEFEEDERROR"></span>MultipleFeedError</p></td>
<td><p>ADF では、メディアの 1 つ以上の部分を同時に給紙でした。</p></td>
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

一部のエラー名が有効でのみ特定[**コンポーネント**](component.md)要素。

両方を拡張して一部この要素に使用できる値。

## <a name="see-also"></a>関連項目


[**コンポーネント**](component.md)

[**ConditionHistoryEntry**](conditionhistoryentry.md)

[**DeviceCondition**](devicecondition.md)

 

 







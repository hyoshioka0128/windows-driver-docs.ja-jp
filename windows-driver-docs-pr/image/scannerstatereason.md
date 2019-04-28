---
title: ScannerStateReason 要素
description: 省略可能な ScannerStateReason 要素には、スキャナーが現在の状態の理由についての情報の 1 つを指定します。
ms.assetid: 7f10476a-d3ef-40a1-a355-ab735a6afe60
keywords:
- ScannerStateReason 要素イメージング デバイス
topic_type:
- apiref
api_name:
- wscn ScannerStateReason
api_type:
- Schema
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: e5442865363ffa6dc9ab774d8fbf29e1d57a031a
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63370047"
---
# <a name="scannerstatereason-element"></a>ScannerStateReason 要素


省略可能な**ScannerStateReason**要素については、スキャナーが現在の状態の理由の 1 つを指定します。

<a name="usage"></a>使用方法
-----

```xml
<wscn:ScannerStateReason>
  text
</wscn:ScannerStateReason>
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
<td><p><span id="AttentionRequired"></span><span id="attentionrequired"></span><span id="ATTENTIONREQUIRED"></span>AttentionRequired</p></td>
<td><p>デバイスのスキャンでは、続行する前に、ユーザーの介入が必要です。</p></td>
</tr>
<tr class="even">
<td><p><span id="Calibrating"></span><span id="calibrating"></span><span id="CALIBRATING"></span>調整</p></td>
<td><p>デバイスのスキャンがその内部コンポーネントにイメージを取得するための準備を調整します。</p></td>
</tr>
<tr class="odd">
<td><p><span id="CoverOpen"></span><span id="coveropen"></span><span id="COVEROPEN"></span>CoverOpen</p></td>
<td><p>デバイスのスキャンの詳細のカバーのいずれかの方法は、開いています。</p></td>
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
<tr class="even">
<td><p><span id="None"></span><span id="none"></span><span id="NONE"></span>[なし]</p></td>
<td><p>現在の状態の理由はありません。</p></td>
</tr>
<tr class="odd">
<td><p><span id="Paused"></span><span id="paused"></span><span id="PAUSED"></span>一時停止</p></td>
<td><p>スキャナーが一時停止し、スキャナーの状態が停止します。 この状態で、スキャナーにスキャンされた出力は生成されません。</p></td>
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
<td><p><a href="scannerstatereasons.md" data-raw-source="[&lt;strong&gt;ScannerStateReasons&lt;/strong&gt;](scannerstatereasons.md)"><strong>ScannerStateReasons</strong></a></p></td>
</tr>
</tbody>
</table>

<a name="remarks"></a>注釈
-------

これらの理由の一部には、現在定義されている WSD スキャン サービス操作のセットに応じて、スキャナーに入れませんスキャナー状態について説明します。 スキャナーは、たとえば、 **Paused**があってもない"*PauseScanner*"操作。 その他のいくつかのプロトコルまたはコンソール アクションがその状態を入力するスキャナーがあるために、このような状態が存在します。

WSD スキャン サービスはその実装で検出する条件を表す値をサポートする必要があります。 そのため、WSD スキャン サービスでは、検出できる許可された値のサブセットのみをサポートできます。

許可の値を拡張できますが、クライアントでは、このリストを拡張する場合に影響があります。 クライアントは通常ローカライズ、 [ **ScannerStateReasons** ](scannerstatereasons.md)クライアントがベンダー拡張機能の値を認識しないため、エンドユーザーの言語に (その他の文字列変数の値) と同じ値です。 ただし、クライアントは、直接受信される値を表示できます。 この値は、エンドユーザーも、値を理解しないので、英語でなければなりません。 スキャン サービスが、一般的なを使用する代わりに、 **AttentionRequired**値し、スキャナーのコンソールでは、スキャナーでは、ユーザーに表示し、問題について説明します。

## <a name="see-also"></a>関連項目


[**ScannerStateReasons**](scannerstatereasons.md)

 

 







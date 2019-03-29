---
title: タイム トラベルの拡張機能のデバッグ
description: このセクションでは、タイム トラベル デバッガー拡張機能コマンドを使用する方法について説明します。
ms.date: 09/22/2017
ms.localizationpriority: medium
ms.openlocfilehash: e46b66c7beb256c32a62c49617d65d5a0fe09c5c
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56572535"
---
#  <a name="time-travel-debugging-extension-commands"></a>タイム トラベルの拡張機能コマンドのデバッグ

![クロックが表示された短い時間旅行ロゴ](images/ttd-time-travel-debugging-logo.png)

このセクションでは、時間の旅行デバッガー拡張機能コマンドについて説明します。


## <a name="span-idinthissectionspanin-this-section"></a><span id="in_this_section"></span>このセクションの内容


<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">トピック</th>
<th align="left">説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><a href="time-travel-debugging-extension-tt.md" data-raw-source="[&lt;strong&gt;!tt (time travel)&lt;/strong&gt;](time-travel-debugging-extension-tt.md)"><strong>! tt (タイム トラベル)</strong></a></p></td>
<td align="left"><p><a href="time-travel-debugging-extension-tt.md" data-raw-source="[&lt;strong&gt;!tt (time travel)&lt;/strong&gt;](time-travel-debugging-extension-tt.md)"> <strong>! Tt (タイム トラベル)</strong> </a>デバッガーの拡張機能を時間で前方と後方を移動することができます。</p></td>

</tr>
<tr class="even">
<td align="left"><p><a href="time-travel-debugging-extension-positions.md" data-raw-source="[&lt;strong&gt;!positions&lt;/strong&gt;](time-travel-debugging-extension-positions.md)"><strong>! 位置</strong></a></p></td>
<td align="left"><p><a href="time-travel-debugging-extension-positions.md" data-raw-source="[&lt;strong&gt;!positions&lt;/strong&gt;](time-travel-debugging-extension-positions.md)"> <strong>! 位置</strong></a>拡張機能がアクティブなすべてのスレッドをタイム トラベルのトレースで現在の位置を含むを表示します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="time-travel-debugging-extension-index.md" data-raw-source="[&lt;strong&gt;!index&lt;/strong&gt;](time-travel-debugging-extension-index.md)"><strong>! インデックス</strong></a></p></td>
<td align="left"><p><a href="time-travel-debugging-extension-index.md" data-raw-source="[&lt;strong&gt;!index&lt;/strong&gt;](time-travel-debugging-extension-index.md)"> <strong>! インデックス</strong></a>インデックス タイム トラベルの拡張機能は、トレースまたはインデックスの状態情報が表示されます。</p></td>
</tr>
</tbody>
</table>

### <a name="spanspan-idadditionalinformationspanadditional-information"></a></span><span id="ADDITIONAL_INFORMATION"></span>追加情報

この拡張機能のみの動作時間は、トレースを移動します。 タイム トラベルの詳細については、次を参照してください。[時出張デバッグ - 概要](time-travel-debugging-overview.md)します。

### <a name="dll"></a>DLL

時間は、コマンドが ttdext.dll で実装されているデバッガー拡張機能を移動します。 タイム トラベル コマンド dll は WinDbg のプレビューで自動的に読み込まれます。 コマンドを使用して、ロード、ttdext.dll を手動で読み込む必要はありません。
 
## <a name="see-also"></a>関連項目

[旅行時間 - デバッグの概要](time-travel-debugging-overview.md)

---







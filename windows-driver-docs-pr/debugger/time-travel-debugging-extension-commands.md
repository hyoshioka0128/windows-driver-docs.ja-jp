---
title: タイムトラベルデバッグ拡張機能
description: このセクションでは、タイムトラベルデバッガー拡張機能コマンドの使用方法について説明します。
ms.date: 09/22/2017
ms.localizationpriority: medium
ms.openlocfilehash: 838337a0fc9db255097d190ee383f6e0cc252c20
ms.sourcegitcommit: ee70846334ab6710ec0f9143e9f3a3754bc69f98
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/23/2020
ms.locfileid: "76706981"
---
# <a name="time-travel-debugging-extension-commands"></a>タイムトラベルデバッグ拡張コマンド

![時計を示す短いタイムトラベルロゴ](images/ttd-time-travel-debugging-logo.png)

このセクションでは、タイムトラベルデバッガー拡張機能のコマンドについて説明します。

## <a name="span-idin_this_sectionspanin-this-section"></a><span id="in_this_section"></span>このセクションの内容

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
<td align="left"><p><a href="time-travel-debugging-extension-tt.md" data-raw-source="[&lt;strong&gt;!tt (time travel)&lt;/strong&gt;](time-travel-debugging-extension-tt.md)"><strong>! tt (タイムトラベル)</strong></a></p></td>
<td align="left"><p>時間を前後に移動できるようにする、 <a href="time-travel-debugging-extension-tt.md" data-raw-source="[&lt;strong&gt;!tt (time travel)&lt;/strong&gt;](time-travel-debugging-extension-tt.md)"><strong>! tt (タイムトラベル)</strong></a>デバッガー拡張機能。</p></td>

</tr>
<tr class="even">
<td align="left"><p><a href="time-travel-debugging-extension-positions.md" data-raw-source="[&lt;strong&gt;!positions&lt;/strong&gt;](time-travel-debugging-extension-positions.md)"><strong>! 位置</strong></a></p></td>
<td align="left"><p><a href="time-travel-debugging-extension-positions.md" data-raw-source="[&lt;strong&gt;!positions&lt;/strong&gt;](time-travel-debugging-extension-positions.md)"><strong>! 位置</strong></a>拡張は、タイムトラベルトレースの現在の位置を含む、すべてのアクティブなスレッドを表示します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="time-travel-debugging-extension-index.md" data-raw-source="[&lt;strong&gt;!index&lt;/strong&gt;](time-travel-debugging-extension-index.md)"><strong>! インデックス</strong></a></p></td>
<td align="left"><p><a href="time-travel-debugging-extension-index.md" data-raw-source="[&lt;strong&gt;!index&lt;/strong&gt;](time-travel-debugging-extension-index.md)"><strong>! インデックス</strong></a>拡張インデックスは、タイムトラベルをトレースしたり、インデックスの状態情報を表示したりします。</p></td>
</tr>
</tbody>
</table>

### <a name="spanspan-idadditional_informationspanadditional-information"></a>追加<span id="ADDITIONAL_INFORMATION"></span>情報の </span>

この拡張機能は、タイムトラベルトレースでのみ機能します。 タイムトラベルの詳細については、「[タイムトラベルデバッグ-概要](time-travel-debugging-overview.md)」を参照してください。

### <a name="dll"></a>DLL

タイムトラベルデバッガー拡張機能のコマンドは、ttdext に実装されています。 タイムトラベルコマンド dll は、WinDbg プレビューで自動的に読み込まれます。 Load コマンドを使用して、手動で ttdext を読み込む必要はありません。
 
## <a name="see-also"></a>関連項目

[タイムトラベルのデバッグ-概要](time-travel-debugging-overview.md)

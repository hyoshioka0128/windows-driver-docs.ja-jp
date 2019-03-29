---
title: デバッグ用 WIA 関数
description: デバッグ用 WIA 関数
ms.assetid: 164eeab3-1e4a-46de-99db-28b8f63593a4
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 25de71792686b2927acc5253190bd144db5109d3
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56578315"
---
# <a name="wia-functions-for-debugging"></a>デバッグ用 WIA 関数





WIA ミニドライバーを開発している場合は、ログ トレースのメッセージ、警告メッセージ、およびエラー メッセージには、次の関数を使用できます。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>関数</th>
<th>説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff549627" data-raw-source="[&lt;strong&gt;wiauDbgDump&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff549627)"><strong>wiauDbgDump</strong></a></p></td>
<td><p>1 つまたは複数のデータ値を含むメッセージを記録します。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff549633" data-raw-source="[&lt;strong&gt;wiauDbgError&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff549633)"><strong>wiauDbgError</strong></a></p></td>
<td><p>エラー メッセージを記録します。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff549637" data-raw-source="[&lt;strong&gt;wiauDbgErrorHr&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff549637)"><strong>wiauDbgErrorHr</strong></a></p></td>
<td><p>HRESULT とエラー メッセージ文字列を含むメッセージを記録します。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff549643" data-raw-source="[&lt;strong&gt;wiauDbgFlags&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff549643)"><strong>wiauDbgFlags</strong></a></p></td>
<td><p>特定のデバッグ フラグが設定されているかどうかを判断します。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff549649" data-raw-source="[&lt;strong&gt;wiauDbgHelper&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff549649)"><strong>wiauDbgHelper</strong></a></p></td>
<td><p>メッセージを書式設定し、ログ ファイルやデバッガーに書き込みます。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff549653" data-raw-source="[&lt;strong&gt;wiauDbgHelper2&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff549653)"><strong>wiauDbgHelper2</strong></a></p></td>
<td><p>ログ ファイル、またはデバッガー、またはその両方にメッセージを書き込みます。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff549660" data-raw-source="[&lt;strong&gt;wiauDbgInit&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff549660)"><strong>wiauDbgInit</strong></a></p></td>
<td><p>WIA がデバッグを初期化します。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff549667" data-raw-source="[&lt;strong&gt;wiauDbgLegacyError&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff549667)"><strong>wiauDbgLegacyError</strong></a></p></td>
<td><p>エラー メッセージを記録します。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff549671" data-raw-source="[&lt;strong&gt;wiauDbgLegacyError2&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff549671)"><strong>wiauDbgLegacyError2</strong></a></p></td>
<td><p>エラー メッセージを記録します。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff549675" data-raw-source="[&lt;strong&gt;wiauDbgLegacyHresult2&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff549675)"><strong>wiauDbgLegacyHresult2</strong></a></p></td>
<td><p>HRESULT を格納している既定のメッセージを記録します。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff550150" data-raw-source="[&lt;strong&gt;wiauDbgLegacyTrace&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff550150)"><strong>wiauDbgLegacyTrace</strong></a></p></td>
<td><p>トレース メッセージを記録します。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff550152" data-raw-source="[&lt;strong&gt;wiauDbgLegacyTrace2&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff550152)"><strong>wiauDbgLegacyTrace2</strong></a></p></td>
<td><p>トレース メッセージを記録します。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff550156" data-raw-source="[&lt;strong&gt;wiauDbgLegacyWarning&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff550156)"><strong>wiauDbgLegacyWarning</strong></a></p></td>
<td><p>警告メッセージを記録します。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff550159" data-raw-source="[&lt;strong&gt;wiauDbgSetFlags&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff550159)"><strong>wiauDbgSetFlags</strong></a></p></td>
<td><p>デバッグ フラグを設定します。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff550161" data-raw-source="[&lt;strong&gt;wiauDbgTrace&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff550161)"><strong>wiauDbgTrace</strong></a></p></td>
<td><p>トレース メッセージを記録します。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff550163" data-raw-source="[&lt;strong&gt;wiauDbgWarning&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff550163)"><strong>wiauDbgWarning</strong></a></p></td>
<td><p>警告メッセージを記録します。</p></td>
</tr>
</tbody>
</table>

 

 

 





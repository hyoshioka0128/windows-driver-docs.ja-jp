---
title: デバッグ用 WIA 関数
description: デバッグ用 WIA 関数
ms.assetid: 164eeab3-1e4a-46de-99db-28b8f63593a4
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: cc27ec5636d5acdde4ce84e2ad66581afa88adc7
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72840694"
---
# <a name="wia-functions-for-debugging"></a>デバッグ用 WIA 関数





次の関数を使用すると、WIA ミニドライバーを開発するときに、トレースメッセージ、警告メッセージ、およびエラーメッセージをログに記録できます。

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
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wiautil/nf-wiautil-wiaudbgdump" data-raw-source="[&lt;strong&gt;wiauDbgDump&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiautil/nf-wiautil-wiaudbgdump)"><strong>Wi/Dbgダンプ</strong></a></p></td>
<td><p>1つ以上のデータ値を含むメッセージをログに記録します。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wiautil/nf-wiautil-wiaudbgerror" data-raw-source="[&lt;strong&gt;wiauDbgError&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiautil/nf-wiautil-wiaudbgerror)"><strong>Wi/Dbgerror</strong></a></p></td>
<td><p>エラーメッセージを記録します。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wiautil/nf-wiautil-wiaudbgerrorhr" data-raw-source="[&lt;strong&gt;wiauDbgErrorHr&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiautil/nf-wiautil-wiaudbgerrorhr)"><strong>Wi/Dbgerrorhr</strong></a></p></td>
<td><p>HRESULT とそのエラーメッセージ文字列を含むメッセージをログに記録します。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wiautil/nf-wiautil-wiaudbgflags" data-raw-source="[&lt;strong&gt;wiauDbgFlags&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiautil/nf-wiautil-wiaudbgflags)"><strong>Wi/Dbgflags</strong></a></p></td>
<td><p>特定のデバッグフラグが設定されているかどうかを判断します。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wiautil/nf-wiautil-wiaudbghelper" data-raw-source="[&lt;strong&gt;wiauDbgHelper&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiautil/nf-wiautil-wiaudbghelper)"><strong>Wi/Dbghelper</strong></a></p></td>
<td><p>メッセージをフォーマットし、ログファイルまたはデバッガーに書き込みます。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wiautil/nf-wiautil-wiaudbghelper2" data-raw-source="[&lt;strong&gt;wiauDbgHelper2&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiautil/nf-wiautil-wiaudbghelper2)"><strong>wiauDbgHelper2</strong></a></p></td>
<td><p>ログファイル、デバッガー、またはその両方にメッセージを書き込みます。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wiautil/nf-wiautil-wiaudbginit" data-raw-source="[&lt;strong&gt;wiauDbgInit&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiautil/nf-wiautil-wiaudbginit)"><strong>Wi/Dbginit</strong></a></p></td>
<td><p>WIA デバッグを初期化します。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wiautil/nf-wiautil-wiaudbglegacyerror" data-raw-source="[&lt;strong&gt;wiauDbgLegacyError&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiautil/nf-wiautil-wiaudbglegacyerror)"><strong>wiauDbgLegacyError</strong></a></p></td>
<td><p>エラーメッセージを記録します。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wiautil/nf-wiautil-wiaudbglegacyerror2" data-raw-source="[&lt;strong&gt;wiauDbgLegacyError2&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiautil/nf-wiautil-wiaudbglegacyerror2)"><strong>wiauDbgLegacyError2</strong></a></p></td>
<td><p>エラーメッセージを記録します。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wiautil/nf-wiautil-wiaudbglegacyhresult2" data-raw-source="[&lt;strong&gt;wiauDbgLegacyHresult2&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiautil/nf-wiautil-wiaudbglegacyhresult2)"><strong>wiauDbgLegacyHresult2</strong></a></p></td>
<td><p>HRESULT を含む既定のメッセージをログに記録します。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wiautil/nf-wiautil-wiaudbglegacytrace" data-raw-source="[&lt;strong&gt;wiauDbgLegacyTrace&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiautil/nf-wiautil-wiaudbglegacytrace)"><strong>wiauDbgLegacyTrace</strong></a></p></td>
<td><p>トレースメッセージをログに記録します。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wiautil/nf-wiautil-wiaudbglegacytrace2" data-raw-source="[&lt;strong&gt;wiauDbgLegacyTrace2&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiautil/nf-wiautil-wiaudbglegacytrace2)"><strong>wiauDbgLegacyTrace2</strong></a></p></td>
<td><p>トレースメッセージをログに記録します。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wiautil/nf-wiautil-wiaudbglegacywarning" data-raw-source="[&lt;strong&gt;wiauDbgLegacyWarning&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiautil/nf-wiautil-wiaudbglegacywarning)"><strong>wiauDbgLegacyWarning</strong></a></p></td>
<td><p>警告メッセージを記録します。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wiautil/nf-wiautil-wiaudbgsetflags" data-raw-source="[&lt;strong&gt;wiauDbgSetFlags&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiautil/nf-wiautil-wiaudbgsetflags)"><strong>Wi/Dbgsetflags</strong></a></p></td>
<td><p>デバッグフラグを設定します。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wiautil/nf-wiautil-wiaudbgtrace" data-raw-source="[&lt;strong&gt;wiauDbgTrace&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiautil/nf-wiautil-wiaudbgtrace)"><strong>Wi/Dbgtrace</strong></a></p></td>
<td><p>トレースメッセージをログに記録します。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wiautil/nf-wiautil-wiaudbgwarning" data-raw-source="[&lt;strong&gt;wiauDbgWarning&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiautil/nf-wiautil-wiaudbgwarning)"><strong>Wi/Dbgwarning</strong></a></p></td>
<td><p>警告メッセージを記録します。</p></td>
</tr>
</tbody>
</table>

 

 

 





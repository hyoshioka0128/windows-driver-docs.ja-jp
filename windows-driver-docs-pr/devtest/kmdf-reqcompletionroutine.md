---
title: ReqCompletionRoutine ルール (kmdf)
description: ReqCompletionRoutine ルールでは、要求が I/O のターゲットに送信される前に完了ルーチンを設定する必要がありますを指定します。
ms.assetid: 0ddf6980-0540-4224-9800-3cd534f03230
ms.date: 05/21/2018
keywords:
- ReqCompletionRoutine ルール (kmdf)
topic_type:
- apiref
api_name:
- ReqCompletionRoutine
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: d4b4a897ad6a9b90cf1ee010372c6c928ceabd71
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56537700"
---
# <a name="reqcompletionroutine-rule-kmdf"></a>ReqCompletionRoutine ルール (kmdf)


**ReqCompletionRoutine**ルールでは、要求が I/O のターゲットに送信される前に完了ルーチンを設定する必要がありますを指定します。

場合は、要求が同期的には送信されませんまたは送信ポート、忘れるは送信されません (で指定された、 **WDF\_要求\_送信\_オプション\_送信\_AND\_破棄**フラグ)、I/O ターゲットが、要求が完了したときに、ドライバーを通知するために、ドライバーが完了ルーチンを設定する必要があります。

|              |      |
|--------------|------|
| ドライバー モデル | KMDF |

<a name="how-to-test"></a>テスト方法
-----------

<table>
<colgroup>
<col width="100%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">コンパイル時</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>実行<a href="https://msdn.microsoft.com/library/windows/hardware/ff552808" data-raw-source="[Static Driver Verifier](https://msdn.microsoft.com/library/windows/hardware/ff552808)">Static Driver Verifier</a>を指定し、 <strong>ReqCompletionRoutine</strong>ルール。</p>
コードの分析を実行するには、次の手順に従います。
<ol>
<li><a href="https://msdn.microsoft.com/library/windows/hardware/hh454281#preparing-your-source-code" data-raw-source="[Prepare your code (use role type declarations).](https://msdn.microsoft.com/library/windows/hardware/hh454281#preparing-your-source-code)">(ロールの型宣言の使用)、コードを準備します。</a></li>
<li><a href="https://msdn.microsoft.com/library/windows/hardware/hh454281#running-static-driver-verifier" data-raw-source="[Run Static Driver Verifier.](https://msdn.microsoft.com/library/windows/hardware/hh454281#running-static-driver-verifier)">Static Driver Verifier を実行します。</a></li>
<li><a href="https://msdn.microsoft.com/library/windows/hardware/hh454281#viewing-and-analyzing-the-results" data-raw-source="[View and analyze the results.](https://msdn.microsoft.com/library/windows/hardware/hh454281#viewing-and-analyzing-the-results)">表示し、結果を分析します。</a></li>
</ol>
<p>詳細については、<a href="https://msdn.microsoft.com/library/windows/hardware/hh454281" data-raw-source="[Using Static Driver Verifier to Find Defects in Drivers](https://msdn.microsoft.com/library/windows/hardware/hh454281)">ドライバーで障害を検出する Static Driver Verifier を使用して</a>を参照してください。</p></td>
</tr>
</tbody>
</table>

<a name="applies-to"></a>適用対象
----------

[**WdfRequestSend**](https://msdn.microsoft.com/library/windows/hardware/ff550027)
[**WdfRequestSetCompletionRoutine** ](https://msdn.microsoft.com/library/windows/hardware/ff550030)も参照してください
--------

[I/O 要求の完了](https://msdn.microsoft.com/library/windows/hardware/ff540740)
[キャンセルおよび終了コードを同期する](https://msdn.microsoft.com/library/windows/hardware/ff544726)
[**WDF\_要求\_送信\_オプション\_フラグ**](https://msdn.microsoft.com/library/windows/hardware/ff552493)
[**WDF\_要求\_送信\_オプション**](https://msdn.microsoft.com/library/windows/hardware/ff552491)
 

 






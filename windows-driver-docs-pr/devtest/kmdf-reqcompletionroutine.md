---
title: ReqCompletionRoutine ルール (kmdf)
description: ReqCompletionRoutine 規則は、要求が i/o ターゲットに送信される前に完了ルーチンを設定する必要があることを指定します。
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
ms.openlocfilehash: f399895f87bd345e0bd24d2d923e2177f7d7fed3
ms.sourcegitcommit: 82a9be3b3584f991e5121f8f46a972e04185fa52
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/02/2020
ms.locfileid: "85918220"
---
# <a name="reqcompletionroutine-rule-kmdf"></a>ReqCompletionRoutine ルール (kmdf)


**ReqCompletionRoutine**規則は、要求が i/o ターゲットに送信される前に完了ルーチンを設定する必要があることを指定します。

要求が同期的に送信されない場合、または送信および破棄として送信されない場合 ( **WDF \_ request \_ send \_ オプションの \_ send \_ と \_ 忘れる**フラグによって指定されます)、ドライバーは、要求が完了したときに i/o ターゲットがドライバーに通知できるように、完了ルーチンを設定する必要があります。

**ドライバーモデル: KMDF**

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
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/static-driver-verifier" data-raw-source="[Static Driver Verifier](https://docs.microsoft.com/windows-hardware/drivers/devtest/static-driver-verifier)">静的ドライバー検証ツール</a>を実行し、 <strong>ReqCompletionRoutine</strong>規則を指定します。</p>
コードの分析を実行するには、次の手順に従います。
<ol>
<li><a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers#preparing-your-source-code" data-raw-source="[Prepare your code (use role type declarations).](https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers#preparing-your-source-code)">コードを準備します (役割の種類の宣言を使います)。</a></li>
<li><a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers#running-static-driver-verifier" data-raw-source="[Run Static Driver Verifier.](https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers#running-static-driver-verifier)">静的ドライバー検証ツールを実行します。</a></li>
<li><a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers#viewing-and-analyzing-the-results" data-raw-source="[View and analyze the results.](https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers#viewing-and-analyzing-the-results)">結果を表示して分析します。</a></li>
</ol>
<p>詳細については、「 <a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers" data-raw-source="[Using Static Driver Verifier to Find Defects in Drivers](https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers)">Static Driver Verifier を使用したドライバーの欠陥の検出</a>」を参照してください。</p></td>
</tr>
</tbody>
</table>

<a name="applies-to"></a>適用対象
----------

[**Wdfrequestsend**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestsend) 
[**Wdfrequestset補完ルーチン**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestsetcompletionroutine)関連項目
--------

[I/o 要求](https://docs.microsoft.com/windows-hardware/drivers/wdf/completing-i-o-requests) 
 を完了しています[キャンセルと完了コード](https://docs.microsoft.com/windows-hardware/drivers/wdf/synchronizing-cancel-and-completion-code) 
 の同期[**WDF \_要求 \_ 送信 \_ オプション \_ フラグ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/ne-wdfrequest-_wdf_request_send_options_flags) 
 [**WDF \_ 要求の \_ 送信 \_ オプション**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/ns-wdfrequest-_wdf_request_send_options)
 

 






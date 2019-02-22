---
title: ReqNotCanceledLocal ルール (kmdf)
description: ReqNotCanceledLocal ルールを既定の I/O キューのコールバック関数で取り消し可能としてマークされている要求を完了すると場合、WdfRequestUnmarkCancelable メソッド呼び出す必要がありますの完了前に、I/O 要求でを指定します。
ms.assetid: 3cc3d517-6fb9-46b2-9d22-6bdbef442007
ms.date: 05/21/2018
keywords:
- ReqNotCanceledLocal ルール (kmdf)
topic_type:
- apiref
api_name:
- ReqNotCanceledLocal
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 0219b8a27eb7fe6fc1cccc34028b6f97216659a4
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56527665"
---
# <a name="reqnotcanceledlocal-rule-kmdf"></a>ReqNotCanceledLocal ルール (kmdf)


**ReqNotCanceledLocal**ルール完了を指定する要求がキャンセル可能としてマークされている場合は、既定 I/O キュー コールバック関数で、 [ **WdfRequestUnmarkCancelable** ](https://msdn.microsoft.com/library/windows/hardware/ff550035)完了前に、I/O 要求のメソッドを呼び出す必要があります。 呼び出す前に、要求が取り消された場合を除き、I/O 要求を完了する必要があります**WdfRequestUnmarkCancelable**します。

場合によっては、キャンセル可能なマークされた要求[ **WdfRequestMarkCancelable** ](https://msdn.microsoft.com/library/windows/hardware/ff549983)が完了 (呼び出して[ **WdfRequestComplete**](https://msdn.microsoft.com/library/windows/hardware/ff549945)、[ **WdfRequestCompleteWithInformation**](https://msdn.microsoft.com/library/windows/hardware/ff549948)、または[ **WdfRequestCompleteWithPriorityBoost**](https://msdn.microsoft.com/library/windows/hardware/ff549949))、 [ **WdfRequestUnmarkCancelable** ](https://msdn.microsoft.com/library/windows/hardware/ff550035) I/O 要求が完了する前に、メソッドを呼び出す必要があります。 しない限り、要求を完了する、 **WdfRequestUnmarkCancelable**メソッドに相当するステータスを返します**状態\_CANCELLED**します。

要求の既定の I/O キューのコールバック関数は、 [ *EvtIoDefault*](https://msdn.microsoft.com/library/windows/hardware/ff541757)、 [ *EvtIoRead*](https://msdn.microsoft.com/library/windows/hardware/ff541776)、 [ *EvtIoWrite*](https://msdn.microsoft.com/library/windows/hardware/ff541813)、 [ *EvtIoDeviceControl*](https://msdn.microsoft.com/library/windows/hardware/ff541758)、 [ *EvtIoInternalDeviceControl* ](https://msdn.microsoft.com/library/windows/hardware/ff541768).

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
<td align="left"><p>実行<a href="https://msdn.microsoft.com/library/windows/hardware/ff552808" data-raw-source="[Static Driver Verifier](https://msdn.microsoft.com/library/windows/hardware/ff552808)">Static Driver Verifier</a>を指定し、 <strong>ReqNotCanceledLocal</strong>ルール。</p>
コードの分析を実行するには、次の手順に従います。
<ol>
<li><a href="https://msdn.microsoft.com/library/windows/hardware/hh454281#preparing-your-source-code" data-raw-source="[Prepare your code (use role type declarations).](https://msdn.microsoft.com/library/windows/hardware/hh454281#preparing-your-source-code)">(ロールの型宣言の使用)、コードを準備します。</a></li>
<li><a href="https://msdn.microsoft.com/library/windows/hardware/hh454281#running-static-driver-verifier" data-raw-source="[Run Static Driver Verifier.](https://msdn.microsoft.com/library/windows/hardware/hh454281#running-static-driver-verifier)">Static Driver Verifier を実行します。</a></li>
<li><a href="https://msdn.microsoft.com/library/windows/hardware/hh454281#viewing-and-analyzing-the-results" data-raw-source="[View and analyze the results.](https://msdn.microsoft.com/library/windows/hardware/hh454281#viewing-and-analyzing-the-results)">表示し、結果を分析します。</a></li>
</ol>
<p>詳細については、次を参照してください。<a href="https://msdn.microsoft.com/library/windows/hardware/hh454281" data-raw-source="[Using Static Driver Verifier to Find Defects in Drivers](https://msdn.microsoft.com/library/windows/hardware/hh454281)">ドライバーで障害を検出する Static Driver Verifier を使用して</a>します。</p></td>
</tr>
</tbody>
</table>

<a name="applies-to"></a>適用対象
----------

[**WdfRequestComplete**](https://msdn.microsoft.com/library/windows/hardware/ff549945)
[**WdfRequestCompleteWithInformation** ](https://msdn.microsoft.com/library/windows/hardware/ff549948) 
 [ **WdfRequestCompleteWithPriorityBoost**](https://msdn.microsoft.com/library/windows/hardware/ff549949)
[**WdfRequestMarkCancelable** ](https://msdn.microsoft.com/library/windows/hardware/ff549983) 
 [ **WdfRequestMarkCancelableEx**](https://msdn.microsoft.com/library/windows/hardware/ff549984)
[**WdfRequestUnmarkCancelable**](https://msdn.microsoft.com/library/windows/hardware/ff550035)
 

 






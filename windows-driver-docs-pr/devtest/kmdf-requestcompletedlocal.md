---
title: RequestCompletedLocal ルール (kmdf)
description: RequestCompletedLocal ルールことを指定します、EvtIoDefault、EvtIoRead、EvtIoWrite、EvtIoDeviceControl、および EvtIoInternalDeviceControl のコールバック関数のいずれかで、I/O 要求を完了していない場合とで WdfRequestMarkCancelable が呼び出されていない場合、コールバック関数内で要求するドライバーのコードで要求の完了に問題がある可能性があります。
ms.assetid: bc36da0c-5507-49a1-89d9-046d66c8f831
ms.date: 05/21/2018
keywords:
- RequestCompletedLocal ルール (kmdf)
topic_type:
- apiref
api_name:
- RequestCompletedLocal
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 7b67a3169823b84e6987d81b0727780c4cf54ca5
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56580754"
---
# <a name="requestcompletedlocal-rule-kmdf"></a>RequestCompletedLocal ルール (kmdf)


**RequestCompletedLocal**ルールを指定するのいずれかで、I/O 要求を完了していない場合、 [ *EvtIoDefault*](https://msdn.microsoft.com/library/windows/hardware/ff541757)、 [ *EvtIoRead* ](https://msdn.microsoft.com/library/windows/hardware/ff541776)、 [ *EvtIoWrite*](https://msdn.microsoft.com/library/windows/hardware/ff541813)、 [ *EvtIoDeviceControl*](https://msdn.microsoft.com/library/windows/hardware/ff541758)、および[*EvtIoInternalDeviceControl* ](https://msdn.microsoft.com/library/windows/hardware/ff541768)コールバック関数と if [ **WdfRequestMarkCancelable** ](https://msdn.microsoft.com/library/windows/hardware/ff549983)内での要求では呼び出されませんでした、コールバック関数では、ドライバーのコードで要求の完了に問題がある可能性があります。

この規則の対象のドライバーの目的はのみ、 [RequestCompleted](kmdf-requestcompleted.md)ルールは適用されません。

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
<td align="left"><p>実行<a href="https://msdn.microsoft.com/library/windows/hardware/ff552808" data-raw-source="[Static Driver Verifier](https://msdn.microsoft.com/library/windows/hardware/ff552808)">Static Driver Verifier</a>を指定し、 <strong>RequestCompletedLocal</strong>ルール。</p>
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

<a name="applies-to"></a>対象
----------

[**WdfDeviceEnqueueRequest**](https://msdn.microsoft.com/library/windows/hardware/ff545945)
[**WdfDmaTransactionInitialize** ](https://msdn.microsoft.com/library/windows/hardware/ff547099) 
 [ **WdfDmaTransactionInitializeUsingRequest**](https://msdn.microsoft.com/library/windows/hardware/ff547107)
[**WdfIoTargetSendInternalIoctlOthersSynchronously** ](https://msdn.microsoft.com/library/windows/hardware/ff548651) 
[ **WdfIoTargetSendInternalIoctlSynchronously**](https://msdn.microsoft.com/library/windows/hardware/ff548656)
[**WdfIoTargetSendIoctlSynchronously** ](https://msdn.microsoft.com/library/windows/hardware/ff548660) 
 [ **WdfIoTargetSendReadSynchronously**](https://msdn.microsoft.com/library/windows/hardware/ff548669)
[**WdfIoTargetSendWriteSynchronously**](https://msdn.microsoft.com/library/windows/hardware/ff548672) 
 [ **WdfRequestComplete**](https://msdn.microsoft.com/library/windows/hardware/ff549945)
[**WdfRequestCompleteWithInformation**](https://msdn.microsoft.com/library/windows/hardware/ff549948) 
 [ **WdfRequestCompleteWithPriorityBoost** ](https://msdn.microsoft.com/library/windows/hardware/ff549949) 
 [ **WdfRequestForwardToIoQueue**](https://msdn.microsoft.com/library/windows/hardware/ff549958)
[**WdfRequestMarkCancelable** ](https://msdn.microsoft.com/library/windows/hardware/ff549983) 
 [ **WdfRequestMarkCancelableEx**](https://msdn.microsoft.com/library/windows/hardware/ff549984)
[**WdfRequestSend** ](https://msdn.microsoft.com/library/windows/hardware/ff550027) 
 [ **WdfRequestStopAcknowledge**](https://msdn.microsoft.com/library/windows/hardware/ff550033)
[**WdfWorkItemEnqueue**](https://msdn.microsoft.com/library/windows/hardware/ff551203)
 

 






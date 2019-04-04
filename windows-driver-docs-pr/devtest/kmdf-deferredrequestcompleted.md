---
title: DeferredRequestCompleted ルール (kmdf)
description: DeferredRequestCompleted ルールでは、ドライバーの既定の I/O キューに表示される、I/O 要求は、コールバック関数では、完了していないが、後で処理の遅延が場合、要求する必要があるが完了している、遅延処理のコールバック関数を指定します要求が転送され、フレームワークに配信しない限り、または WdfRequestStopAcknowledge メソッドが呼び出された場合を除き、します。
ms.assetid: 14ed0dda-8acb-48fe-933f-e498c41f5403
ms.date: 05/21/2018
keywords:
- DeferredRequestCompleted ルール (kmdf)
topic_type:
- apiref
api_name:
- DeferredRequestCompleted
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 96a4a462b858be1d066a6a8e587eaa4b2007d26a
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56532085"
---
# <a name="deferredrequestcompleted-rule-kmdf"></a>DeferredRequestCompleted ルール (kmdf)


**DeferredRequestCompleted**規則を指定する場合、ドライバーの既定の I/O キューに表示される、I/O 要求は、コールバック関数では、完了していないが、後で処理の遅延が、要求する必要がありますを完了、遅延でコールバック関数の処理か、要求が転送され、フレームワークに配信される場合を除き、 [ **WdfRequestStopAcknowledge** ](https://msdn.microsoft.com/library/windows/hardware/ff550033)メソッドが呼び出されます。

**DeferredRequestCompleted**ルールを使用して遅延の要求を識別することが必要です、  **\_ \_sdv\_保存\_要求**と**\_ \_sdv\_取得\_要求**マクロ。 これらのマクロを使用する方法については、次を参照してください[Using \_ \_sdv\_保存\_要求と\_ \_sdv\_取得\_の要求。遅延プロシージャ呼び出し](https://msdn.microsoft.com/library/windows/hardware/ff556071)します。 前提条件規則**AliasWithinTimerDpc**これらのマクロの存在を確認します。

終了前に、I/O 要求のコールバック関数からを除き、次の場合、キューのコールバック関数のいずれかで、ドライバーの既定のキューに表示され、遅延の要求を完了する必要があります。

-   I/O 要求が I/O のターゲットに、または別のキューに転送されました

-   I/O 要求がフレームワークに配信されました (呼び出して[ **WdfDeviceEnqueueRequest**](https://msdn.microsoft.com/library/windows/hardware/ff545945))

-   **WdfRequestStopAcknowledge**メソッドが呼び出されました

ドライバーは、次のコールバック関数を終了したときに、規則が確認済み。

-   **EvtIoStop**、 **EvtCleanupCallback**または**EvtDestroyCallback**キュー

-   **EvtCleanupCallback**または**EvtDestroyCallback**ファイルのオブジェクト

-   **EvtFileClose**、 **EvtFileCleanup**、 **EvtDeviceSelfManagedIoSuspend**、 **EvtDeviceSelfManagedIoFlush**、 **EvtDeviceSelfManagedIoCleanup**、 **EvtDeviceShutdownNotification**、 **EvtDeviceSurpriseRemoval**、 **EvtCleanupCallback**または**EvtDestroyCallback**デバイス

-   **EvtDriverUnload**

プレゼンテーションは、I/O に対して I/O キューのコールバック関数の要求**EvtIoDefault**、 **EvtIoRead**、 **EvtIoWrite**、 **EvtIoDeviceControl**、および**EvtIoInternalDeviceControl**します。

I/O 要求の遅延処理のコールバック関数は**EvtTimerFunc**、 **EvtDpcFunc**、 **EvtInterruptDpc**、 **EvtInterruptEnable**、 **EvtInterruptDisable**、および**EvtWorkItem**します。

**DeferredRequestCompleted**ルールの呼び出しを使用して、 **WdfRequestMarkCancelable**、 **WdfDmaTransactionInitializeUsingRequest**、 **WdfDmaTransactionInitialize**、または**WdfWorkItemEnqueue**メソッドを I/O 要求が遅延されることを示します。

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
<td align="left"><p>実行<a href="https://msdn.microsoft.com/library/windows/hardware/ff552808" data-raw-source="[Static Driver Verifier](https://msdn.microsoft.com/library/windows/hardware/ff552808)">Static Driver Verifier</a>を指定し、 <strong>DeferredRequestCompleted</strong>ルール。</p>
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
[**WdfRequestUnmarkCancelable** ](https://msdn.microsoft.com/library/windows/hardware/ff550035)
 [ **WdfWorkItemEnqueue**](https://msdn.microsoft.com/library/windows/hardware/ff551203)
 

 






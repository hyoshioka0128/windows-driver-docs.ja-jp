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
ms.openlocfilehash: 4c38aa3c239ab500a874f9cd63b5b6ea81bf845f
ms.sourcegitcommit: f663c383886d87ea762e419963ff427500cc5042
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67393182"
---
# <a name="deferredrequestcompleted-rule-kmdf"></a>DeferredRequestCompleted ルール (kmdf)


**DeferredRequestCompleted**規則を指定する場合、ドライバーの既定の I/O キューに表示される、I/O 要求は、コールバック関数では、完了していないが、後で処理の遅延が、要求する必要がありますを完了、遅延でコールバック関数の処理か、要求が転送され、フレームワークに配信される場合を除き、 [ **WdfRequestStopAcknowledge** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nf-wdfrequest-wdfrequeststopacknowledge)メソッドが呼び出されます。

**DeferredRequestCompleted**ルールを使用して遅延の要求を識別することが必要です、  **\_ \_sdv\_保存\_要求**と **\_ \_sdv\_取得\_要求**マクロ。 これらのマクロを使用する方法については、次を参照してください[Using \_ \_sdv\_保存\_要求と\_ \_sdv\_取得\_の要求。遅延プロシージャ呼び出し](https://docs.microsoft.com/windows-hardware/drivers/devtest/using---sdv-save-request-and---sdv-retrieve-request-for-deferred-proce)します。 前提条件規則**AliasWithinTimerDpc**これらのマクロの存在を確認します。

終了前に、I/O 要求のコールバック関数からを除き、次の場合、キューのコールバック関数のいずれかで、ドライバーの既定のキューに表示され、遅延の要求を完了する必要があります。

-   I/O 要求が I/O のターゲットに、または別のキューに転送されました

-   I/O 要求がフレームワークに配信されました (呼び出して[ **WdfDeviceEnqueueRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nf-wdfdevice-wdfdeviceenqueuerequest))

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
<td align="left"><p>実行<a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/static-driver-verifier" data-raw-source="[Static Driver Verifier](https://docs.microsoft.com/windows-hardware/drivers/devtest/static-driver-verifier)">Static Driver Verifier</a>を指定し、 <strong>DeferredRequestCompleted</strong>ルール。</p>
コードの分析を実行するには、次の手順に従います。
<ol>
<li><a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers#preparing-your-source-code" data-raw-source="[Prepare your code (use role type declarations).](https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers#preparing-your-source-code)">(ロールの型宣言の使用)、コードを準備します。</a></li>
<li><a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers#running-static-driver-verifier" data-raw-source="[Run Static Driver Verifier.](https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers#running-static-driver-verifier)">Static Driver Verifier を実行します。</a></li>
<li><a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers#viewing-and-analyzing-the-results" data-raw-source="[View and analyze the results.](https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers#viewing-and-analyzing-the-results)">表示し、結果を分析します。</a></li>
</ol>
<p>詳細については、次を参照してください。<a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers" data-raw-source="[Using Static Driver Verifier to Find Defects in Drivers](https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers)">ドライバーで障害を検出する Static Driver Verifier を使用して</a>します。</p></td>
</tr>
</tbody>
</table>

<a name="applies-to"></a>適用対象
----------

[**WdfDeviceEnqueueRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nf-wdfdevice-wdfdeviceenqueuerequest)
[**WdfDmaTransactionInitialize** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdmatransaction/nf-wdfdmatransaction-wdfdmatransactioninitialize) 
 [ **WdfDmaTransactionInitializeUsingRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdmatransaction/nf-wdfdmatransaction-wdfdmatransactioninitializeusingrequest)
[**WdfIoTargetSendInternalIoctlOthersSynchronously** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfiotarget/nf-wdfiotarget-wdfiotargetsendinternalioctlotherssynchronously) 
[ **WdfIoTargetSendInternalIoctlSynchronously**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfiotarget/nf-wdfiotarget-wdfiotargetsendinternalioctlsynchronously)
[**WdfIoTargetSendIoctlSynchronously** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfiotarget/nf-wdfiotarget-wdfiotargetsendioctlsynchronously) 
 [ **WdfIoTargetSendReadSynchronously**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfiotarget/nf-wdfiotarget-wdfiotargetsendreadsynchronously)
[**WdfIoTargetSendWriteSynchronously**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfiotarget/nf-wdfiotarget-wdfiotargetsendwritesynchronously) 
 [ **WdfRequestComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nf-wdfrequest-wdfrequestcomplete)
[**WdfRequestCompleteWithInformation**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nf-wdfrequest-wdfrequestcompletewithinformation) 
 [ **WdfRequestCompleteWithPriorityBoost** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nf-wdfrequest-wdfrequestcompletewithpriorityboost) 
 [ **WdfRequestForwardToIoQueue**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nf-wdfrequest-wdfrequestforwardtoioqueue)
[**WdfRequestMarkCancelable** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nf-wdfrequest-wdfrequestmarkcancelable) 
 [ **WdfRequestMarkCancelableEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nf-wdfrequest-wdfrequestmarkcancelableex)
[**WdfRequestSend** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nf-wdfrequest-wdfrequestsend) 
 [ **WdfRequestStopAcknowledge**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nf-wdfrequest-wdfrequeststopacknowledge)
[**WdfRequestUnmarkCancelable** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nf-wdfrequest-wdfrequestunmarkcancelable)
 [ **WdfWorkItemEnqueue**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfworkitem/nf-wdfworkitem-wdfworkitemenqueue)
 

 






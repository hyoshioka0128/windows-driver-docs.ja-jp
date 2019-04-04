---
title: RequestCompleted ルール (kmdf)
description: DeferredRequestCompleted ルールでは、非フィルター ドライバーのドライバーの既定の I/O キューに表示される各要求する必要がありますが完了したこと、WdfRequestStopAcknowledge が呼び出された場合、要求が遅延または転送、しない限り、またはを指定します。
ms.assetid: fb034d81-d49d-43a5-92b9-9b4e3f3056ee
ms.date: 05/21/2018
keywords:
- RequestCompleted ルール (kmdf)
topic_type:
- apiref
api_name:
- RequestCompleted
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 9e82f7bc398cca3626b207be36fd80b16866e7f9
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56582030"
---
# <a name="requestcompleted-rule-kmdf"></a>RequestCompleted ルール (kmdf)


[ **DeferredRequestCompleted** ](kmdf-deferredrequestcompleted.md)非フィルター ドライバーのドライバーの既定の I/O キューに表示される各要求する必要がありますが完了したこと、要求が遅延または転送、しない限り、規則を指定または場合[ **WdfRequestStopAcknowledge** ](https://msdn.microsoft.com/library/windows/hardware/ff550033)が呼び出されます。

次の場合を除く、I/O 要求のコールバック関数を終了、前に、キューのコールバック関数のいずれかで、ドライバーの既定のキューに表示される、I/O 要求を完了する必要があります。

-   要求の遅延 (DPC または作業項目、たとえば)。 この場合、使用することができます、 [DeferredRequestCompleted](kmdf-deferredrequestcompleted.md)ルール。

-   I/O のターゲットに、または別のキューに要求が転送されます。

-   フレームワークに、要求が配信されました (呼び出して[ **WdfDeviceEnqueueRequest**](https://msdn.microsoft.com/library/windows/hardware/ff545945))

-   [**WdfRequestStopAcknowledge** ](https://msdn.microsoft.com/library/windows/hardware/ff550033)が呼び出されました

ドライバーは、次のコールバック関数を終了したときに、規則が確認済み。

-   [*EvtIoStop*](https://msdn.microsoft.com/library/windows/hardware/ff541788)、 [ *EvtCleanupCallback* ](https://msdn.microsoft.com/library/windows/hardware/ff540840)または[ *EvtDestroyCallback* ](https://msdn.microsoft.com/library/windows/hardware/ff540841)キュー

-   [*EvtCleanupCallback* ](https://msdn.microsoft.com/library/windows/hardware/ff540840)または[ *EvtDestroyCallback* ](https://msdn.microsoft.com/library/windows/hardware/ff540841)ファイルのオブジェクト

-   [*EvtFileClose*](https://msdn.microsoft.com/library/windows/hardware/ff541702)、 [ *EvtFileCleanup*](https://msdn.microsoft.com/library/windows/hardware/ff541700)、 [ *EvtDeviceSelfManagedIoSuspend*](https://msdn.microsoft.com/library/windows/hardware/ff540907)、 [ *EvtDeviceSelfManagedIoFlush*](https://msdn.microsoft.com/library/windows/hardware/ff540901)、 [ *EvtDeviceSelfManagedIoCleanup*](https://msdn.microsoft.com/library/windows/hardware/ff540898)、 [ *EvtDeviceShutdownNotification*](https://msdn.microsoft.com/library/windows/hardware/ff540911)、 [ *EvtDeviceSurpriseRemoval*](https://msdn.microsoft.com/library/windows/hardware/ff540913)、 [ *EvtCleanupCallback*](https://msdn.microsoft.com/library/windows/hardware/ff540840)または[ *EvtDestroyCallback* ](https://msdn.microsoft.com/library/windows/hardware/ff540841)デバイス

-   [*EvtDriverUnload*](https://msdn.microsoft.com/library/windows/hardware/ff541694)

要求のプレゼンテーションの I/O キューのコールバック関数は[ *EvtIoDefault*](https://msdn.microsoft.com/library/windows/hardware/ff541757)、 [ *EvtIoRead*](https://msdn.microsoft.com/library/windows/hardware/ff541776)、 [ *EvtIoWrite*](https://msdn.microsoft.com/library/windows/hardware/ff541813)、 [ *EvtIoDeviceControl*](https://msdn.microsoft.com/library/windows/hardware/ff541758)、および[ *EvtIoInternalDeviceControl*](https://msdn.microsoft.com/library/windows/hardware/ff541768)

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
<td align="left"><p>実行<a href="https://msdn.microsoft.com/library/windows/hardware/ff552808" data-raw-source="[Static Driver Verifier](https://msdn.microsoft.com/library/windows/hardware/ff552808)">Static Driver Verifier</a>を指定し、 <strong>RequestCompleted</strong>ルール。</p>
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
 

 






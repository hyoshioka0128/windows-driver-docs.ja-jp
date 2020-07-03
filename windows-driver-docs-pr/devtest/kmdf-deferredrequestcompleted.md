---
title: DeferredRequestCompleted ルール (kmdf)
description: DeferredRequestCompleted ルールでは、ドライバーの既定の i/o キューに提示された i/o 要求がコールバック関数では完了せず、後で処理するために遅延される場合、要求が転送されてフレームワークに配信されない限り、要求は遅延処理コールバック関数で完了する必要があります。
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
ms.openlocfilehash: f698bfcb3314a4ef6ab2eccbce5f1ca119935ce9
ms.sourcegitcommit: 82a9be3b3584f991e5121f8f46a972e04185fa52
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/02/2020
ms.locfileid: "85918030"
---
# <a name="deferredrequestcompleted-rule-kmdf"></a>DeferredRequestCompleted ルール (kmdf)


**DeferredRequestCompleted**ルールでは、ドライバーの既定の i/o キューに提示された i/o 要求がコールバック関数では完了せず、後で処理するために遅延される場合、要求が転送されてフレームワークに配信されない限り、要求は遅延処理コールバック関数で[**WdfRequestStopAcknowledge**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequeststopacknowledge)完了する必要があります。

**DeferredRequestCompleted**ルールでは、 ** \_ \_ sdv \_ save \_ 要求**マクロと** \_ \_ sdv \_ 取得 \_ 要求**マクロを使用して遅延要求を識別する必要があります。 これらのマクロの使用方法の詳細については、「 [ \_ \_ sdv \_ \_ の保存要求の使用」および「 \_ \_ \_ \_ 遅延プロシージャ呼び出しのための sdv の取得要求](https://docs.microsoft.com/windows-hardware/drivers/devtest/using---sdv-save-request-and---sdv-retrieve-request-for-deferred-proce)」を参照してください。 前提条件の規則**AliasWithinTimerDpc**は、これらのマクロの存在を確認します。

キューのコールバック関数と遅延の1つを通じて、ドライバーの既定のキューに提示される要求は、次の場合を除き、i/o 要求のコールバック関数から抜ける前に完了する必要があります。

-   I/o 要求は、i/o ターゲットまたは別のキューに転送されました

-   I/o 要求がフレームワークに配信されました ( [**Wdfdeviceenqueuerequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdeviceenqueuerequest)呼び出すことによって)

-   **Wdfrequeststopacknowledge**メソッドが呼び出されました

このルールは、ドライバーが次のコールバック関数から終了したときに検証されます。

-   キューの**Evtiostop**、 **evtiostop** 、または**evtiostop**

-   File オブジェクトの**Evtcleanupcallback**または**Evtcleanupcallback**

-   **Evtfileclose**、 **EvtFileCleanup**、 **evtdeviceselfmanagediosuspend**、 **EvtDeviceSelfManagedIoFlush**、 **evtdeviceselfmanagediocleanup、evtdevice**、デバイスの**EvtDeviceSurpriseRemoval**、 **evtcleanupcallback** 、または**evtdestroycallback** **EvtDeviceShutdownNotification**

-   **EvtDriverUnload**

I/o 要求プレゼンテーション用の i/o キューコールバック関数は、 **Evtiodefault**、 **EvtIoRead**、 **evtiodefault**、 **Evtiodevicecontrol**、および**evtiointernaldevicecontrol**です。

I/o 要求の遅延処理のコールバック関数は、 **Evttimerfunc**、 **EvtDpcFunc**、 **EvtInterruptDpc**、 **EvtInterruptEnable**、 **EvtInterruptDisable**、および**evtworkitem**です。

**DeferredRequestCompleted**ルールでは、 **Wdfrequestmarkcancelable** **wdfdmatransactioninitializeuses 要求**、 **wdfdmatransactioninitialize**、または**wdfworkitemのエンキュー**メソッドの呼び出しを使用して、i/o 要求が遅延していることを示します。

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
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/static-driver-verifier" data-raw-source="[Static Driver Verifier](https://docs.microsoft.com/windows-hardware/drivers/devtest/static-driver-verifier)">静的ドライバー検証ツール</a>を実行し、 <strong>DeferredRequestCompleted</strong>規則を指定します。</p>
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

[**Wdfdeviceenqueuerequest 
[**Wdfdmatransactioninitialize**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdmatransaction/nf-wdfdmatransaction-wdfdmatransactioninitialize) 
[**Wdfdmatransactioninitializeenabled 要求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdmatransaction/nf-wdfdmatransaction-wdfdmatransactioninitializeusingrequest) 
[**WdfIoTargetSendInternalIoctlOthersSynchronously**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfiotarget/nf-wdfiotarget-wdfiotargetsendinternalioctlotherssynchronously) 
[**Wdfiotargetsend、同期的**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfiotarget/nf-wdfiotarget-wdfiotargetsendinternalioctlsynchronously) 
 に[**Wdfiotargetsendioctlsynchronously**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfiotarget/nf-wdfiotarget-wdfiotargetsendioctlsynchronously) 
[**Wdfiotargetsendreadsynchronously**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfiotarget/nf-wdfiotarget-wdfiotargetsendreadsynchronously) 
[**WdfIoTargetSendWriteSynchronously**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfiotarget/nf-wdfiotarget-wdfiotargetsendwritesynchronously) 
[**Wdfrequestcomplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestcomplete) 
[**Wdfrequestcompletewithinformation**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestcompletewithinformation) 
[**Wdfrequestcompletewith優先順位ブースト**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestcompletewithpriorityboost) 
[**Wdfrequestforwardtoioqueue**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestforwardtoioqueue) 
[**Wdfrequestmarkcancelable**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestmarkcancelable) 
 可能[**Wdfrequestmarkcancelableex**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestmarkcancelableex) 
[**Wdfrequestsend**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestsend) 
[**Wdfrequeststopacknowledge**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequeststopacknowledge) 
[**Wdfrequestunmarkcancelable**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestunmarkcancelable) 
 可能[**Wdfworkitemenqueue キュー**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfworkitem/nf-wdfworkitem-wdfworkitemenqueue)**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdeviceenqueuerequest)
 

 






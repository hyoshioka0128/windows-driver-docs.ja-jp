---
title: DeferredRequestCompleted ルール (kmdf)
description: DeferredRequestCompleted ルールは、ドライバーの既定の i/o キューに提示された i/o 要求がコールバック関数では完了せず、後で処理するために遅延される場合、遅延処理のコールバック関数で要求を完了する必要があることを指定します。要求が転送されてフレームワークに配信されない限り、または WdfRequestStopAcknowledge メソッドが呼び出されない限り。
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
ms.openlocfilehash: 9af9c81ee0f38132368f4dada39b1ca1a8a666a1
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72840235"
---
# <a name="deferredrequestcompleted-rule-kmdf"></a>DeferredRequestCompleted ルール (kmdf)


**DeferredRequestCompleted**ルールは、ドライバーの既定の i/o キューに提示された i/o 要求がコールバック関数では完了せず、後で処理するために遅延される場合、遅延処理のコールバックで要求を完了する必要があることを指定します。関数。要求が転送されてフレームワークに配信される場合、または[**Wdfrequeststopacknowledge**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequeststopacknowledge)メソッドが呼び出されない場合はです。

**DeferredRequestCompleted**ルールでは、 **\_\_sdv\_** を使用して遅延要求を識別し、\_要求を保存し\_\_**sdv\_\_要求**マクロを取得する必要があります。 これらのマクロの使用方法の詳細については、「 [\_\_sdv\_を使用して\_要求を保存する」および「\_\_sdv\_遅延プロシージャ呼び出しの要求\_取得](https://docs.microsoft.com/windows-hardware/drivers/devtest/using---sdv-save-request-and---sdv-retrieve-request-for-deferred-proce)する」を参照してください。 前提条件の規則**AliasWithinTimerDpc**は、これらのマクロの存在を確認します。

キューのコールバック関数と遅延の1つを通じて、ドライバーの既定のキューに提示される要求は、次の場合を除き、i/o 要求のコールバック関数から抜ける前に完了する必要があります。

-   I/o 要求は、i/o ターゲットまたは別のキューに転送されました

-   I/o 要求がフレームワークに配信されました ( [**Wdfdeviceenqueuerequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdeviceenqueuerequest)呼び出すことによって)

-   **Wdfrequeststopacknowledge**メソッドが呼び出されました

このルールは、ドライバーが次のコールバック関数から終了したときに検証されます。

-   キューの**Evtiostop**、 **evtiostop** 、または**evtiostop**

-   File オブジェクトの**Evtcleanupcallback**または**Evtcleanupcallback**

-   **Evtfileclose**、 **EvtFileCleanup**、 **evtdeviceselfmanagediosuspend**、 **EvtDeviceSelfManagedIoFlush**、 **evtdeviceselfmanagediocleanup、evtdevice**、デバイスの**EvtDeviceSurpriseRemoval**、 **evtcleanupcallback** 、または**evtdestroycallback**

-   **EvtDriverUnload**

I/o 要求プレゼンテーション用の i/o キューコールバック関数は、 **Evtiodefault**、 **EvtIoRead**、 **evtiodefault**、 **Evtiodevicecontrol**、および**evtiointernaldevicecontrol**です。

I/o 要求の遅延処理のコールバック関数は、 **Evttimerfunc**、 **EvtDpcFunc**、 **EvtInterruptDpc**、 **EvtInterruptEnable**、 **EvtInterruptDisable**、および**evtworkitem**です。

**DeferredRequestCompleted**ルールでは、 **Wdfrequestmarkcancelable** **wdfdmatransactioninitializeuses 要求**、 **wdfdmatransactioninitialize**、または**wdfworkitemのエンキュー**メソッドの呼び出しを使用して、i/o 要求が遅延しています。

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
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/static-driver-verifier" data-raw-source="[Static Driver Verifier](https://docs.microsoft.com/windows-hardware/drivers/devtest/static-driver-verifier)">静的ドライバー検証ツール</a>を実行し、 <strong>DeferredRequestCompleted</strong>規則を指定します。</p>
コードの分析を実行するには、次の手順に従います。
<ol>
<li><a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers#preparing-your-source-code" data-raw-source="[Prepare your code (use role type declarations).](https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers#preparing-your-source-code)">コードを準備します (ロールの種類の宣言を使用します)。</a></li>
<li><a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers#running-static-driver-verifier" data-raw-source="[Run Static Driver Verifier.](https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers#running-static-driver-verifier)">静的ドライバー検証ツールを実行します。</a></li>
<li><a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers#viewing-and-analyzing-the-results" data-raw-source="[View and analyze the results.](https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers#viewing-and-analyzing-the-results)">結果を表示して分析します。</a></li>
</ol>
<p>詳細については、「 <a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers" data-raw-source="[Using Static Driver Verifier to Find Defects in Drivers](https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers)">Static Driver Verifier を使用したドライバーの欠陥の検出</a>」を参照してください。</p></td>
</tr>
</tbody>
</table>

<a name="applies-to"></a>適用対象
----------

Wd
[**Deviceenqueu
** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdeviceenqueuerequest) [**Wdfdmatransactioninitialize**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdmatransaction/nf-wdfdmatransaction-wdfdmatransactioninitialize) [**Wdfdmatransactioninitializeon request**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdmatransaction/nf-wdfdmatransaction-wdfdmatransactioninitializeusingrequest)

[**WdfIoTargetSendInternalIoctlOthersSynchronously**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfiotarget/nf-wdfiotarget-wdfiotargetsendinternalioctlotherssynchronously)を[**同期的**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfiotarget/nf-wdfiotarget-wdfiotargetsendinternalioctlsynchronously)に同期的に
wdfiotargetsendioctlは同期的に
wdfiotargetsendientl
[**WdfIoTargetSendWriteSynchronously**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfiotarget/nf-wdfiotarget-wdfiotargetsendwritesynchronously)
[](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfiotarget/nf-wdfiotarget-wdfiotargetsendioctlsynchronously) [](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfiotarget/nf-wdfiotarget-wdfiotargetsendreadsynchronously) [**WdfRequestComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestcomplete)
[**wdfrequestcompletewith
** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestcompletewithinformation) [**Wdfrequestcompletetoioブースト**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestcompletewithpriorityboost)
[**Wdfrequestforwardtoioqueue**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestforwardtoioqueue)
[**Wdfrequestmarkを**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestmarkcancelable)
[**Wdfrequestmarkcancelableex
Wdfrequestmarkcancelableex**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestmarkcancelableex)
Wdfrequestunmarkcancel
[](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestsend) wdfworkitemunmarkキャンセル[](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestunmarkcancelable) [ **
** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequeststopacknowledge) [**wdfrequestcomplete エンキュー**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfworkitem/nf-wdfworkitem-wdfworkitemenqueue)
 

 






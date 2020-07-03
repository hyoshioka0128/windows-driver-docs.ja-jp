---
title: MdlAfterReqCompletedWriteA ルール (kmdf)
description: MdlAfterReqCompletedWriteA ルールは、EvtIoWrite コールバック関数内で、i/o 要求の完了後に取得されたメモリ記述子リスト (MDL) オブジェクトにアクセスできないことを指定します。
ms.assetid: 325a5ef6-459d-4457-bbad-774c76ddcdb9
ms.date: 05/21/2018
keywords:
- MdlAfterReqCompletedWriteA ルール (kmdf)
topic_type:
- apiref
api_name:
- MdlAfterReqCompletedWriteA
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: f73d83bcf192df0e76d0ddb3b549109020cd7197
ms.sourcegitcommit: 82a9be3b3584f991e5121f8f46a972e04185fa52
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/02/2020
ms.locfileid: "85918168"
---
# <a name="mdlafterreqcompletedwritea-rule-kmdf"></a>MdlAfterReqCompletedWriteA ルール (kmdf)


**MdlAfterReqCompletedWriteA**ルールは、 [*Evtiowrite*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfio/nc-wdfio-evt_wdf_io_queue_io_write)コールバック関数内で、i/o 要求の完了後に取得されたメモリ記述子リスト (MDL) オブジェクトにアクセスできないことを指定します。

デバイスの i/o キューのドライバーの*Evtiowrite*コールバック関数内では、WdfRequestRetrieveInputWdmMdl メソッドの呼び出しによって取得された要求バッファーに、 [**Wdfrequestcomplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestcomplete)、 [**wdfrequestcompletewithinformation**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestcompletewithinformation)、または[**wdfrequestcompletewith**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestcompletewithpriorityboost)を呼び出した後にアクセスすることはできません。 [**WdfRequestRetrieveInputWdmMdl**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestretrieveinputwdmmdl)

この規則では、次の MDL アクセス機能について検討します。

[**WDF \_メモリ \_ 記述子 \_ 初期化 \_ MDL**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfmemory/nf-wdfmemory-wdf_memory_descriptor_init_mdl) 
 [**MmGetMdlByteCount**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-mmgetmdlbytecount) 
 [**MmGetSystemAddressForMdlSafe**](https://docs.microsoft.com/windows-hardware/drivers/kernel/mm-bad-pointer) 
 [**mmgetmdlvirtualaddress**](https://docs.microsoft.com/windows-hardware/drivers/kernel/mm-bad-pointer) 
 [**iobuildpartialmdl**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iobuildpartialmdl) (1 番目と2番目のパラメーター) [**keflushiobuffers**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-keflushiobuffers) 
 [**MmGetMdlPfnArray**](https://docs.microsoft.com/windows-hardware/drivers/kernel/mm-bad-pointer) 
 [**mmgetmdlvirtualaddress**](https://docs.microsoft.com/windows-hardware/drivers/kernel/mm-bad-pointer) 
 [**mm mdlfor再利用**](https://docs.microsoft.com/windows-hardware/drivers/kernel/mm-bad-pointer) 
 [**wdfdmatransactioninitialize**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdmatransaction/nf-wdfdmatransaction-wdfdmatransactioninitialize)

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
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/static-driver-verifier" data-raw-source="[Static Driver Verifier](https://docs.microsoft.com/windows-hardware/drivers/devtest/static-driver-verifier)">静的ドライバー検証ツール</a>を実行し、 <strong>MdlAfterReqCompletedWriteA</strong>規則を指定します。</p>
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

[**WDF \_メモリ \_ 記述子 \_ 初期化 \_ MDL**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfmemory/nf-wdfmemory-wdf_memory_descriptor_init_mdl) 
 [**wdfdmatransactioninitialize**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdmatransaction/nf-wdfdmatransaction-wdfdmatransactioninitialize)wdfrequestcomplete を完了しました。これには、wdfrequestWdfRequestRetrieveInputWdmMdl を使用して、 
 [**WdfRequestComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestcomplete) 
 [**WdfRequestCompleteWithInformation**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestcompletewithinformation) 
 [**wdfrequestcompleteを**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestcompletewithpriorityboost)完了します。 
 [**WdfRequestRetrieveInputWdmMdl**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestretrieveinputwdmmdl) 
 [**IoBuildPartialMdl**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iobuildpartialmdl) 
 [**KeFlushIoBuffers**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-keflushiobuffers) 
 [**MmGetMdlByteCount**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-mmgetmdlbytecount) 
 [**mmgetmdlbyteoffset**](https://docs.microsoft.com/windows-hardware/drivers/kernel/mm-bad-pointer) 
 [**MmGetMdlPfnArray**](https://docs.microsoft.com/windows-hardware/drivers/kernel/mm-bad-pointer) 
 [**mmgetmdlbyteoffset**](https://docs.microsoft.com/windows-hardware/drivers/kernel/mm-bad-pointer) 
 [**MmGetSystemAddressForMdlSafe**](https://docs.microsoft.com/windows-hardware/drivers/kernel/mm-bad-pointer) 
 [**mmgetmdlbyteoffset 利用**](https://docs.microsoft.com/windows-hardware/drivers/kernel/mm-bad-pointer)









---
title: MdlAfterReqCompletedIoctl ルール (kmdf)
description: MdlAfterReqCompletedIoctl ルールでは、EvtIoDeviceControl コールバック関数内で、i/o 要求の完了後にメモリ記述子リスト (MDL) にアクセスできないことを指定します。
ms.assetid: ce82cca4-f0e3-4e84-8599-4094fa1ed4c2
ms.date: 05/21/2018
keywords:
- MdlAfterReqCompletedIoctl ルール (kmdf)
topic_type:
- apiref
api_name:
- MdlAfterReqCompletedIoctl
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 535e8c8ce1ebba8f0a6534a054367a580f261b44
ms.sourcegitcommit: 82a9be3b3584f991e5121f8f46a972e04185fa52
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/02/2020
ms.locfileid: "85918178"
---
# <a name="mdlafterreqcompletedioctl-rule-kmdf"></a>MdlAfterReqCompletedIoctl ルール (kmdf)


**MdlAfterReqCompletedIoctl**ルールでは、 [*Evtiodevicecontrol*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfio/nc-wdfio-evt_wdf_io_queue_io_device_control)コールバック関数内で、i/o 要求の完了後にメモリ記述子リスト (MDL) にアクセスできないことを指定します。

ドライバーの[*Evtiodevicecontrol*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfio/nc-wdfio-evt_wdf_io_queue_io_device_control)コールバック関数内で、 [**WdfRequestRetrieveInputWdmMdl**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestretrieveinputwdmmdl)または[**WdfRequestRetrieveOutputWdmMdl**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestretrieveoutputwdmmdl)メソッドを呼び出して取得した MDL は、 [**wdfrequestcomplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestcomplete)、 [**Wdfrequestcompletewithinformation**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestcompletewithinformation)、または[**wdfrequestcompletewith**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestcompletewithpriorityboost)を呼び出した後に、i/o 要求でアクセスできません。

このルールでは、次の MDL アクセス関数について見ていきます。

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
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/static-driver-verifier" data-raw-source="[Static Driver Verifier](https://docs.microsoft.com/windows-hardware/drivers/devtest/static-driver-verifier)">静的ドライバー検証ツール</a>を実行し、 <strong>MdlAfterReqCompletedIoctl</strong>規則を指定します。</p>
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

[**Wdfrequestcomplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestcomplete) 
[**Wdfrequestcompletewithinformation**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestcompletewithinformation) 
[**Wdfrequestcompletewith優先順位ブースト**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestcompletewithpriorityboost) 
[**WdfRequestRetrieveInputWdmMdl**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestretrieveinputwdmmdl) 
[**WdfRequestRetrieveOutputWdmMdl**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestretrieveoutputwdmmdl)









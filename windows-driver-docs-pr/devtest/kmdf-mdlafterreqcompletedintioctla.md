---
title: MdlAfterReqCompletedIntIoctlA ルール (kmdf)
description: MdlAfterReqCompletedIntIoctlA ルールでは、EvtIoInternalDeviceControl コールバック関数内でメモリの記述子のリスト (MDL) にアクセスできないこと、I/O 要求が完了した後を指定します。
ms.assetid: 34f3122d-ef9e-4080-8716-5e195ab934ae
ms.date: 05/21/2018
keywords:
- MdlAfterReqCompletedIntIoctlA ルール (kmdf)
topic_type:
- apiref
api_name:
- MdlAfterReqCompletedIntIoctlA
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: f2a29def3387dd0777141846077e5d919df1944c
ms.sourcegitcommit: f663c383886d87ea762e419963ff427500cc5042
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67393226"
---
# <a name="mdlafterreqcompletedintioctla-rule-kmdf"></a>MdlAfterReqCompletedIntIoctlA ルール (kmdf)


**MdlAfterReqCompletedIntIoctlA**ルールでは、ことを指定します、 [ *EvtIoInternalDeviceControl* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfio/nc-wdfio-evt_wdf_io_queue_io_internal_device_control)コールバック関数では、メモリの記述子のリスト (MDL) がすることはできませんI/O 要求が完了した後にアクセスします。

ドライバーの内*EvtIoInternalDeviceControl*コールバック関数を呼び出すことによって取得された MDL、 [ **WdfRequestRetrieveInputWdmMdl** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nf-wdfrequest-wdfrequestretrieveinputwdmmdl)または[ **WdfRequestRetrieveOutputWdmMdl** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nf-wdfrequest-wdfrequestretrieveoutputwdmmdl)メソッドを呼び出した後にアクセスできない[ **WdfRequestComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nf-wdfrequest-wdfrequestcomplete)、 [**WdfRequestCompleteWithInformation**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nf-wdfrequest-wdfrequestcompletewithinformation)、または[ **WdfRequestCompleteWithPriorityBoost** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nf-wdfrequest-wdfrequestcompletewithpriorityboost) I/O 要求。

このルールでは、次の MDL アクセス関数と見なされます。

[**WDF\_メモリ\_記述子\_INIT\_MDL**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfmemory/nf-wdfmemory-wdf_memory_descriptor_init_mdl)
[**MmGetMdlByteCount** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-mmgetmdlbytecount) 
[ **MmGetSystemAddressForMdlSafe**](https://docs.microsoft.com/windows-hardware/drivers/kernel/mm-bad-pointer)
[**MmGetMdlVirtualAddress** ](https://docs.microsoft.com/windows-hardware/drivers/kernel/mm-bad-pointer) 
 [**IoBuildPartialMdl** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iobuildpartialmdl) (最初と 2 番目のパラメーター) [ **KeFlushIoBuffers** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-keflushiobuffers) 
 [ **MmGetMdlPfnArray**](https://docs.microsoft.com/windows-hardware/drivers/kernel/mm-bad-pointer)
[**MmGetMdlByteOffset** ](https://docs.microsoft.com/windows-hardware/drivers/kernel/mm-bad-pointer) 
 [ **MmPrepareMdlForReuse**](https://docs.microsoft.com/windows-hardware/drivers/kernel/mm-bad-pointer)
[**WdfDmaTransactionInitialize**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdmatransaction/nf-wdfdmatransaction-wdfdmatransactioninitialize)

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
<td align="left"><p>実行<a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/static-driver-verifier" data-raw-source="[Static Driver Verifier](https://docs.microsoft.com/windows-hardware/drivers/devtest/static-driver-verifier)">Static Driver Verifier</a>を指定し、 <strong>MdlAfterReqCompletedIntIoctlA</strong>ルール。</p>
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

[**WDF\_メモリ\_記述子\_INIT\_MDL**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfmemory/nf-wdfmemory-wdf_memory_descriptor_init_mdl)
[**WdfDmaTransactionInitialize** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdmatransaction/nf-wdfdmatransaction-wdfdmatransactioninitialize)
 [ **WdfRequestComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nf-wdfrequest-wdfrequestcomplete)
[**WdfRequestCompleteWithInformation** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nf-wdfrequest-wdfrequestcompletewithinformation)
 [ **WdfRequestCompleteWithPriorityBoost**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nf-wdfrequest-wdfrequestcompletewithpriorityboost)
[**WdfRequestRetrieveInputWdmMdl** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nf-wdfrequest-wdfrequestretrieveinputwdmmdl)
 [ **WdfRequestRetrieveOutputWdmMdl**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nf-wdfrequest-wdfrequestretrieveoutputwdmmdl)
[**IoBuildPartialMdl** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iobuildpartialmdl) 
[ **KeFlushIoBuffers**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-keflushiobuffers)
[**MmGetMdlByteCount** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-mmgetmdlbytecount) 
 [ **MmGetMdlByteOffset**](https://docs.microsoft.com/windows-hardware/drivers/kernel/mm-bad-pointer)
[**MmGetMdlPfnArray** ](https://docs.microsoft.com/windows-hardware/drivers/kernel/mm-bad-pointer) 
[ **MmGetMdlVirtualAddress**](https://docs.microsoft.com/windows-hardware/drivers/kernel/mm-bad-pointer)
[**MmGetSystemAddressForMdlSafe** ](https://docs.microsoft.com/windows-hardware/drivers/kernel/mm-bad-pointer) 
 [ **MmPrepareMdlForReuse**](https://docs.microsoft.com/windows-hardware/drivers/kernel/mm-bad-pointer)









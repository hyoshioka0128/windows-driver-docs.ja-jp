---
title: BufAfterReqCompletedIntIoctlA ルール (kmdf)
description: BufAfterReqCompletedIntIoctlA ルールは、要求が完了すると、そのバッファーにアクセスできないこと (内 EvtIoInternalDeviceControl コールバックのみ) を確認します。
ms.assetid: 3635DB6D-00C7-44DD-B05A-7EAA16B18937
ms.date: 05/21/2018
keywords:
- BufAfterReqCompletedIntIoctlA ルール (kmdf)
topic_type:
- apiref
api_name:
- BufAfterReqCompletedIntIoctlA
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 91030846a810b96b2847cea1c7f83ae396dbe90b
ms.sourcegitcommit: f663c383886d87ea762e419963ff427500cc5042
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67391735"
---
# <a name="bufafterreqcompletedintioctla-rule-kmdf"></a>BufAfterReqCompletedIntIoctlA ルール (kmdf)


**BufAfterReqCompletedIntIoctlA**ルールは、要求が完了した後、バッファーにアクセスできないことを確認します (内部[ *EvtIoInternalDeviceControl* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfio/nc-wdfio-evt_wdf_io_queue_io_internal_device_control)コールバックのみ)。 バッファーが呼び出すことによって取得された[ **WdfRequestRetrieveInputBuffer** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nf-wdfrequest-wdfrequestretrieveinputbuffer)または[ **WdfRequestRetrieveOutputBuffer** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nf-wdfrequest-wdfrequestretrieveoutputbuffer)または[ **WdfRequestRetrieveUnsafeUserInputBuffer** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nf-wdfrequest-wdfrequestretrieveunsafeuserinputbuffer)または[ **WdfRequestRetrieveUnsafeUserOutputBuffer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nf-wdfrequest-wdfrequestretrieveunsafeuseroutputbuffer)します。

内で、 [ *EvtIoInternalDeviceControl* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfio/nc-wdfio-evt_wdf_io_queue_io_internal_device_control) I/O キュー イベントのコールバック関数を呼び出すことによって取得要求のバッファー [ **WdfRequestRetrieveInputBuffer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nf-wdfrequest-wdfrequestretrieveinputbuffer)または[ **WdfRequestRetrieveOutputBuffer** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nf-wdfrequest-wdfrequestretrieveoutputbuffer)または[ **WdfRequestRetrieveUnsafeUserInputBuffer** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nf-wdfrequest-wdfrequestretrieveunsafeuserinputbuffer)または[ **WdfRequestRetrieveUnsafeUserOutputBuffer** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nf-wdfrequest-wdfrequestretrieveunsafeuseroutputbuffer)後にアクセスすることはできません、 [ **WdfRequestComplete** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nf-wdfrequest-wdfrequestcomplete)、 [ **WdfRequestCompleteWithInformation**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nf-wdfrequest-wdfrequestcompletewithinformation)、または[ **WdfRequestCompleteWithPriorityBoost** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nf-wdfrequest-wdfrequestcompletewithpriorityboost)メソッドが要求で呼び出されました。 次のバッファーへのアクセス機能が考えられます。[**RtlMoveMemory** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-rtlmovememory) (、バッファーと、翌月 1 日と 2 番目のパラメーターとして)、 [ **RtlZeroMemory**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-rtlzeromemory)、 [ **RtlCompareMemory** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-rtlcomparememory)、 [ **ZwReadFile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-ntreadfile)、 [ **ZwWriteFile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-ntwritefile)、 [ **WDF\_メモリ\_記述子\_INIT\_バッファー**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfmemory/nf-wdfmemory-wdf_memory_descriptor_init_buffer)、 [ **WdfMemoryCreatePreallocated**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfmemory/nf-wdfmemory-wdfmemorycreatepreallocated)、 [ **WdfMemoryAssignBuffer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfmemory/nf-wdfmemory-wdfmemoryassignbuffer)、 [ **WdfMemoryCopyFromBuffer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfmemory/nf-wdfmemory-wdfmemorycopyfrombuffer)、 [ **WdfMemoryCopyToBuffer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfmemory/nf-wdfmemory-wdfmemorycopytobuffer)します。

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
<td align="left"><p>実行<a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/static-driver-verifier" data-raw-source="[Static Driver Verifier](https://docs.microsoft.com/windows-hardware/drivers/devtest/static-driver-verifier)">Static Driver Verifier</a>を指定し、 <strong>BufAfterReqCompletedIntIoctlA</strong>ルール。</p>
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

<a name="applies-to"></a>対象
----------

[**WDF\_メモリ\_記述子\_INIT\_バッファー**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfmemory/nf-wdfmemory-wdf_memory_descriptor_init_buffer)
[**WdfMemoryAssignBuffer** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfmemory/nf-wdfmemory-wdfmemoryassignbuffer)
 [ **WdfMemoryCopyFromBuffer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfmemory/nf-wdfmemory-wdfmemorycopyfrombuffer)
[**WdfMemoryCopyToBuffer** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfmemory/nf-wdfmemory-wdfmemorycopytobuffer) 
 [ **WdfMemoryCreatePreallocated**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfmemory/nf-wdfmemory-wdfmemorycreatepreallocated)
[**WdfRequestComplete** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nf-wdfrequest-wdfrequestcomplete) 
[ **WdfRequestCompleteWithInformation**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nf-wdfrequest-wdfrequestcompletewithinformation)
[**WdfRequestCompleteWithPriorityBoost** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nf-wdfrequest-wdfrequestcompletewithpriorityboost)
 [ **WdfRequestRetrieveInputBuffer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nf-wdfrequest-wdfrequestretrieveinputbuffer)
[**WdfRequestRetrieveOutputBuffer** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nf-wdfrequest-wdfrequestretrieveoutputbuffer) 
 [ **WdfRequestRetrieveUnsafeUserInputBuffer** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nf-wdfrequest-wdfrequestretrieveunsafeuserinputbuffer) 
 [ **WdfRequestRetrieveUnsafeUserOutputBuffer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nf-wdfrequest-wdfrequestretrieveunsafeuseroutputbuffer)
[**RtlCompareMemory** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-rtlcomparememory) 
 [**RtlMoveMemory**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-rtlmovememory)
[**RtlZeroMemory** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-rtlzeromemory) 
 [ **ZwReadFile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-ntreadfile)
 

 






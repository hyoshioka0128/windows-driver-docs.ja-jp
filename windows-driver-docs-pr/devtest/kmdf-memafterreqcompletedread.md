---
title: MemAfterReqCompletedRead ルール (kmdf)
description: MemAfterReqCompletedRead ルールでは、EvtIoRead コールバック関数内で、i/o 要求の完了後にフレームワークメモリオブジェクトにアクセスできないことを指定します。
ms.assetid: 0c19b9e3-5968-4d93-9449-96e8a93fffde
ms.date: 05/21/2018
keywords:
- MemAfterReqCompletedRead ルール (kmdf)
topic_type:
- apiref
api_name:
- MemAfterReqCompletedRead
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 4270bb786c99eb712cd54e7d3db3d43fc91f5c1a
ms.sourcegitcommit: 82a9be3b3584f991e5121f8f46a972e04185fa52
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/02/2020
ms.locfileid: "85918158"
---
# <a name="memafterreqcompletedread-rule-kmdf"></a>MemAfterReqCompletedRead ルール (kmdf)


**MemAfterReqCompletedRead**ルールでは、 [*EvtIoRead*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfio/nc-wdfio-evt_wdf_io_queue_io_read)コールバック関数内で、i/o 要求の完了後にフレームワークメモリオブジェクトにアクセスできないことを指定します。

ドライバーの[*EvtIoRead*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfio/nc-wdfio-evt_wdf_io_queue_io_read) callback 関数内では、 [**WdfRequestRetrieveOutputMemory**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestretrieveoutputmemory)メソッドの呼び出しによって取得されたフレームワークメモリオブジェクトは、 [**wdfrequestcomplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestcomplete)、 [**wdfrequestcompletewithinformation**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestcompletewithinformation)、または[**wdfrequestcompletewith**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestcompletewithpriorityboost)を呼び出した後に、i/o 要求に対してアクセスすることはできません。

この規則では、次の2つのメモリアクセス方法を考慮します。

[**WdfRequestRetrieveInputMemory**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestretrieveinputmemory) 
[ **WdfRequestRetrieveOutputMemory**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestretrieveoutputmemory)

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
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/static-driver-verifier" data-raw-source="[Static Driver Verifier](https://docs.microsoft.com/windows-hardware/drivers/devtest/static-driver-verifier)">静的ドライバー検証ツール</a>を実行し、 <strong>MemAfterReqCompletedRead</strong>規則を指定します。</p>
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
[**WdfRequestRetrieveInputMemory**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestretrieveinputmemory) 
[**WdfRequestRetrieveOutputMemory**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestretrieveoutputmemory)









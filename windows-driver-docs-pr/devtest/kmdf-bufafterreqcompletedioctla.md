---
title: BufAfterReqCompletedIoctlA ルール (kmdf)
description: BufAfterReqCompletedIoctlA ルールでは、EvtIoDeviceControl コールバック関数内で取得される I/O 要求のバッファーにアクセスできないこと、I/O 要求が完了した後を指定します。
ms.assetid: c81f80b0-290e-41f1-b7df-9f6528261366
ms.date: 05/21/2018
keywords:
- BufAfterReqCompletedIoctlA ルール (kmdf)
topic_type:
- apiref
api_name:
- BufAfterReqCompletedIoctlA
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 57f1587ff917b01a4d52332e11cd92bda5cacaec
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63340414"
---
# <a name="bufafterreqcompletedioctla-rule-kmdf"></a>BufAfterReqCompletedIoctlA ルール (kmdf)


**BufAfterReqCompletedIoctlA**ルールでは、ことを指定します、 [ *EvtIoDeviceControl* ](https://msdn.microsoft.com/library/windows/hardware/ff541758)コールバック関数、取得される I/O 要求のバッファーにアクセスできませんI/O 要求が完了するとします。

ドライバーの内**EvtIoDeviceControl**コールバック関数を呼び出すことによって取得された要求バッファー [ **WdfRequestRetrieveInputBuffer**](https://msdn.microsoft.com/library/windows/hardware/ff550014)、 [ **WdfRequestRetrieveOutputBuffer**](https://msdn.microsoft.com/library/windows/hardware/ff550018)、 [ **WdfRequestRetrieveUnsafeUserInputBuffer**](https://msdn.microsoft.com/library/windows/hardware/ff550022)、または[ **WdfRequestRetrieveUnsafeUserOutputBuffer** ](https://msdn.microsoft.com/library/windows/hardware/ff550024)呼び出した後にアクセスできません[ **WdfRequestComplete**](https://msdn.microsoft.com/library/windows/hardware/ff549945)、 [ **WdfRequestCompleteWithInformation**](https://msdn.microsoft.com/library/windows/hardware/ff549948)、または[ **WdfRequestCompleteWithPriorityBoost** ](https://msdn.microsoft.com/library/windows/hardware/ff549949) I/O 要求。

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
<td align="left"><p>実行<a href="https://msdn.microsoft.com/library/windows/hardware/ff552808" data-raw-source="[Static Driver Verifier](https://msdn.microsoft.com/library/windows/hardware/ff552808)">Static Driver Verifier</a>を指定し、 <strong>BufAfterReqCompletedIoctlA</strong>ルール。</p>
コードの分析を実行するには、次の手順に従います。
<ol>
<li><a href="https://msdn.microsoft.com/library/windows/hardware/hh454281#preparing-your-source-code" data-raw-source="[Prepare your code (use role type declarations).](https://msdn.microsoft.com/library/windows/hardware/hh454281#preparing-your-source-code)">(ロールの型宣言の使用)、コードを準備します。</a></li>
<li><a href="https://msdn.microsoft.com/library/windows/hardware/hh454281#running-static-driver-verifier" data-raw-source="[Run Static Driver Verifier.](https://msdn.microsoft.com/library/windows/hardware/hh454281#running-static-driver-verifier)">Static Driver Verifier を実行します。</a></li>
<li><a href="https://msdn.microsoft.com/library/windows/hardware/hh454281#viewing-and-analyzing-the-results" data-raw-source="[View and analyze the results.](https://msdn.microsoft.com/library/windows/hardware/hh454281#viewing-and-analyzing-the-results)">表示し、結果を分析します。</a></li>
</ol>
<p>詳細については、次を参照してください。<a href="https://msdn.microsoft.com/library/windows/hardware/hh454281" data-raw-source="[Using Static Driver Verifier to Find Defects in Drivers](https://msdn.microsoft.com/library/windows/hardware/hh454281)">ドライバーで障害を検出する Static Driver Verifier を使用して</a>します。</p></td>
</tr>
</tbody>
</table>

<a name="applies-to"></a>対象
----------

[**WDF\_メモリ\_記述子\_INIT\_バッファー**](https://msdn.microsoft.com/library/windows/hardware/ff552393)
[**WdfMemoryAssignBuffer** ](https://msdn.microsoft.com/library/windows/hardware/ff548697)
 [ **WdfMemoryCopyFromBuffer**](https://msdn.microsoft.com/library/windows/hardware/ff548701)
[**WdfMemoryCopyToBuffer** ](https://msdn.microsoft.com/library/windows/hardware/ff548703) 
 [ **WdfMemoryCreatePreallocated**](https://msdn.microsoft.com/library/windows/hardware/ff548712)
[**WdfRequestComplete** ](https://msdn.microsoft.com/library/windows/hardware/ff549945) 
[ **WdfRequestCompleteWithInformation**](https://msdn.microsoft.com/library/windows/hardware/ff549948)
[**WdfRequestCompleteWithPriorityBoost** ](https://msdn.microsoft.com/library/windows/hardware/ff549949)
 [ **WdfRequestRetrieveInputBuffer**](https://msdn.microsoft.com/library/windows/hardware/ff550014)
[**WdfRequestRetrieveOutputBuffer** ](https://msdn.microsoft.com/library/windows/hardware/ff550018) 
 [ **WdfRequestRetrieveUnsafeUserInputBuffer** ](https://msdn.microsoft.com/library/windows/hardware/ff550022) 
 [ **WdfRequestRetrieveUnsafeUserOutputBuffer**](https://msdn.microsoft.com/library/windows/hardware/ff550024)
[**RtlCompareMemory** ](https://msdn.microsoft.com/library/windows/hardware/ff561778) 
 [**RtlMoveMemory**](https://msdn.microsoft.com/library/windows/hardware/ff562030)
[**RtlZeroMemory** ](https://msdn.microsoft.com/library/windows/hardware/ff563610) 
 [ **ZwReadFile** ](https://msdn.microsoft.com/library/windows/hardware/ff567072)も参照してください
--------

[**BufAfterReqCompletedIoctl**](kmdf-bufafterreqcompletedioctl.md)
 

 






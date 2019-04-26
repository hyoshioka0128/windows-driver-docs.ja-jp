---
title: BufAfterReqCompletedIntIoctl rule (kmdf)
description: BufAfterReqCompletedIntIoctl ルールでは、要求が完了すると、そのバッファーにアクセスできないこと (内 EvtIoInternalDeviceControl コールバック関数のみ) を指定します。
ms.assetid: 6632262F-8163-4B4C-9B07-BCBD7CDA6E33
ms.date: 05/21/2018
keywords:
- BufAfterReqCompletedIntIoctl rule (kmdf)
topic_type:
- apiref
api_name:
- BufAfterReqCompletedIntIoctl
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 415c9fba991f6b732a177ef1ff5f2932330ff290
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63340442"
---
# <a name="bufafterreqcompletedintioctl-rule-kmdf"></a>BufAfterReqCompletedIntIoctl rule (kmdf)


**BufAfterReqCompletedIntIoctl**ルールでは、要求が完了すると、そのバッファーにアクセスできないことを指定します (内部[ *EvtIoInternalDeviceControl* ](https://msdn.microsoft.com/library/windows/hardware/ff541768)コールバック関数の場合のみ)。 バッファーが呼び出すことによって取得[ **WdfRequestRetrieveOutputBuffer** ](https://msdn.microsoft.com/library/windows/hardware/ff550018)または[ **WdfRequestRetrieveUnsafeUserOutputBuffer** ](https://msdn.microsoft.com/library/windows/hardware/ff550024)または[ **WdfRequestRetrieveInputBuffer** ](https://msdn.microsoft.com/library/windows/hardware/ff550014)または[ **WdfRequestRetrieveUnsafeUserInputBuffer**](https://msdn.microsoft.com/library/windows/hardware/ff550022)します。

内で、 [ *EvtIoInternalDeviceControl* ](https://msdn.microsoft.com/library/windows/hardware/ff541768) I/O キュー イベントのコールバック関数を呼び出すことによって取得要求のバッファー [ **WdfRequestRetrieveInputBuffer**](https://msdn.microsoft.com/library/windows/hardware/ff550014)、 [ **WdfRequestRetrieveOutputBuffer**](https://msdn.microsoft.com/library/windows/hardware/ff550018)、 [ **WdfRequestRetrieveUnsafeUserInputBuffer**](https://msdn.microsoft.com/library/windows/hardware/ff550022)、または[ **WdfRequestRetrieveUnsafeUserOutputBuffer** ](https://msdn.microsoft.com/library/windows/hardware/ff550024)要求が完了した後にアクセスすることはできません。 呼び出すことによって、要求が完了した[ **WdfRequestComplete**](https://msdn.microsoft.com/library/windows/hardware/ff549945)、 [ **WdfRequestCompleteWithInformation**](https://msdn.microsoft.com/library/windows/hardware/ff549948)、または**WdfRequestComplete**、 [ **WdfRequestCompleteWithPriorityBoost**](https://msdn.microsoft.com/library/windows/hardware/ff549949)します。 次のバッファーへのアクセス機能が考えられます。**WdfRequestRetrieveOutputBuffer**、 **WdfRequestRetrieveUnsafeUserOutputBuffer**、 **WdfRequestRetrieveInputBuffer**と**WdfRequestRetrieveUnsafeUserInputBuffer**します。

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
<td align="left"><p>実行<a href="https://msdn.microsoft.com/library/windows/hardware/ff552808" data-raw-source="[Static Driver Verifier](https://msdn.microsoft.com/library/windows/hardware/ff552808)">Static Driver Verifier</a>を指定し、 <strong>BufAfterReqCompletedIntIoctl</strong>ルール。</p>
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

<a name="applies-to"></a>適用対象
----------

[**WdfRequestComplete**](https://msdn.microsoft.com/library/windows/hardware/ff549945)
[**WdfRequestCompleteWithInformation** ](https://msdn.microsoft.com/library/windows/hardware/ff549948) 
 [ **WdfRequestCompleteWithPriorityBoost**](https://msdn.microsoft.com/library/windows/hardware/ff549949)
[**WdfRequestRetrieveInputBuffer** ](https://msdn.microsoft.com/library/windows/hardware/ff550014) 
 [ **WdfRequestRetrieveOutputBuffer**](https://msdn.microsoft.com/library/windows/hardware/ff550018)
[**WdfRequestRetrieveUnsafeUserInputBuffer** ](https://msdn.microsoft.com/library/windows/hardware/ff550022) 
 [**WdfRequestRetrieveUnsafeUserOutputBuffer**](https://msdn.microsoft.com/library/windows/hardware/ff550024)
 

 






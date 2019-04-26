---
title: BufAfterReqCompletedWrite ルール (kmdf)
description: BufAfterReqCompletedWrite ルールでは、EvtIoWrite コールバック関数内で取得される I/O 要求のバッファーにアクセスできないこと、I/O 要求が完了した後を指定します。
ms.assetid: fc41d125-1b76-4645-9b89-bf6cea2e04b2
ms.date: 05/21/2018
keywords:
- BufAfterReqCompletedWrite ルール (kmdf)
topic_type:
- apiref
api_name:
- BufAfterReqCompletedWrite
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 84e9164e81e8ff3bcd2097251b2b421cc4c034c0
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63340422"
---
# <a name="bufafterreqcompletedwrite-rule-kmdf"></a>BufAfterReqCompletedWrite ルール (kmdf)


BufAfterReqCompletedWrite ルールでは、ことを指定します、 [ *EvtIoWrite* ](https://msdn.microsoft.com/library/windows/hardware/ff541813) I/O 要求が完了した後、コールバック関数、取得される I/O 要求のバッファーにアクセスできません。

ドライバーの内**EvtIoWrite**コールバック関数を呼び出すことによって取得された要求バッファー [ **WdfRequestRetrieveInputBuffer** ](https://msdn.microsoft.com/library/windows/hardware/ff550014)または[ **WdfRequestRetrieveUnsafeUserInputBuffer** ](https://msdn.microsoft.com/library/windows/hardware/ff550022)呼び出した後にアクセスできません[ **WdfRequestComplete**](https://msdn.microsoft.com/library/windows/hardware/ff549945)、 [ **WdfRequestCompleteWithInformation**](https://msdn.microsoft.com/library/windows/hardware/ff549948)、または[ **WdfRequestCompleteWithPriorityBoost** ](https://msdn.microsoft.com/library/windows/hardware/ff549949) I/O 要求。

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
<td align="left"><p>実行<a href="https://msdn.microsoft.com/library/windows/hardware/ff552808" data-raw-source="[Static Driver Verifier](https://msdn.microsoft.com/library/windows/hardware/ff552808)">Static Driver Verifier</a>を指定し、 <strong>BufAfterReqCompletedWrite</strong>ルール。</p>
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
 

 






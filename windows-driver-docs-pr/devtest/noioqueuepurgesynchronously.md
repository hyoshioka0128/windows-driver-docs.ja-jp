---
title: NoIoQueuePurgeSynchronously ルール (kmdf)
ms.assetid: 9255C644-1141-4D9A-8B84-BF98FB9E262A
ms.date: 05/21/2018
description: ''
keywords:
- NoIoQueuePurgeSynchronously ルール (kmdf)
topic_type:
- apiref
api_name:
- NoIoQueuePurgeSynchronously
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: ce60382513796f59cd722077d1aee635c273d97b
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63374647"
---
# <a name="noioqueuepurgesynchronously-rule-kmdf"></a>NoIoQueuePurgeSynchronously ルール (kmdf)


**NoIoQueuePurgeSynchronously**ルールでは、WDF のドライバーを呼び出さないことを検証、 [ **WdfIoQueueStopSynchronously**](https://msdn.microsoft.com/library/windows/hardware/ff548489)、 [ **WdfIoQueueDrainSynchronously**](https://msdn.microsoft.com/library/windows/hardware/ff547412)、 [ **WdfIoQueueStopAndPurgeSynchronously**](https://msdn.microsoft.com/library/windows/hardware/hh439293)、または[ **WdfIoQueuePurgeSynchronously** ](https://msdn.microsoft.com/library/windows/hardware/ff548449)次 EvtIO から functions におけるキュー オブジェクト イベントのコールバック関数。

[*EvtIoDefault*](https://msdn.microsoft.com/library/windows/hardware/ff541757)
[*EvtIoDeviceControl*](https://msdn.microsoft.com/library/windows/hardware/ff541758)
[*EvtIoInternalDeviceControl* ](https://msdn.microsoft.com/library/windows/hardware/ff541768) 
 [ *EvtIoRead*](https://msdn.microsoft.com/library/windows/hardware/ff541776)
[*EvtIoWrite*](https://msdn.microsoft.com/library/windows/hardware/ff541813)

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
<td align="left"><p>実行<a href="https://msdn.microsoft.com/library/windows/hardware/ff552808" data-raw-source="[Static Driver Verifier](https://msdn.microsoft.com/library/windows/hardware/ff552808)">Static Driver Verifier</a>を指定し、 <strong>NoIoQueuePurgeSynchronously</strong>ルール。</p>
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

[**WdfRequestCancelSentRequest**](https://msdn.microsoft.com/library/windows/hardware/ff549941)
[**WdfRequestComplete** ](https://msdn.microsoft.com/library/windows/hardware/ff549945) 
 [ **WdfRequestCompleteWithInformation**](https://msdn.microsoft.com/library/windows/hardware/ff549948)
[**WdfRequestCompleteWithPriorityBoost** ](https://msdn.microsoft.com/library/windows/hardware/ff549949) 
 [**WdfRequestMarkCancelable**](https://msdn.microsoft.com/library/windows/hardware/ff549983)
[**WdfRequestMarkCancelableEx** ](https://msdn.microsoft.com/library/windows/hardware/ff549984) 
 [ **WdfRequestStopAcknowledge**](https://msdn.microsoft.com/library/windows/hardware/ff550033)
[**WdfRequestUnmarkCancelable**](https://msdn.microsoft.com/library/windows/hardware/ff550035)









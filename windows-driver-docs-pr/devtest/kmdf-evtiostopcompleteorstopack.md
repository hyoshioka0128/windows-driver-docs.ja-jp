---
title: EvtIoStopCompleteOrStopAck ルール (kmdf)
description: EvtIoStopCompleteOrStopAck ルールでは、こと EvtIoStop コールバック内で関数が、ドライバー、フレームワークによって表示される I/O 要求ごとに、次のメソッドのいずれかを指定します。
ms.assetid: d534a08e-4bee-4ec6-ac6b-03a6454fb60f
ms.date: 05/21/2018
keywords:
- EvtIoStopCompleteOrStopAck ルール (kmdf)
topic_type:
- apiref
api_name:
- EvtIoStopCompleteOrStopAck
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 97c62d6a0b2f7408d62c4a8aae8f74884e4814f8
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56530220"
---
# <a name="evtiostopcompleteorstopack-rule-kmdf"></a>EvtIoStopCompleteOrStopAck ルール (kmdf)


**EvtIoStopCompleteOrStopAck**ルールでは、ことを指定します、 [ *EvtIoStop* ](https://msdn.microsoft.com/library/windows/hardware/ff541788) I/O 要求ごとに次のいずれかのドライバーのコールバック関数を呼び出すフレームワークによって表示されます。 これを行わないと、ドライバーは別の低電力状態に入るをシステムをブロックする可能性があります。

[**WdfRequestComplete**](https://msdn.microsoft.com/library/windows/hardware/ff549945)
[**WdfRequestCompleteWithInformation** ](https://msdn.microsoft.com/library/windows/hardware/ff549948) 
 [ **WdfRequestCompleteWithPriorityBoost**](https://msdn.microsoft.com/library/windows/hardware/ff549949)
[**WdfRequestCancelSentRequest** ](https://msdn.microsoft.com/library/windows/hardware/ff549941) 
 [ **WdfRequestStopAcknowledge**](https://msdn.microsoft.com/library/windows/hardware/ff550033)

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
<td align="left"><p>実行<a href="https://msdn.microsoft.com/library/windows/hardware/ff552808" data-raw-source="[Static Driver Verifier](https://msdn.microsoft.com/library/windows/hardware/ff552808)">Static Driver Verifier</a>を指定し、 <strong>EvtIoStopCompleteOrStopAck</strong>ルール。</p>
コードの分析を実行するには、次の手順に従います。
<ol>
<li><a href="https://msdn.microsoft.com/library/windows/hardware/hh454281#preparing-your-source-code" data-raw-source="[Prepare your code (use role type declarations).](https://msdn.microsoft.com/library/windows/hardware/hh454281#preparing-your-source-code)">(ロールの型宣言の使用)、コードを準備します。</a></li>
<li><a href="https://msdn.microsoft.com/library/windows/hardware/hh454281#running-static-driver-verifier" data-raw-source="[Run Static Driver Verifier.](https://msdn.microsoft.com/library/windows/hardware/hh454281#running-static-driver-verifier)">Static Driver Verifier を実行します。</a></li>
<li><a href="https://msdn.microsoft.com/library/windows/hardware/hh454281#viewing-and-analyzing-the-results" data-raw-source="[View and analyze the results.](https://msdn.microsoft.com/library/windows/hardware/hh454281#viewing-and-analyzing-the-results)">表示し、結果を分析します。</a></li>
</ol>
<p>詳細については、<a href="https://msdn.microsoft.com/library/windows/hardware/hh454281" data-raw-source="[Using Static Driver Verifier to Find Defects in Drivers](https://msdn.microsoft.com/library/windows/hardware/hh454281)">ドライバーで障害を検出する Static Driver Verifier を使用して</a>を参照してください。</p></td>
</tr>
</tbody>
</table>

<a name="applies-to"></a>適用対象
----------

[**WdfRequestCancelSentRequest**](https://msdn.microsoft.com/library/windows/hardware/ff549941)
[**WdfRequestComplete** ](https://msdn.microsoft.com/library/windows/hardware/ff549945) 
 [ **WdfRequestCompleteWithInformation**](https://msdn.microsoft.com/library/windows/hardware/ff549948)
[**WdfRequestCompleteWithPriorityBoost** ](https://msdn.microsoft.com/library/windows/hardware/ff549949) 
 [**WdfRequestStopAcknowledge**](https://msdn.microsoft.com/library/windows/hardware/ff550033)









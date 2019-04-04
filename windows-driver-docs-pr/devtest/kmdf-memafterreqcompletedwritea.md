---
title: MemAfterReqCompletedWriteA ルール (kmdf)
description: MemAfterReqCompletedWriteA ルールでは、EvtIoWrite コールバック関数内で framework メモリ オブジェクトにアクセスできないこと、I/O 要求が完了した後を指定します。
ms.assetid: ac1d8aa5-9b33-4118-8f9a-11673d0f827c
ms.date: 05/21/2018
keywords:
- MemAfterReqCompletedWriteA ルール (kmdf)
topic_type:
- apiref
api_name:
- MemAfterReqCompletedWriteA
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: a4b8962832468ae34f8553a7278e9306e20f2f00
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56538288"
---
# <a name="memafterreqcompletedwritea-rule-kmdf"></a>MemAfterReqCompletedWriteA ルール (kmdf)


**MemAfterReqCompletedWriteA**ルールでは、ことを指定します、 [ *EvtIoWrite* ](https://msdn.microsoft.com/library/windows/hardware/ff541813)コールバック関数では、framework のメモリ オブジェクトは、I/O の後にアクセスできません要求が完了したとします。

ドライバーの内[ *EvtIoWrite* ](https://msdn.microsoft.com/library/windows/hardware/ff541813)コールバック関数を呼び出すことによって取得された framework メモリ オブジェクト、 [ **WdfRequestRetrieveInputMemory**](https://msdn.microsoft.com/library/windows/hardware/ff550015)メソッドを呼び出した後にアクセスできない[ **WdfRequestComplete**](https://msdn.microsoft.com/library/windows/hardware/ff549945)、 [ **WdfRequestCompleteWithInformation** ](https://msdn.microsoft.com/library/windows/hardware/ff549948)、または[ **WdfRequestCompleteWithPriorityBoost** ](https://msdn.microsoft.com/library/windows/hardware/ff549949) I/O 要求。

このルールは、次の 8 つのアクセス方法を考慮します。

[**WdfMemoryGetBuffer**](https://msdn.microsoft.com/library/windows/hardware/ff548715)
[**WDF\_メモリ\_記述子\_INIT\_処理**](https://msdn.microsoft.com/library/windows/hardware/ff552395) 
[ **WdfMemoryAssignBuffer**](https://msdn.microsoft.com/library/windows/hardware/ff548697)
[**WdfMemoryCopyToBuffer** ](https://msdn.microsoft.com/library/windows/hardware/ff548703) 
 [ **WdfMemoryCopyFromBuffer**](https://msdn.microsoft.com/library/windows/hardware/ff548701)
[**WdfObjectReference** ](https://msdn.microsoft.com/library/windows/hardware/ff548758) 
 [ **WdfObjectDereference**](https://msdn.microsoft.com/library/windows/hardware/ff548739)
[**WdfObjectDelete**](https://msdn.microsoft.com/library/windows/hardware/ff548734)

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
<td align="left"><p>実行<a href="https://msdn.microsoft.com/library/windows/hardware/ff552808" data-raw-source="[Static Driver Verifier](https://msdn.microsoft.com/library/windows/hardware/ff552808)">Static Driver Verifier</a>を指定し、 <strong>MemAfterReqCompletedWriteA</strong>ルール。</p>
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

[**WDF\_メモリ\_記述子\_INIT\_処理**](https://msdn.microsoft.com/library/windows/hardware/ff552395)
[**WdfMemoryAssignBuffer** ](https://msdn.microsoft.com/library/windows/hardware/ff548697)
 [ **WdfMemoryCopyFromBuffer**](https://msdn.microsoft.com/library/windows/hardware/ff548701)
[**WdfMemoryCopyToBuffer** ](https://msdn.microsoft.com/library/windows/hardware/ff548703) 
 [ **WdfMemoryGetBuffer**](https://msdn.microsoft.com/library/windows/hardware/ff548715)
[**WdfObjectDelete** ](https://msdn.microsoft.com/library/windows/hardware/ff548734) 
 [ **WdfObjectDereference**](https://msdn.microsoft.com/library/windows/hardware/ff548739)
[**WdfObjectReference** ](https://msdn.microsoft.com/library/windows/hardware/ff548758) 
 [ **WdfRequestComplete**](https://msdn.microsoft.com/library/windows/hardware/ff549945)
[**WdfRequestCompleteWithInformation** ](https://msdn.microsoft.com/library/windows/hardware/ff549948) 
 [ **WdfRequestCompleteWithPriorityBoost**](https://msdn.microsoft.com/library/windows/hardware/ff549949)
[**WdfRequestRetrieveInputMemory**](https://msdn.microsoft.com/library/windows/hardware/ff550015)









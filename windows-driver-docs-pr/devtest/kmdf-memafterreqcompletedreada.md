---
title: MemAfterReqCompletedReadA ルール (kmdf)
description: MemAfterReqCompletedReadA ルールでは、EvtIoRead コールバック関数内で framework メモリ オブジェクトにアクセスできないこと、I/O 要求が完了した後を指定します。
ms.assetid: 5853fae3-3049-43d8-8452-a1afb268004b
ms.date: 05/21/2018
keywords:
- MemAfterReqCompletedReadA ルール (kmdf)
topic_type:
- apiref
api_name:
- MemAfterReqCompletedReadA
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: ed79469dcece02aab09cf428b95f4840d601356b
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56551869"
---
# <a name="memafterreqcompletedreada-rule-kmdf"></a>MemAfterReqCompletedReadA ルール (kmdf)


**MemAfterReqCompletedReadA**ルールでは、ことを指定します、 [ *EvtIoRead* ](https://msdn.microsoft.com/library/windows/hardware/ff541776)コールバック関数では、framework のメモリ オブジェクトは、I/O 要求の後にアクセスできません完了しました。

ドライバーの内*EvtIoRead*コールバック関数を呼び出すことによって取得された framework メモリ オブジェクト、 [ **WdfRequestRetrieveOutputMemory** ](https://msdn.microsoft.com/library/windows/hardware/ff550019)メソッドことはできません呼び出した後にアクセスする[ **WdfRequestComplete**](https://msdn.microsoft.com/library/windows/hardware/ff549945)、 [ **WdfRequestCompleteWithInformation**](https://msdn.microsoft.com/library/windows/hardware/ff549948)、または[ **WdfRequestCompleteWithPriorityBoost** ](https://msdn.microsoft.com/library/windows/hardware/ff549949) I/O 要求。

このルールは、次のメモリ アクセス方法を考慮します。

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
<td align="left"><p>実行<a href="https://msdn.microsoft.com/library/windows/hardware/ff552808" data-raw-source="[Static Driver Verifier](https://msdn.microsoft.com/library/windows/hardware/ff552808)">Static Driver Verifier</a>を指定し、 <strong>MemAfterReqCompletedReadA</strong>ルール。</p>
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
[**WdfRequestRetrieveOutputMemory**](https://msdn.microsoft.com/library/windows/hardware/ff550019)









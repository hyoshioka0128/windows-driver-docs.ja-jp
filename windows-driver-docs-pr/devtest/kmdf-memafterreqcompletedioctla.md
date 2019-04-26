---
title: MemAfterReqCompletedIoctlA ルール (kmdf)
description: MemAfterReqCompletedIoctlA ルールでは、EvtIoDeviceControl コールバック関数内で framework メモリ オブジェクトにアクセスできないこと、I/O 要求が完了した後を指定します。
ms.assetid: 99ce4759-779f-44d5-a245-6cfcbecef489
ms.date: 05/21/2018
keywords:
- MemAfterReqCompletedIoctlA ルール (kmdf)
topic_type:
- apiref
api_name:
- MemAfterReqCompletedIoctlA
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: ea61995a3604c12cb266ce6ad0a5d18e87302ada
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63350369"
---
# <a name="memafterreqcompletedioctla-rule-kmdf"></a>MemAfterReqCompletedIoctlA ルール (kmdf)


**MemAfterReqCompletedIoctlA**ルールでは、ことを指定します、 [ *EvtIoDeviceControl* ](https://msdn.microsoft.com/library/windows/hardware/ff541758)コールバック関数では、framework のメモリ オブジェクトは、後にアクセスできない、I/O 要求が完了したとします。

ドライバーの内[ *EvtIoDeviceControl* ](https://msdn.microsoft.com/library/windows/hardware/ff541758)コールバック関数を呼び出すことによって取得された framework メモリ オブジェクト、 [ **WdfRequestRetrieveInputMemory**](https://msdn.microsoft.com/library/windows/hardware/ff550015)または[ **WdfRequestRetrieveOutputMemory** ](https://msdn.microsoft.com/library/windows/hardware/ff550019)メソッドを呼び出した後にアクセスできない[ **WdfRequestComplete**](https://msdn.microsoft.com/library/windows/hardware/ff549945)、 [ **WdfRequestCompleteWithInformation**](https://msdn.microsoft.com/library/windows/hardware/ff549948)、または[ **WdfRequestCompleteWithPriorityBoost** ](https://msdn.microsoft.com/library/windows/hardware/ff549949)I/O 要求。

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
<td align="left"><p>実行<a href="https://msdn.microsoft.com/library/windows/hardware/ff552808" data-raw-source="[Static Driver Verifier](https://msdn.microsoft.com/library/windows/hardware/ff552808)">Static Driver Verifier</a>を指定し、 <strong>MemAfterReqCompletedIoctlA</strong>ルール。</p>
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
[**WdfRequestRetrieveInputMemory** ](https://msdn.microsoft.com/library/windows/hardware/ff550015) 
[ **WdfRequestRetrieveOutputMemory**](https://msdn.microsoft.com/library/windows/hardware/ff550019)









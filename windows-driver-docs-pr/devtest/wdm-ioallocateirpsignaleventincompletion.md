---
title: IoAllocateIrpSignalEventInCompletion ルール
description: IoAllocateIrpSignalEventInCompletion ルールでは、ドライバーは Irp-PendingReturned フラグが設定され、完了ルーチンは、ローカルで作成された非同期 IRP の処理時に、ソース ファイルを完了ルーチンの KeSetEvent を呼び出すことを指定します。
ms.assetid: 856D9755-F400-4586-9DF8-DE9ADCCCE44A
ms.date: 05/21/2018
keywords:
- IoAllocateIrpSignalEventInCompletion ルール
topic_type:
- apiref
api_name:
- IoAllocateIrpSignalEventInCompletion
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: de5953d8f2a5bc049c65d2e1b94dc639b4d9ba30
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56574841"
---
# <a name="ioallocateirpsignaleventincompletion-rule"></a>IoAllocateIrpSignalEventInCompletion ルール


**IoAllocateIrpSignalEventInCompletion**ルールでは、ドライバーを呼び出す必要がありますを指定します[ **KeSetEvent** ](https://msdn.microsoft.com/library/windows/hardware/ff553253)完了ルーチンの場合、 **Irp-&gt;PendingReturned**フラグが設定され、ローカルで作成された非同期 IRP の処理が完了ルーチン。

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
<td align="left"><p>実行<a href="https://msdn.microsoft.com/library/windows/hardware/ff552808" data-raw-source="[Static Driver Verifier](https://msdn.microsoft.com/library/windows/hardware/ff552808)">Static Driver Verifier</a>を指定し、 <strong>IoAllocateIrpSignalEventInCompletion</strong>ルール。</p>
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

<a name="applies-to"></a>対象
----------

[**IoAllocateIrp**](https://msdn.microsoft.com/library/windows/hardware/ff548257)
[**IoBuildDeviceIoControlRequest**](https://msdn.microsoft.com/library/windows/hardware/ff548318)
[**IoSetCompletionRoutine**](https://msdn.microsoft.com/library/windows/hardware/ff549679) 
 [ **IoSetCompletionRoutineEx**](https://msdn.microsoft.com/library/windows/hardware/ff549686)
[**KeInitializeEvent** ](https://msdn.microsoft.com/library/windows/hardware/ff552137) 
 [ **KeSetEvent**](https://msdn.microsoft.com/library/windows/hardware/ff553253)
 

 






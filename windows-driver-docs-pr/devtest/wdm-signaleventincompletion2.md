---
title: SignalEventInCompletion2 ルール (wdm)
description: SignalEventInCompletion2 ルールでは、非同期の IRP を処理するときに Irp-PendingReturned フラグが設定されている場合は、完了ルーチンで、KeSetEvent を呼び出す ドライバーが必要なを指定します。
ms.assetid: 48BFBB4D-0D42-4C83-8EA8-6874F31238FC
ms.date: 05/21/2018
keywords:
- SignalEventInCompletion2 ルール (wdm)
topic_type:
- apiref
api_name:
- SignalEventInCompletion2
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 2ef8d4af15a6ca3cbf6ea51fd3851f2b6bf3fe70
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56551895"
---
# <a name="signaleventincompletion2-rule-wdm"></a>SignalEventInCompletion2 ルール (wdm)


**SignalEventInCompletion2**ルールでは、非同期の IRP を処理するときに呼び出す [ドライバーが必要なを指定します、 [ **KeSetEvent** ](https://msdn.microsoft.com/library/windows/hardware/ff553253)完了ルーチンの場合、**Irp -&gt;PendingReturned**フラグを設定します。

この場合は、完了のルーチンは呼び出されません。

|              |     |
|--------------|-----|
| ドライバー モデル | WDM |

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
<td align="left"><p>実行<a href="https://msdn.microsoft.com/library/windows/hardware/ff552808" data-raw-source="[Static Driver Verifier](https://msdn.microsoft.com/library/windows/hardware/ff552808)">Static Driver Verifier</a>を指定し、 <strong>SignalEventInCompletion2</strong>ルール。</p>
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

[**IoSetCompletionRoutine**](https://msdn.microsoft.com/library/windows/hardware/ff549679)
[**IoSetCompletionRoutineEx**](https://msdn.microsoft.com/library/windows/hardware/ff549686)
[**KeInitializeEvent**](https://msdn.microsoft.com/library/windows/hardware/ff552137)
 

 






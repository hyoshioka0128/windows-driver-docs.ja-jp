---
title: SignalEventInCompletion ルール (wdm)
description: SignalEventInCompletion ルールでは、非同期の IRP を処理するときに Irp-PendingReturned フラグが設定されている場合は、完了ルーチンで、KeSetEvent を呼び出す ドライバーが必要なを指定します。
ms.assetid: CF79EB38-82B0-4CD5-B629-8B8D84EB60CA
ms.date: 05/21/2018
keywords:
- SignalEventInCompletion ルール (wdm)
topic_type:
- apiref
api_name:
- SignalEventInCompletion
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 66f1ccb811ddfcd856c6b8d2d459ab7ab244a39a
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56549919"
---
# <a name="signaleventincompletion-rule-wdm"></a>SignalEventInCompletion ルール (wdm)


**SignalEventInCompletion**ルールでは、非同期の IRP を処理するときに呼び出す [ドライバーが必要なを指定します、 [ **KeSetEvent** ](https://msdn.microsoft.com/library/windows/hardware/ff553253)完了ルーチンの場合、**Irp -&gt;PendingReturned**フラグを設定します。

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
<td align="left"><p>実行<a href="https://msdn.microsoft.com/library/windows/hardware/ff552808" data-raw-source="[Static Driver Verifier](https://msdn.microsoft.com/library/windows/hardware/ff552808)">Static Driver Verifier</a>を指定し、 <strong>SignalEventInCompletion</strong>ルール。</p>
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

[**IoBuildDeviceIoControlRequest**](https://msdn.microsoft.com/library/windows/hardware/ff548318)
[**IoBuildSynchronousFsdRequest** ](https://msdn.microsoft.com/library/windows/hardware/ff548330) 
 [ **IoSetCompletionRoutine**](https://msdn.microsoft.com/library/windows/hardware/ff549679)
[**IoSetCompletionRoutineEx** ](https://msdn.microsoft.com/library/windows/hardware/ff549686) 
 [ **KeInitializeEvent**](https://msdn.microsoft.com/library/windows/hardware/ff552137)
[**KeSetEvent**](https://msdn.microsoft.com/library/windows/hardware/ff553253)
 

 






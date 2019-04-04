---
title: IoAllocateForward ルール (wdm)
description: IoAllocateForward ルールを指定 IRP が IoAllocateIrp への呼び出しによって生成される場合、ドライバーする必要があります設定完了ルーチン保留または PoCallDriver を呼び出す前に。
ms.assetid: 5FA404C9-B5FD-47DA-9F9D-14C8F269B6A4
ms.date: 05/21/2018
keywords:
- IoAllocateForward ルール (wdm)
topic_type:
- apiref
api_name:
- IoAllocateForward
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 74ca8582ea831b4a9c7856b25b78e23032e8d7e1
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56536907"
---
# <a name="ioallocateforward-rule-wdm"></a>IoAllocateForward ルール (wdm)


**IoAllocateForward** IRP がへの呼び出しによって生成される場合をルール指定[ **IoAllocateIrp**](https://msdn.microsoft.com/library/windows/hardware/ff548257)ドライバーはを呼び出す前に完了ルーチンを設定する必要があります[**保留**](https://msdn.microsoft.com/library/windows/hardware/ff548336)または[ **PoCallDriver**](https://msdn.microsoft.com/library/windows/hardware/ff559654)します。

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
<td align="left"><p>実行<a href="https://msdn.microsoft.com/library/windows/hardware/ff552808" data-raw-source="[Static Driver Verifier](https://msdn.microsoft.com/library/windows/hardware/ff552808)">Static Driver Verifier</a>を指定し、 <strong>IoAllocateForward</strong>ルール。</p>
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

[**IoAllocateIrp**](https://msdn.microsoft.com/library/windows/hardware/ff548257)
[**保留**](https://msdn.microsoft.com/library/windows/hardware/ff548336)
[**IoSetCompletionRoutine** ](https://msdn.microsoft.com/library/windows/hardware/ff549679)
 [ **IoSetCompletionRoutineEx**](https://msdn.microsoft.com/library/windows/hardware/ff549686)
[**PoCallDriver**](https://msdn.microsoft.com/library/windows/hardware/ff559654)
 

 






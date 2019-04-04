---
title: PendedCompletedRequest ルール (wdm)
description: PendedCompletedRequest ルールでは、ドライバーのディスパッチ ルーチンに状態が返されないことを指定します\_IRP ドライバーには受信の IRP で IoCompleteRequest が呼び出された場合に保留します。
ms.assetid: 875409b0-b91c-44e6-8240-c5e656b70048
ms.date: 05/21/2018
keywords:
- PendedCompletedRequest ルール (wdm)
topic_type:
- apiref
api_name:
- PendedCompletedRequest
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 7563af494ff29f615f716bc0779e8c7a1067291b
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56581311"
---
# <a name="pendedcompletedrequest-rule-wdm"></a>PendedCompletedRequest ルール (wdm)


**PendedCompletedRequest**ルールでは、ドライバーのディスパッチ ルーチンに状態が返されないことを指定します\_IRP ドライバーが呼び出された場合に保留[ **IoCompleteRequest**](https://msdn.microsoft.com/library/windows/hardware/ff548343)の IRP を受信します。

このルールは、ドライバーは、任意のディスパッチ ルーチンの実行が開始した場合に適用されません。

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
<td align="left"><p>実行<a href="https://msdn.microsoft.com/library/windows/hardware/ff552808" data-raw-source="[Static Driver Verifier](https://msdn.microsoft.com/library/windows/hardware/ff552808)">Static Driver Verifier</a>を指定し、 <strong>PendedCompletedRequest</strong>ルール。</p>
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

[**保留**](https://msdn.microsoft.com/library/windows/hardware/ff548336)
[**IoCompleteRequest**](https://msdn.microsoft.com/library/windows/hardware/ff548343)
[**IoSetCompletionRoutine**](https://msdn.microsoft.com/library/windows/hardware/ff549679) 
 [ **KeInitializeEvent**](https://msdn.microsoft.com/library/windows/hardware/ff552137)
[**kewaitforsingleobject の 1** ](https://msdn.microsoft.com/library/windows/hardware/ff553350)
 [ **PoCallDriver**](https://msdn.microsoft.com/library/windows/hardware/ff559654)
[**RemoveHeadList**](https://msdn.microsoft.com/library/windows/hardware/ff561032)
 

 






---
title: CompleteRequestStatusCheck rule (wdm)
description: CompleteRequestStatusCheck ルールは、IRP の I/O の状態値が下位のドライバーによって返される状態値と一致することを確認します。
ms.assetid: 3B61137E-1D10-443B-A653-B32D638B17DB
ms.date: 05/21/2018
keywords:
- CompleteRequestStatusCheck rule (wdm)
topic_type:
- apiref
api_name:
- CompleteRequestStatusCheck
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 669cf9c721cef0c8ff84d830d71e786c73e6af08
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56573417"
---
# <a name="completerequeststatuscheck-rule-wdm"></a>CompleteRequestStatusCheck rule (wdm)


**CompleteRequestStatusCheck** IRP の I/O の状態値が下位のドライバーによって返される状態値と一致する規則を確認します。

IRP の状態が状態の場合、ドライバーのディスパッチ ルーチンは IRP を完了できませんが\_保留します。

ドライバーのディスパッチ ルーチンがステータスの IRP を完了できません\_下位のドライバーが IRP が失敗した場合は成功します。

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
<td align="left"><p>実行<a href="https://msdn.microsoft.com/library/windows/hardware/ff552808" data-raw-source="[Static Driver Verifier](https://msdn.microsoft.com/library/windows/hardware/ff552808)">Static Driver Verifier</a>を指定し、 <strong>CompleteRequestStatusCheck</strong>ルール。</p>
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

[**IoAcquireRemoveLock**](https://msdn.microsoft.com/library/windows/hardware/ff548204)
[**保留**](https://msdn.microsoft.com/library/windows/hardware/ff548336)
[**IoCompleteRequest** ](https://msdn.microsoft.com/library/windows/hardware/ff548343)
 [ **IoMarkIrpPending**](https://msdn.microsoft.com/library/windows/hardware/ff549422)
[**IoSetCompletionRoutine** ](https://msdn.microsoft.com/library/windows/hardware/ff549679) 
[ **IoSetCompletionRoutineEx**](https://msdn.microsoft.com/library/windows/hardware/ff549686)
[**kewaitforsingleobject の 1** ](https://msdn.microsoft.com/library/windows/hardware/ff553350) 
 [**PoCallDriver**](https://msdn.microsoft.com/library/windows/hardware/ff559654)
 

 






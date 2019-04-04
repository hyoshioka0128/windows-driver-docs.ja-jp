---
title: WithinCriticalRegion ルール (storport)
description: このルールは、通常カーネル APC 配信が無効になっている場合にのみ、特定の同期機能へのドライバーの呼び出しが行われることを確認します。
ms.assetid: 338E6995-0EB2-476D-B5F5-504DC8FF8609
ms.date: 05/21/2018
keywords:
- WithinCriticalRegion ルール (storport)
topic_type:
- apiref
api_name:
- WithinCriticalRegion
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: a1c354900f90e89144d16aac2a3f2ac01b25c3a2
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56556682"
---
# <a name="withincriticalregion-rule-storport"></a>WithinCriticalRegion ルール (storport)


このルールは、通常カーネル APC 配信が無効になっている場合にのみ、特定の同期機能へのドライバーの呼び出しが行われることを確認します。

|              |          |
|--------------|----------|
| ドライバー モデル | Storport |

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
<td align="left"><p>実行<a href="https://msdn.microsoft.com/library/windows/hardware/ff552808" data-raw-source="[Static Driver Verifier](https://msdn.microsoft.com/library/windows/hardware/ff552808)">Static Driver Verifier</a>を指定し、 <strong>WithinCriticalRegion</strong>ルール。</p>
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

[**ExAcquireResourceExclusiveLite**](https://msdn.microsoft.com/library/windows/hardware/ff544351)
[**ExAcquireResourceSharedLite** ](https://msdn.microsoft.com/library/windows/hardware/ff544363) 
 [ **ExAcquireSharedStarveExclusive**](https://msdn.microsoft.com/library/windows/hardware/ff544367)
[**ExAcquireSharedWaitForExclusive** ](https://msdn.microsoft.com/library/windows/hardware/ff544370) 
 [ **ExReleaseResourceForThreadLite**](https://msdn.microsoft.com/library/windows/hardware/ff545585)
[**ExReleaseResourceLite** ](https://msdn.microsoft.com/library/windows/hardware/ff545597) 
 [ **KeEnterCriticalRegion**](https://msdn.microsoft.com/library/windows/hardware/ff552021)
[**KeLeaveCriticalRegion**](https://msdn.microsoft.com/library/windows/hardware/ff552964)
 

 






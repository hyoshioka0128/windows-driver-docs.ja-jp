---
title: StorPortIrql ルール (storport)
description: StorPortIrql ルールでは、適切な IRQL レベル StorPort ルーチンが呼び出されることを確認します。
ms.assetid: 6A3946AB-DFB6-4447-9EF3-F0A003DB58E9
ms.date: 05/21/2018
keywords:
- StorPortIrql ルール (storport)
topic_type:
- apiref
api_name:
- StorPortIrql
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 80d2136af0dd47906761db2370990fa8b51b19a8
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56571614"
---
# <a name="storportirql-rule-storport"></a>StorPortIrql ルール (storport)


**StorPortIrql**ルールが StorPort ルーチンが、適切な IRQL レベルと呼ばれることを確認します。

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
<td align="left"><p>実行<a href="https://msdn.microsoft.com/library/windows/hardware/ff552808" data-raw-source="[Static Driver Verifier](https://msdn.microsoft.com/library/windows/hardware/ff552808)">Static Driver Verifier</a>を指定し、 <strong>StorPortIrql</strong>ルール。</p>
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

[**StorPortAllocateContiguousMemorySpecifyCacheNode**](https://msdn.microsoft.com/library/windows/hardware/ff567027)
[**StorPortAllocateMdl** ](https://msdn.microsoft.com/library/windows/hardware/ff567028) 
 [ **StorPortAllocatePool**](https://msdn.microsoft.com/library/windows/hardware/ff567031)
[**StorPortBuildMdlForNonPagedPool** ](https://msdn.microsoft.com/library/windows/hardware/ff567036) 
 [ **StorPortFreeContiguousMemorySpecifyCache**](https://msdn.microsoft.com/library/windows/hardware/ff567059)
[**StorPortFreeMdl** ](https://msdn.microsoft.com/library/windows/hardware/ff567063) 
 [ **StorPortFreePool**](https://msdn.microsoft.com/library/windows/hardware/ff567065)
[**StorPortGetActiveGroupCount** ](https://msdn.microsoft.com/library/windows/hardware/ff567071) 
 [ **StorPortGetActiveNodeCount**](https://msdn.microsoft.com/library/windows/hardware/ff567073)
[**StorPortGetCurrentProcessorNumber** ](https://msdn.microsoft.com/library/windows/hardware/ff567077) 
 [ **StorPortGetGroupAffinity**](https://msdn.microsoft.com/library/windows/hardware/ff567084)
[**StorPortGetHighestNodeNumber** ](https://msdn.microsoft.com/library/windows/hardware/ff567085) 
 [**StorPortGetLogicalProcessorRelationship**](https://msdn.microsoft.com/library/windows/hardware/ff567087)
[**StorPortGetNodeAffinity** ](https://msdn.microsoft.com/library/windows/hardware/ff567091)
 [ **StorPortGetSystemAddress**](https://msdn.microsoft.com/library/windows/hardware/ff567100)
[**StorPortLogSystemEvent** ](https://msdn.microsoft.com/library/windows/hardware/ff567428) 
 [ **StorPortPutScatterGatherList** ](https://msdn.microsoft.com/library/windows/hardware/ff567463) 
 [ **StorPortRegistryRead**](https://msdn.microsoft.com/library/windows/hardware/ff567491)
[**StorPortRegistryWrite**](https://msdn.microsoft.com/library/windows/hardware/ff567492)
 

 






---
title: StorPortIrql ルール (storport)
description: StorPortIrql ルールは、StorPort ルーチンが正しい IRQL レベルで呼び出されることを確認します。
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
ms.openlocfilehash: f6e5da0970b6ac8fc9a139c99ede070fd7865f0b
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72840016"
---
# <a name="storportirql-rule-storport"></a>StorPortIrql ルール (storport)


**Storportirql**ルールは、StorPort ルーチンが正しい IRQL レベルで呼び出されることを確認します。

|              |          |
|--------------|----------|
| ドライバーモデル | Storport |

<a name="how-to-test"></a>テストする方法
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
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/static-driver-verifier" data-raw-source="[Static Driver Verifier](https://docs.microsoft.com/windows-hardware/drivers/devtest/static-driver-verifier)">静的ドライバー検証ツール</a>を実行し、 <strong>Storportirql</strong>ルールを指定します。</p>
コードの分析を実行するには、次の手順に従います。
<ol>
<li><a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers#preparing-your-source-code" data-raw-source="[Prepare your code (use role type declarations).](https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers#preparing-your-source-code)">コードを準備します (ロールの種類の宣言を使用します)。</a></li>
<li><a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers#running-static-driver-verifier" data-raw-source="[Run Static Driver Verifier.](https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers#running-static-driver-verifier)">静的ドライバー検証ツールを実行します。</a></li>
<li><a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers#viewing-and-analyzing-the-results" data-raw-source="[View and analyze the results.](https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers#viewing-and-analyzing-the-results)">結果を表示して分析します。</a></li>
</ol>
<p>詳細については、「 <a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers" data-raw-source="[Using Static Driver Verifier to Find Defects in Drivers](https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers)">Static Driver Verifier を使用したドライバーの欠陥の検出</a>」を参照してください。</p></td>
</tr>
</tbody>
</table>

<a name="applies-to"></a>適用対象
----------

[**StorPortAllocateContiguousMemorySpecifyCacheNode**](https://docs.microsoft.com/windows-hardware/drivers/ddi/storport/nf-storport-storportallocatecontiguousmemoryspecifycachenode)
[**StorPortAllocateMdl**](https://docs.microsoft.com/windows-hardware/drivers/ddi/storport/nf-storport-storportallocatemdl)
[**StorPortAllocatePool**](https://docs.microsoft.com/windows-hardware/drivers/ddi/storport/nf-storport-storportallocatepool)
[**StorPortBuildMdlForNonPagedPool**](https://docs.microsoft.com/windows-hardware/drivers/ddi/storport/nf-storport-storportbuildmdlfornonpagedpool)
[**StorPortFreeContiguousMemorySpecifyCache**](https://docs.microsoft.com/windows-hardware/drivers/ddi/storport/nf-storport-storportfreecontiguousmemoryspecifycache)
[**Storportfreemdl**](https://docs.microsoft.com/windows-hardware/drivers/ddi/storport/nf-storport-storportfreemdl)
[**storportfreepool**](https://docs.microsoft.com/windows-hardware/drivers/ddi/storport/nf-storport-storportfreepool)
[**storportgetactivegroupcount**](https://docs.microsoft.com/windows-hardware/drivers/ddi/storport/nf-storport-storportgetactivegroupcount)
[**StorPortGetActiveNodeCount**](https://docs.microsoft.com/windows-hardware/drivers/ddi/storport/nf-storport-storportgetactivenodecount)
[**Storportgetcurrentprocessornumber**](https://docs.microsoft.com/windows-hardware/drivers/ddi/storport/nf-storport-storportgetcurrentprocessornumber)
[**StorPortGetGroupAffinity**](https://docs.microsoft.com/windows-hardware/drivers/ddi/storport/nf-storport-storportgetgroupaffinity)
[**StorPortGetHighestNodeNumber**](https://docs.microsoft.com/windows-hardware/drivers/ddi/storport/nf-storport-storportgethighestnodenumber)
[**storportgetcurrentprocessornumber**](https://docs.microsoft.com/windows-hardware/drivers/ddi/storport/nf-storport-storportgetlogicalprocessorrelationship)
[**StorPortGetNodeAffinity**](https://docs.microsoft.com/windows-hardware/drivers/ddi/storport/nf-storport-storportgetnodeaffinity)
[**StorPortGetSystemAddress**](https://docs.microsoft.com/windows-hardware/drivers/ddi/storport/nf-storport-storportgetsystemaddress)
[**Storportgetnodeaffinity**](https://docs.microsoft.com/windows-hardware/drivers/ddi/storport/nf-storport-storportlogsystemevent)
[**StorPortPutScatterGatherList**](https://docs.microsoft.com/windows-hardware/drivers/ddi/storport/nf-storport-storportputscattergatherlist)
[**storportregistryread**](https://docs.microsoft.com/windows-hardware/drivers/ddi/storport/nf-storport-storportregistryread)
[**StorPortRegistryWrite**](https://docs.microsoft.com/windows-hardware/drivers/ddi/storport/nf-storport-storportregistrywrite)
 

 






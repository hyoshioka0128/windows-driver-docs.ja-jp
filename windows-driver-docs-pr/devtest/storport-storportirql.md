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
ms.openlocfilehash: dc0eb437e406493cd6240481c2125a9c8c208940
ms.sourcegitcommit: f663c383886d87ea762e419963ff427500cc5042
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67391845"
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
<td align="left"><p>実行<a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/static-driver-verifier" data-raw-source="[Static Driver Verifier](https://docs.microsoft.com/windows-hardware/drivers/devtest/static-driver-verifier)">Static Driver Verifier</a>を指定し、 <strong>StorPortIrql</strong>ルール。</p>
コードの分析を実行するには、次の手順に従います。
<ol>
<li><a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers#preparing-your-source-code" data-raw-source="[Prepare your code (use role type declarations).](https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers#preparing-your-source-code)">(ロールの型宣言の使用)、コードを準備します。</a></li>
<li><a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers#running-static-driver-verifier" data-raw-source="[Run Static Driver Verifier.](https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers#running-static-driver-verifier)">Static Driver Verifier を実行します。</a></li>
<li><a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers#viewing-and-analyzing-the-results" data-raw-source="[View and analyze the results.](https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers#viewing-and-analyzing-the-results)">表示し、結果を分析します。</a></li>
</ol>
<p>詳細については、次を参照してください。<a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers" data-raw-source="[Using Static Driver Verifier to Find Defects in Drivers](https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers)">ドライバーで障害を検出する Static Driver Verifier を使用して</a>します。</p></td>
</tr>
</tbody>
</table>

<a name="applies-to"></a>対象
----------

[**StorPortAllocateContiguousMemorySpecifyCacheNode**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/storport/nf-storport-storportallocatecontiguousmemoryspecifycachenode)
[**StorPortAllocateMdl** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/storport/nf-storport-storportallocatemdl) 
 [ **StorPortAllocatePool**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/storport/nf-storport-storportallocatepool)
[**StorPortBuildMdlForNonPagedPool** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/storport/nf-storport-storportbuildmdlfornonpagedpool) 
 [ **StorPortFreeContiguousMemorySpecifyCache**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/storport/nf-storport-storportfreecontiguousmemoryspecifycache)
[**StorPortFreeMdl** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/storport/nf-storport-storportfreemdl) 
 [ **StorPortFreePool**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/storport/nf-storport-storportfreepool)
[**StorPortGetActiveGroupCount** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/storport/nf-storport-storportgetactivegroupcount) 
 [ **StorPortGetActiveNodeCount**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/storport/nf-storport-storportgetactivenodecount)
[**StorPortGetCurrentProcessorNumber** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/storport/nf-storport-storportgetcurrentprocessornumber) 
 [ **StorPortGetGroupAffinity**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/storport/nf-storport-storportgetgroupaffinity)
[**StorPortGetHighestNodeNumber** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/storport/nf-storport-storportgethighestnodenumber) 
 [**StorPortGetLogicalProcessorRelationship**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/storport/nf-storport-storportgetlogicalprocessorrelationship)
[**StorPortGetNodeAffinity** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/storport/nf-storport-storportgetnodeaffinity)
 [ **StorPortGetSystemAddress**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/storport/nf-storport-storportgetsystemaddress)
[**StorPortLogSystemEvent** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/storport/nf-storport-storportlogsystemevent) 
 [ **StorPortPutScatterGatherList** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/storport/nf-storport-storportputscattergatherlist) 
 [ **StorPortRegistryRead**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/storport/nf-storport-storportregistryread)
[**StorPortRegistryWrite**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/storport/nf-storport-storportregistrywrite)
 

 






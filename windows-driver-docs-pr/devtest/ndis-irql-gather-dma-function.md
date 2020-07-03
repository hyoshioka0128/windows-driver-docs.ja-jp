---
title: Irql \_ Gather \_ DMA \_ 関数の規則 (ndis)
description: Irql \_ Gather \_ dma 関数の規則は、 \_ NDIS スキャッター/ギャザー dma 関数を正しい Irql レベルで呼び出す必要があることを指定します。
ms.assetid: 2ac0d238-4ca0-4b07-9318-159cd9a64d35
ms.date: 05/21/2018
keywords:
- Irql_Gather_DMA_Function 規則 (ndis)
topic_type:
- apiref
api_name:
- Irql_Gather_DMA_Function
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: b6e9bda77fffb5b8bd9f4354a45a6f297384185e
ms.sourcegitcommit: 82a9be3b3584f991e5121f8f46a972e04185fa52
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/02/2020
ms.locfileid: "85917778"
---
# <a name="irql_gather_dma_function-rule-ndis"></a>Irql \_ Gather \_ DMA \_ 関数の規則 (ndis)


Irql \_ Gather \_ dma 関数の規則は、 \_ NDIS スキャッター/ギャザー dma 関数を正しい Irql レベルで呼び出す必要があることを指定します。

このルールは、次の NDIS 関数を検証します。

**NdisMAllocateNetBufferSGList** 
**NdisMAllocateSharedMemoryAsyncEx** 
**NdisMDeregisterScatterGatherDma** 
**NdisMFreeNetBufferSGList** 
**NdisMRegisterScatterGatherDma**

**ドライバーモデル: NDIS**

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
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/static-driver-verifier" data-raw-source="[Static Driver Verifier](https://docs.microsoft.com/windows-hardware/drivers/devtest/static-driver-verifier)">静的ドライバー検証ツール</a>を実行し、 <strong>Irql_Gather_DMA_Function</strong>規則を指定します。</p>
コードの分析を実行するには、次の手順に従います。
<ol>
<li><a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers#preparing-your-source-code" data-raw-source="[Prepare your code (use role type declarations).](https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers#preparing-your-source-code)">コードを準備します (役割の種類の宣言を使います)。</a></li>
<li><a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers#running-static-driver-verifier" data-raw-source="[Run Static Driver Verifier.](https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers#running-static-driver-verifier)">静的ドライバー検証ツールを実行します。</a></li>
<li><a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers#viewing-and-analyzing-the-results" data-raw-source="[View and analyze the results.](https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers#viewing-and-analyzing-the-results)">結果を表示して分析します。</a></li>
</ol>
<p>詳細については、「 <a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers" data-raw-source="[Using Static Driver Verifier to Find Defects in Drivers](https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers)">Static Driver Verifier を使用したドライバーの欠陥の検出</a>」を参照してください。</p></td>
</tr>
</tbody>
</table>

<a name="applies-to"></a>適用対象
----------

[**NdisMAllocateNetBufferSGList**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismallocatenetbuffersglist) 
[**NdisMAllocateSharedMemoryAsyncEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismallocatesharedmemoryasyncex) 
[**NdisMDeregisterScatterGatherDma**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismderegisterscattergatherdma) 
[**NdisMFreeNetBufferSGList**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismfreenetbuffersglist) 
[**NdisMRegisterScatterGatherDma**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismregisterscattergatherdma)









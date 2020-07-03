---
title: Irql \_ 同期 \_ 関数ルール (ndis)
description: Irql \_ 同期関数の規則は、 \_ NDIS 割り込みおよび同期 DDIs を正しい Irql レベルで呼び出す必要があることを指定します。
ms.assetid: 5d0e862a-89e6-493d-a102-83430c5140e4
ms.date: 05/21/2018
keywords:
- Irql_Synch_Function 規則 (ndis)
topic_type:
- apiref
api_name:
- Irql_Synch_Function
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 3e9f41b487bea9ad02bb2f71250e0fe2f1d90f4e
ms.sourcegitcommit: 82a9be3b3584f991e5121f8f46a972e04185fa52
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/02/2020
ms.locfileid: "85916510"
---
# <a name="irql_synch_function-rule-ndis"></a>Irql \_ 同期 \_ 関数ルール (ndis)


**Irql \_ 同期 \_ 関数**の規則は、NDIS 割り込みおよび同期 DDIs を正しい Irql レベルで呼び出す必要があることを指定します。

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
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/static-driver-verifier" data-raw-source="[Static Driver Verifier](https://docs.microsoft.com/windows-hardware/drivers/devtest/static-driver-verifier)">静的ドライバー検証ツール</a>を実行し、 <strong>Irql_Synch_Function</strong>規則を指定します。</p>
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

[**NDIS \_\_**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-release-mutex) 
 [** \_ \_ \_ ミューテックス**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-wait-for-mutex) 
 [**NdisAcquireReadWriteLock**](https://msdn.microsoft.com/library/windows/hardware/ff560696) 
 [**NdisAcquireSpinLock**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisacquirespinlock) 
 [**NdisDprAcquireSpinLock**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisdpracquirespinlock) 
 [**NdisDprReleaseSpinLock**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisdprreleasespinlock) 
 [**NdisReleaseReadWriteLock**](https://msdn.microsoft.com/library/windows/hardware/ff564521) 
 [**NdisReleaseSpinLock**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisreleasespinlock) 
 [**NdisResetEvent**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisresetevent) 
 [**NdisSetEvent**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndissetevent) NdisReleaseSpinLock NdisResetEvent NdisSetEvent のリリースミューテックス NDIS 待機
 

 






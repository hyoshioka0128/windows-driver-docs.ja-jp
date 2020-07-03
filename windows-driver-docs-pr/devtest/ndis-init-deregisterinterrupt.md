---
title: Init \_ DeRegisterInterrupt rule (ndis)
description: Init DeRegisterInterrupt ルールでは、 \_ MPInitilize 中に NdisMRegisterInterruptEx が少なくとも1回呼び出された場合、NdisMDeregisterInterruptEx は MPHaltEx で少なくとも1回呼び出される必要があることを指定します。
ms.assetid: C7436321-43DD-4B38-A0A3-9888CFDDA284
ms.date: 05/21/2018
keywords:
- Init_DeRegisterInterrupt 規則 (ndis)
topic_type:
- apiref
api_name:
- Init_DeRegisterInterrupt
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: d7bac55d94280de1bfa5e6d84b0497c23e8a3df1
ms.sourcegitcommit: 82a9be3b3584f991e5121f8f46a972e04185fa52
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/02/2020
ms.locfileid: "85916584"
---
# <a name="init_deregisterinterrupt-rule-ndis"></a>Init \_ DeRegisterInterrupt rule (ndis)


**Init \_ DeRegisterInterrupt**ルールでは、MPInitilize 中に[**NdisMRegisterInterruptEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismregisterinterruptex)が少なくとも1回呼び出された場合、 [**NdisMDeregisterInterruptEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismderegisterinterruptex)は MPHaltEx で少なくとも1回呼び出される必要があることを指定します。

初期化プロセスで何らかの問題が発生した場合、またはミニポートを停止した場合に、通常は初期化中に発生する割り込みの登録を取り消し (登録解除) する必要があります。

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
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/static-driver-verifier" data-raw-source="[Static Driver Verifier](https://docs.microsoft.com/windows-hardware/drivers/devtest/static-driver-verifier)">静的ドライバー検証ツール</a>を実行し、 <strong>Init_DeRegisterInterrupt</strong>規則を指定します。</p>
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

[**NdisMDeregisterInterruptEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismderegisterinterruptex) 
[ **NdisMRegisterInterruptEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismregisterinterruptex)
 

 






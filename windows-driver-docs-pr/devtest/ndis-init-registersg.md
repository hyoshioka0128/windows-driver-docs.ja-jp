---
title: 初期化 \_ registersg rule (ndis)
description: Init \_ registersg rule は、初期化プロセスで何らかの問題が発生した場合、またはミニポートドライバーの停止時に、通常は初期化中に発生するスキャッター/ギャザーリスト (SG) の登録を元に戻す必要があることを指定します。MiniportInitializeEx 中に NdisMRegisterScatterGatherDma が少なくとも1回呼び出された場合は、NdisMDeregisterScatterGatherDma 関数を MiniportHaltEx で少なくとも1回呼び出す必要があります。
ms.assetid: c4d00be1-b44b-4769-bbe6-6128a742d088
ms.date: 05/21/2018
keywords:
- Init_RegisterSG 規則 (ndis)
topic_type:
- apiref
api_name:
- Init_RegisterSG
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: c1d9b5023f6d8c9fc0a65f3db4c870578f1bdd34
ms.sourcegitcommit: 82a9be3b3584f991e5121f8f46a972e04185fa52
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/02/2020
ms.locfileid: "85918048"
---
# <a name="init_registersg-rule-ndis"></a>初期化 \_ registersg rule (ndis)


Init \_ registersg rule は、初期化プロセスで何らかの問題が発生した場合、またはミニポートドライバーの停止時に、通常は初期化中に発生するスキャッター/ギャザーリスト (SG) の登録を元に戻す必要があることを指定します。

**MiniportInitializeEx**中に**NdisMRegisterScatterGatherDma**が少なくとも1回呼び出された場合は、 **NdisMDeregisterScatterGatherDma**関数を**miniporthaltex**で少なくとも1回呼び出す必要があります。

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
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/static-driver-verifier" data-raw-source="[Static Driver Verifier](https://docs.microsoft.com/windows-hardware/drivers/devtest/static-driver-verifier)">静的ドライバー検証ツール</a>を実行し、 <strong>Init_RegisterSG</strong>規則を指定します。</p>
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

[**NdisMDeregisterScatterGatherDma**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismderegisterscattergatherdma) 
[ **NdisMRegisterScatterGatherDma**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismregisterscattergatherdma)
 

 






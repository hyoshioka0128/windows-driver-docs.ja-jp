---
title: StorPortAllocatePool ルール (storport)
description: このルールは、割り当て解除されたバッファーで、ミニポートが StorPortFreePool を呼び出すことができないことを確認します。
ms.assetid: DEE1768C-5BFF-4A8A-8AE9-9690FDA653C3
ms.date: 05/21/2018
keywords:
- StorPortAllocatePool ルール (storport)
topic_type:
- apiref
api_name:
- StorPortAllocatePool
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 6418ea45f9434300a03e7c84237ce9ba5d91af0d
ms.sourcegitcommit: 82a9be3b3584f991e5121f8f46a972e04185fa52
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/02/2020
ms.locfileid: "85917442"
---
# <a name="storportallocatepool-rule-storport"></a>StorPortAllocatePool ルール (storport)


このルールは、割り当て解除されたバッファーで、ミニポートが[**Storportfreepool**](https://docs.microsoft.com/windows-hardware/drivers/ddi/storport/nf-storport-storportfreepool)を呼び出すことができないことを確認します。

**ドライバーモデル: Storport**

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
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/static-driver-verifier" data-raw-source="[Static Driver Verifier](https://docs.microsoft.com/windows-hardware/drivers/devtest/static-driver-verifier)">静的ドライバー検証ツール</a>を実行し、 <strong>StorPortAllocatePool</strong>規則を指定します。</p>
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

[**StorPortAllocatePool**](https://docs.microsoft.com/windows-hardware/drivers/ddi/storport/nf-storport-storportallocatepool) 
[ **Storportfreepool**](https://docs.microsoft.com/windows-hardware/drivers/ddi/storport/nf-storport-storportfreepool)
 

 






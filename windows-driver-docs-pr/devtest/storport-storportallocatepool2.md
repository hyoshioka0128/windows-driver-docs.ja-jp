---
title: StorPortAllocatePool2 ルール (storport)
description: このルールは、割り当てられたバッファーに対して、最初に割り当て解除せずに StorPortAllocatePool を呼び出すことができないことを確認します。
ms.assetid: 3ECEDFDA-AE04-4DAC-926C-FB19CD955A38
ms.date: 05/21/2018
keywords:
- StorPortAllocatePool2 ルール (storport)
topic_type:
- apiref
api_name:
- StorPortAllocatePool2
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: a0d473a450ed39467ce4814be85123173e30f039
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72839289"
---
# <a name="storportallocatepool2-rule-storport"></a>StorPortAllocatePool2 ルール (storport)


このルールは、割り当てられたバッファーに対して、最初に割り当て解除せずに[**StorPortAllocatePool**](https://docs.microsoft.com/windows-hardware/drivers/ddi/storport/nf-storport-storportallocatepool)を呼び出すことができないことを確認します。

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
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/static-driver-verifier" data-raw-source="[Static Driver Verifier](https://docs.microsoft.com/windows-hardware/drivers/devtest/static-driver-verifier)">静的ドライバー検証ツール</a>を実行し、 <strong>StorPortAllocatePool2</strong>規則を指定します。</p>
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

[**StorPortAllocatePool**](https://docs.microsoft.com/windows-hardware/drivers/ddi/storport/nf-storport-storportallocatepool)
[ **storportfreepool**](https://docs.microsoft.com/windows-hardware/drivers/ddi/storport/nf-storport-storportfreepool)
 

 






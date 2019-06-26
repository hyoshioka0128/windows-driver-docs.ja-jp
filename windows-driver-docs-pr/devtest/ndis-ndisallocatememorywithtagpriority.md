---
title: NdisAllocateMemoryWithTagPriority ルール (ndis)
description: NdisAllocateMemoryWithTagPriority ルール エントリの識別できます Tag.Every メモリの割り当てでプールの一意のタグを使用してそのカーネル デバッガーことを確認する必要があり、ドライバーの検証ツールを提供することがなく、ドライバーをする必要があります NdisAllocateMemoryWithTagPriority が呼び出すされませんを指定する、個別の割り当てられたメモリ ブロックです。
ms.assetid: e27fe997-366d-4fe1-ad1e-3f145dc55f30
ms.date: 05/21/2018
keywords:
- NdisAllocateMemoryWithTagPriority ルール (ndis)
topic_type:
- apiref
api_name:
- NdisAllocateMemoryWithTagPriority
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 487cab2e5d37dc7f22604749261659b9f0f95292
ms.sourcegitcommit: f663c383886d87ea762e419963ff427500cc5042
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67392258"
---
# <a name="ndisallocatememorywithtagpriority-rule-ndis"></a>NdisAllocateMemoryWithTagPriority ルール (ndis)


**NdisAllocateMemoryWithTagPriority**ルールでは、ドライバーを呼び出してはならないことを指定します**NdisAllocateMemoryWithTagPriority**提供せず、*タグ*します。

すべてのメモリ割り当ては、カーネル デバッガーやドライバーの検証ツールが、個別に割り当てられたメモリ ブロックを識別することができますを確実に一意のプール タグを使用してください。

|              |      |
|--------------|------|
| ドライバー モデル | NDIS |

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
<td align="left"><p>実行<a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/static-driver-verifier" data-raw-source="[Static Driver Verifier](https://docs.microsoft.com/windows-hardware/drivers/devtest/static-driver-verifier)">Static Driver Verifier</a>を指定し、 <strong>NdisAllocateMemoryWithTagPriority</strong>ルール。</p>
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

<a name="applies-to"></a>適用対象
----------

[**NdisAllocateMemoryWithTagPriority**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisallocatememorywithtagpriority)
 

 






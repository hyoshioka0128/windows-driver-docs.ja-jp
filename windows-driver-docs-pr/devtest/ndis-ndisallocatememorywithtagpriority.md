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
ms.openlocfilehash: 76fa75da6afb5074bfe646bd298b1564a6a00e65
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56556559"
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
<td align="left"><p>実行<a href="https://msdn.microsoft.com/library/windows/hardware/ff552808" data-raw-source="[Static Driver Verifier](https://msdn.microsoft.com/library/windows/hardware/ff552808)">Static Driver Verifier</a>を指定し、 <strong>NdisAllocateMemoryWithTagPriority</strong>ルール。</p>
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

<a name="applies-to"></a>適用対象
----------

[**NdisAllocateMemoryWithTagPriority**](https://msdn.microsoft.com/library/windows/hardware/ff561606)
 

 






---
title: StorPortAllocatePool2 ルール (storport)
description: このルールは、ミニポートする必要がありますしないようにまず割り当てを解除せず、割り当てられたバッファーの StorPortAllocatePool を呼び出すかを確認します。
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
ms.openlocfilehash: 1fb500904bcc8cd2d3de64feba8d17752ce4f879
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63345696"
---
# <a name="storportallocatepool2-rule-storport"></a>StorPortAllocatePool2 ルール (storport)


このルールは、ミニポートが呼び出しを試みる必要がありますいないを確認します。 [ **StorPortAllocatePool** ](https://msdn.microsoft.com/library/windows/hardware/ff567031)で最初に割り当てを解除せず、割り当てられたバッファー。

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
<td align="left"><p>実行<a href="https://msdn.microsoft.com/library/windows/hardware/ff552808" data-raw-source="[Static Driver Verifier](https://msdn.microsoft.com/library/windows/hardware/ff552808)">Static Driver Verifier</a>を指定し、 <strong>StorPortAllocatePool2</strong>ルール。</p>
コードの分析を実行するには、次の手順に従います。
<ol>
<li><a href="https://msdn.microsoft.com/library/windows/hardware/hh454281#preparing-your-source-code" data-raw-source="[Prepare your code (use role type declarations).](https://msdn.microsoft.com/library/windows/hardware/hh454281#preparing-your-source-code)">(ロールの型宣言の使用)、コードを準備します。</a></li>
<li><a href="https://msdn.microsoft.com/library/windows/hardware/hh454281#running-static-driver-verifier" data-raw-source="[Run Static Driver Verifier.](https://msdn.microsoft.com/library/windows/hardware/hh454281#running-static-driver-verifier)">Static Driver Verifier を実行します。</a></li>
<li><a href="https://msdn.microsoft.com/library/windows/hardware/hh454281#viewing-and-analyzing-the-results" data-raw-source="[View and analyze the results.](https://msdn.microsoft.com/library/windows/hardware/hh454281#viewing-and-analyzing-the-results)">表示し、結果を分析します。</a></li>
</ol>
<p>詳細については、次を参照してください。<a href="https://msdn.microsoft.com/library/windows/hardware/hh454281" data-raw-source="[Using Static Driver Verifier to Find Defects in Drivers](https://msdn.microsoft.com/library/windows/hardware/hh454281)">ドライバーで障害を検出する Static Driver Verifier を使用して</a>します。</p></td>
</tr>
</tbody>
</table>

<a name="applies-to"></a>適用対象
----------

[**StorPortAllocatePool**](https://msdn.microsoft.com/library/windows/hardware/ff567031)
[**StorPortFreePool**](https://msdn.microsoft.com/library/windows/hardware/ff567065)
 

 






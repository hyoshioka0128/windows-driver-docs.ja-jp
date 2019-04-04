---
title: IoReuseIrp2 ルール (wdm)
description: IoReuseIrp2 ルールでは、ドライバーがドライバー内で割り当てられていた Irp でのみ IoReuseIrp を使用することを指定します。
ms.assetid: 707E14EA-96C2-4B50-B381-C3FCF45FA26C
ms.date: 05/21/2018
keywords:
- IoReuseIrp2 ルール (wdm)
topic_type:
- apiref
api_name:
- IoReuseIrp2
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: d1948e6bea27a999f1d41d55ca328628cb1b8a9e
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56573419"
---
# <a name="ioreuseirp2-rule-wdm"></a>IoReuseIrp2 ルール (wdm)


**IoReuseIrp2**ルールでは、ドライバーを使用することを指定します[ **IoReuseIrp** ](https://msdn.microsoft.com/library/windows/hardware/ff549661)ドライバー内で割り当てられていた Irp でのみです。

|              |     |
|--------------|-----|
| ドライバー モデル | WDM |

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
<td align="left"><p>実行<a href="https://msdn.microsoft.com/library/windows/hardware/ff552808" data-raw-source="[Static Driver Verifier](https://msdn.microsoft.com/library/windows/hardware/ff552808)">Static Driver Verifier</a>を指定し、 <strong>IoReuseIrp2</strong>ルール。</p>
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

<a name="applies-to"></a>対象
----------

[**IoReuseIrp**](https://msdn.microsoft.com/library/windows/hardware/ff549661)
 

 






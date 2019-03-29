---
title: IrqlMmDispatch ルール (wdm)
description: IrqlMmDispatch ルールでは、IRQL のディスパッチで実行されている場合にのみ、ドライバーが MmFreeContiguousMemory を呼び出すことを指定します\_レベル。
ms.assetid: C8F1CE43-C3E0-4ED3-8AEE-8E5D20FAC6E7
ms.date: 05/21/2018
keywords:
- IrqlMmDispatch ルール (wdm)
topic_type:
- apiref
api_name:
- IrqlMmDispatch
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 80c5c911c0fbce7769347082fcd318bda7c48acb
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56578269"
---
# <a name="irqlmmdispatch-rule-wdm"></a>IrqlMmDispatch ルール (wdm)


**IrqlMmDispatch**ルールでは、ドライバーを呼び出すことを指定します[ **MmFreeContiguousMemory** ](https://msdn.microsoft.com/library/windows/hardware/ff554503)のみとことで実行されている**IRQL &lt;=ディスパッチ\_レベル**します。

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
<td align="left"><p>実行<a href="https://msdn.microsoft.com/library/windows/hardware/ff552808" data-raw-source="[Static Driver Verifier](https://msdn.microsoft.com/library/windows/hardware/ff552808)">Static Driver Verifier</a>を指定し、 <strong>IrqlMmDispatch</strong>ルール。</p>
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

<a name="applies-to"></a>対象
----------

[**MmFreeContiguousMemory**](https://msdn.microsoft.com/library/windows/hardware/ff554503)
 

 






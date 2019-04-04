---
title: SpIrql ルール (storport)
description: このルールは検証 TdiRegisterPnPHandlers TdiDeregisterPnPHandlers のルーチンはのみという名前の IRQL でディスパッチより低い\_レベル。 ただし、ExFreeToNPagedLookasideList が呼び出された場合、規則に合格します。
ms.assetid: 895E3982-F50E-4B7A-9904-8D0D742A9B64
ms.date: 05/21/2018
keywords:
- SpIrql ルール (storport)
topic_type:
- apiref
api_name:
- SpIrql
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 048329ac7e84a8ed81540a5ffc4950afd22a185b
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56570845"
---
# <a name="spirql-rule-storport"></a>SpIrql ルール (storport)


このルールを検証するルーチン**TdiRegisterPnPHandlers**と**TdiDeregisterPnPHandlers**のみ呼び出される IRQL でよりも低い**ディスパッチ\_レベル**. ただし場合、 **ExFreeToNPagedLookasideList**を呼び出すと、ルール パス。

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
<td align="left"><p>実行<a href="https://msdn.microsoft.com/library/windows/hardware/ff552808" data-raw-source="[Static Driver Verifier](https://msdn.microsoft.com/library/windows/hardware/ff552808)">Static Driver Verifier</a>を指定し、 <strong>SpIrql</strong>ルール。</p>
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

[**ExFreeToNPagedLookasideList**](https://msdn.microsoft.com/library/windows/hardware/ff544601)
 

 






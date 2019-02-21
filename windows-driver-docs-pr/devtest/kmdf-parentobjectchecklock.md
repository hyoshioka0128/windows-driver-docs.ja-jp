---
title: ParentObjectCheckLock ルール (kmdf)
description: ParentObjectCheckLock ルールでは、WdfWaitLockCreate と WdfSpinLockCreate 親オブジェクトを設定したドライバーが呼び出す必要がありますを指定します。
ms.assetid: 01B47113-F949-4B38-982A-D13AF0EE68E0
ms.date: 05/21/2018
keywords:
- ParentObjectCheckLock ルール (kmdf)
topic_type:
- apiref
api_name:
- ParentObjectCheckLock
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: f8fd75a9e4255488bc69a2943da2c954435bb8e4
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56538540"
---
# <a name="parentobjectchecklock-rule-kmdf"></a>ParentObjectCheckLock ルール (kmdf)


**ParentObjectCheckLock**ルールでは、ドライバーを呼び出す必要がありますを指定します[ **WdfWaitLockCreate** ](https://msdn.microsoft.com/library/windows/hardware/ff551171)と[ **WdfSpinLockCreate**](https://msdn.microsoft.com/library/windows/hardware/ff550042)親オブジェクトを設定します。

|              |      |
|--------------|------|
| ドライバー モデル | KMDF |

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
<td align="left"><p>実行<a href="https://msdn.microsoft.com/library/windows/hardware/ff552808" data-raw-source="[Static Driver Verifier](https://msdn.microsoft.com/library/windows/hardware/ff552808)">Static Driver Verifier</a>を指定し、 <strong>ParentObjectCheckLock</strong>ルール。</p>
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

[**WdfSpinLockCreate**](https://msdn.microsoft.com/library/windows/hardware/ff550042)
[**WdfWaitLockCreate**](https://msdn.microsoft.com/library/windows/hardware/ff551171)
 

 






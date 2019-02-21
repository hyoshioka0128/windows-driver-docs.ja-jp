---
title: WdfInterruptLockRelease ルール (kmdf)
description: WdfInterruptLockRelease ルールでは、KMDF コールバック ルーチンのバランスの取れた方法で WdfInterruptAcquireLock および WdfInterruptReleaseLock への呼び出しが使用されることを指定します。
ms.assetid: 2cad3811-99c2-4909-bad6-54cab9f006e6
ms.date: 05/21/2018
keywords:
- WdfInterruptLockRelease ルール (kmdf)
topic_type:
- apiref
api_name:
- WdfInterruptLockRelease
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 53e4917f56253a328731f92a3d9b827a4b8a6176
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56553453"
---
# <a name="wdfinterruptlockrelease-rule-kmdf"></a>WdfInterruptLockRelease ルール (kmdf)


**WdfInterruptLockRelease**への呼び出し規則を指定[ **WdfInterruptAcquireLock** ](https://msdn.microsoft.com/library/windows/hardware/ff547340)と[ **WdfInterruptReleaseLock**](https://msdn.microsoft.com/library/windows/hardware/ff547376) KMDF コールバック ルーチンのバランスの取れた方法で使用されます。 任意の KMDF コールバック ルーチンの末尾には、ドライバー保持しないようにする以前の呼び出しによって取得されたフレームワークのスピン ロック オブジェクト**WdfInterruptAcquireLock**します。

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
<td align="left"><p>実行<a href="https://msdn.microsoft.com/library/windows/hardware/ff552808" data-raw-source="[Static Driver Verifier](https://msdn.microsoft.com/library/windows/hardware/ff552808)">Static Driver Verifier</a>を指定し、 <strong>WdfInterruptLockRelease</strong>ルール。</p>
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

[**WdfInterruptAcquireLock**](https://msdn.microsoft.com/library/windows/hardware/ff547340)
[**WdfInterruptReleaseLock**](https://msdn.microsoft.com/library/windows/hardware/ff547376)
 

 






---
title: WdfInterruptLockRelease ルール (kmdf)
description: WdfInterruptLockRelease 規則は、KMDF コールバックルーチン内で、WdfInterruptAcquireLock と WdfInterruptReleaseLock の呼び出しが均衡の取れた方法で使用されることを指定します。
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
ms.openlocfilehash: 5d4c3e7915a66b1ccd1dd038a4565613225914ac
ms.sourcegitcommit: 82a9be3b3584f991e5121f8f46a972e04185fa52
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/02/2020
ms.locfileid: "85917990"
---
# <a name="wdfinterruptlockrelease-rule-kmdf"></a>WdfInterruptLockRelease ルール (kmdf)


**WdfInterruptLockRelease**規則は、kmdf コールバックルーチン内で、 [**WdfInterruptAcquireLock**](https://msdn.microsoft.com/library/windows/hardware/ff547340)と[**WdfInterruptReleaseLock**](https://msdn.microsoft.com/library/windows/hardware/ff547376)の呼び出しが均衡の取れた方法で使用されることを指定します。 KMDF コールバックルーチンの最後では、 **WdfInterruptAcquireLock**への以前の呼び出しによって取得されたフレームワークのスピンロックオブジェクトをドライバーが保持することはできません。

**ドライバーモデル: KMDF**

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
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/static-driver-verifier" data-raw-source="[Static Driver Verifier](https://docs.microsoft.com/windows-hardware/drivers/devtest/static-driver-verifier)">静的ドライバー検証ツール</a>を実行し、 <strong>WdfInterruptLockRelease</strong>規則を指定します。</p>
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

[**WdfInterruptAcquireLock**](https://msdn.microsoft.com/library/windows/hardware/ff547340) 
[ **WdfInterruptReleaseLock**](https://msdn.microsoft.com/library/windows/hardware/ff547376)
 

 






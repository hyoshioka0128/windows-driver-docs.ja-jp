---
title: WdfInterruptLock ルール (kmdf)
description: WdfInterruptLock 規則は、WdfInterruptAcquireLock メソッドの呼び出しが WdfInterruptReleaseLock の呼び出しで厳格な代替で使用されることを指定します。
ms.assetid: bf105e83-dc63-44b1-ba9d-e4d81210fa1a
ms.date: 05/21/2018
keywords:
- WdfInterruptLock ルール (kmdf)
topic_type:
- apiref
api_name:
- WdfInterruptLock
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 4bffa20d56e066cb31d1550f6304b7565090543c
ms.sourcegitcommit: 82a9be3b3584f991e5121f8f46a972e04185fa52
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/02/2020
ms.locfileid: "85917994"
---
# <a name="wdfinterruptlock-rule-kmdf"></a>WdfInterruptLock ルール (kmdf)


**WdfInterruptLock**規則は、 [**WdfInterruptAcquireLock**](https://msdn.microsoft.com/library/windows/hardware/ff547340)メソッドの呼び出しが[**WdfInterruptReleaseLock**](https://msdn.microsoft.com/library/windows/hardware/ff547376)の呼び出しで厳格な代替で使用されることを指定します。 さらに、KMDF コールバックルーチンの最後では、ドライバーは、前の**WdfInterruptAcquireLock**の呼び出しで取得されたフレームワークのスピンロックオブジェクトを保持することはできません。

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
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/static-driver-verifier" data-raw-source="[Static Driver Verifier](https://docs.microsoft.com/windows-hardware/drivers/devtest/static-driver-verifier)">静的ドライバー検証ツール</a>を実行し、 <strong>WdfInterruptLock</strong>規則を指定します。</p>
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
 

 






---
title: WdfSpinlock ロック規則 (kmdf)
description: WdfSpinlock ロック規則は、WdfSpinLockAcquire メソッドへの呼び出しを WdfSpinlockRelease との厳密な代替で使用することを指定します。
ms.assetid: bf95509a-29f7-462d-b883-39aca4193ebb
ms.date: 05/21/2018
keywords:
- WdfSpinlock ロック規則 (kmdf)
topic_type:
- apiref
api_name:
- WdfSpinlock
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: f38aa51f0179b12465b2f4bebd44d5960d6672e1
ms.sourcegitcommit: 82a9be3b3584f991e5121f8f46a972e04185fa52
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/02/2020
ms.locfileid: "85916764"
---
# <a name="wdfspinlock-rule-kmdf"></a>WdfSpinlock ロック規則 (kmdf)


**Wdfspinlock ロック**規則は、 [**WdfSpinLockAcquire**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff550040(v=vs.85))メソッドへの呼び出しを[**WdfSpinlockRelease**](kmdf-wdfspinlockrelease.md)との厳密な代替で使用することを指定します。 KMDF コールバックルーチンの最後では、 **WdfSpinLockAcquire**への以前の呼び出しによって取得されたフレームワークスピンロックオブジェクトをドライバーが保持することはできません。

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
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/static-driver-verifier" data-raw-source="[Static Driver Verifier](https://docs.microsoft.com/windows-hardware/drivers/devtest/static-driver-verifier)">静的ドライバー検証ツール</a>を実行し、 <strong>wdfspinlock ロック</strong>規則を指定します。</p>
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

[**WdfSpinLockAcquire**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff550040(v=vs.85)) 
[**WdfSpinLockCreate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfsync/nf-wdfsync-wdfspinlockcreate) 
[**WdfSpinLockRelease**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff550044(v=vs.85))
 

 






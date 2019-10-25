---
title: IrqlKeApcLte1 ルール (wdm)
ms.assetid: d88e3c0f-574b-41df-97ee-282a9f1eb6f4
ms.date: 05/21/2018
description: ''
keywords:
- IrqlKeApcLte1 ルール (wdm)
topic_type:
- apiref
api_name:
- IrqlKeApcLte1
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 2fb8d54c985f5fad6c87f0bdf8029f948504c519
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72839921"
---
# <a name="irqlkeapclte1-rule-wdm"></a>IrqlKeApcLte1 ルール (wdm)


**IrqlKeApcLte1**規則は、ドライバーが IRQL &lt;= APC\_レベルで実行されている場合にのみ、次のカーネルルーチンを呼び出すように指定します。

-   [**KeAcquireGuardedMutex**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff551892(v=vs.85))

-   [**KeAcquireGuardedMutexUnsafe**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff551894(v=vs.85))

-   [**KeDelayExecutionThread**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-kedelayexecutionthread)

-   [**KeQueryActiveProcessors**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-kequeryactiveprocessors)

-   [**KeReleaseGuardedMutex**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-kereleaseguardedmutex)

-   [**KeReleaseGuardedMutexUnsafe**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-kereleaseguardedmutexunsafe)

-   [**KeTryToAcquireGuardedMutex**](https://msdn.microsoft.com/library/windows/hardware/ff553307)

|              |     |
|--------------|-----|
| ドライバー モデル | WDM |

|                                   |                                                                                                                                       |
|-----------------------------------|---------------------------------------------------------------------------------------------------------------------------------------|
| この規則で見つかったバグ チェック | [**バグチェック 0xC4: ドライバー\_VERIFIER\_検出された\_違反**](https://docs.microsoft.com/windows-hardware/drivers/debugger/bug-check-0xc4--driver-verifier-detected-violation)(0x0002000F) |

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
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/static-driver-verifier" data-raw-source="[Static Driver Verifier](https://docs.microsoft.com/windows-hardware/drivers/devtest/static-driver-verifier)">静的ドライバー検証ツール</a>を実行し、 <strong>IrqlKeApcLte1</strong>規則を指定します。</p>
コードの分析を実行するには、次の手順に従います。
<ol>
<li><a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers#preparing-your-source-code" data-raw-source="[Prepare your code (use role type declarations).](https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers#preparing-your-source-code)">コードを準備します (ロールの種類の宣言を使用します)。</a></li>
<li><a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers#running-static-driver-verifier" data-raw-source="[Run Static Driver Verifier.](https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers#running-static-driver-verifier)">静的ドライバー検証ツールを実行します。</a></li>
<li><a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers#viewing-and-analyzing-the-results" data-raw-source="[View and analyze the results.](https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers#viewing-and-analyzing-the-results)">結果を表示して分析します。</a></li>
</ol>
<p>詳細については、「 <a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers" data-raw-source="[Using Static Driver Verifier to Find Defects in Drivers](https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers)">Static Driver Verifier を使用したドライバーの欠陥の検出</a>」を参照してください。</p></td>
</tr>
</tbody>
</table>

<table>
<colgroup>
<col width="100%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">実行時</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/driver-verifier" data-raw-source="[Driver Verifier](https://docs.microsoft.com/windows-hardware/drivers/devtest/driver-verifier)">ドライバーの検証ツール</a>を実行し、[ <a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/ddi-compliance-checking" data-raw-source="[DDI compliance checking](https://docs.microsoft.com/windows-hardware/drivers/devtest/ddi-compliance-checking)">DDI 準拠チェック</a>] オプションを選択します。</p></td>
</tr>
</tbody>
</table>

 

<a name="applies-to"></a>適用対象
----------

[**KeAcquireGuardedMutex**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff551892(v=vs.85))
[**KeAcquireGuardedMutexUnsafe**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff551894(v=vs.85))
[**Kedelayexecutionthread**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-kedelayexecutionthread)
[**kedelayexecutionthread**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-kequeryactiveprocessors)
[**KeReleaseGuardedMutex**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-kereleaseguardedmutex)
[**KeReleaseGuardedMutexUnsafe**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-kereleaseguardedmutexunsafe)
[**KeTryToAcquireGuardedMutex**](https://msdn.microsoft.com/library/windows/hardware/ff553307)
 

 






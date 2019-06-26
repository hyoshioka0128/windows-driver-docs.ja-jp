---
title: WithinCriticalRegion ルール (wdm)
description: WithinCriticalRegion ルールでは、KeEnterCriticalRegion を呼び出した後にだけ、KeLeaveCriticalRegion を呼び出す前に、ドライバーの特定の同期の関数呼び出しが表示されることを指定します。
ms.assetid: 9b74b868-6025-4e81-b5ba-21e0da734cd9
ms.date: 05/21/2018
keywords:
- WithinCriticalRegion ルール (wdm)
topic_type:
- apiref
api_name:
- WithinCriticalRegion
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 425ec10685a31987b83fa26801b72ea20a902e53
ms.sourcegitcommit: f663c383886d87ea762e419963ff427500cc5042
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67392012"
---
# <a name="withincriticalregion-rule-wdm"></a>WithinCriticalRegion ルール (wdm)


**WithinCriticalRegion**ルールでは、ドライバーの特定の同期の関数呼び出しを呼び出した後のみが表示されることを指定します[ **KeEnterCriticalRegion** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddk/nf-ntddk-keentercriticalregion)と呼び出しの前に[ **KeLeaveCriticalRegion**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddk/nf-ntddk-keleavecriticalregion)します。

影響を受ける同期関数、次に示します。

-   [**ExAcquireResourceSharedLite**](https://msdn.microsoft.com/library/windows/hardware/ff544363)

-   [**ExAcquireResourceExclusiveLite**](https://msdn.microsoft.com/library/windows/hardware/ff544351)

-   [**ExAcquireSharedStarveExclusive**](https://msdn.microsoft.com/library/windows/hardware/ff544367)

-   [**ExAcquireSharedWaitForExclusive**](https://msdn.microsoft.com/library/windows/hardware/ff544370)

-   [**ExReleaseResourceLite**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-exreleaseresourcelite)

-   [**ExReleaseResourceForThreadLite**](https://msdn.microsoft.com/library/windows/hardware/ff545585)

このルールは、通常の APC 配信を無効にするには、他の方法を認識しません。 詳細については、次を参照してください。 [ **Apc を無効にすると**](https://docs.microsoft.com/windows-hardware/drivers/kernel/disabling-apcs)します。

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
<td align="left"><p>実行<a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/static-driver-verifier" data-raw-source="[Static Driver Verifier](https://docs.microsoft.com/windows-hardware/drivers/devtest/static-driver-verifier)">Static Driver Verifier</a>を指定し、 <strong>WithinCriticalRegion</strong>ルール。</p>
コードの分析を実行するには、次の手順に従います。
<ol>
<li><a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers#preparing-your-source-code" data-raw-source="[Prepare your code (use role type declarations).](https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers#preparing-your-source-code)">(ロールの型宣言の使用)、コードを準備します。</a></li>
<li><a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers#running-static-driver-verifier" data-raw-source="[Run Static Driver Verifier.](https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers#running-static-driver-verifier)">Static Driver Verifier を実行します。</a></li>
<li><a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers#viewing-and-analyzing-the-results" data-raw-source="[View and analyze the results.](https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers#viewing-and-analyzing-the-results)">表示し、結果を分析します。</a></li>
</ol>
<p>詳細については、次を参照してください。<a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers" data-raw-source="[Using Static Driver Verifier to Find Defects in Drivers](https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers)">ドライバーで障害を検出する Static Driver Verifier を使用して</a>します。</p></td>
</tr>
</tbody>
</table>

<a name="applies-to"></a>適用対象
----------

[**ExAcquireResourceExclusiveLite**](https://msdn.microsoft.com/library/windows/hardware/ff544351)
[**ExAcquireResourceSharedLite** ](https://msdn.microsoft.com/library/windows/hardware/ff544363) 
 [ **ExAcquireSharedStarveExclusive**](https://msdn.microsoft.com/library/windows/hardware/ff544367)
[**ExAcquireSharedWaitForExclusive** ](https://msdn.microsoft.com/library/windows/hardware/ff544370) 
 [ **ExReleaseResourceForThreadLite**](https://msdn.microsoft.com/library/windows/hardware/ff545585)
[**ExReleaseResourceLite** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-exreleaseresourcelite) 
 [ **KeEnterCriticalRegion**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddk/nf-ntddk-keentercriticalregion)
[**KeEnterGuardedRegion** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddk/nf-ntddk-keenterguardedregion) 
 [ **KeLeaveCriticalRegion**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddk/nf-ntddk-keleavecriticalregion)
[**KeLeaveGuardedRegion** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddk/nf-ntddk-keleaveguardedregion)も参照してください
--------

[**ハードウェアの優先度を管理する**](https://docs.microsoft.com/windows-hardware/drivers/kernel/managing-hardware-priorities)
[**スピン ロックの使用中にエラーおよびデッドロックの防止**](https://docs.microsoft.com/windows-hardware/drivers/kernel/preventing-errors-and-deadlocks-while-using-spin-locks)
 

 






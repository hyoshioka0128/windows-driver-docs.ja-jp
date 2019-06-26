---
title: MarkingInterlockedQueuedIrps ルール (wdm)
description: MarkingInterlockedQueuedIrps ルールでは、前に、さらに処理するため、インタロックされた形式でキュー、ドライバーがその保留中として IRP を正しくマークすることを指定します。
ms.assetid: a065b28f-f02a-45af-b9d9-754a36519b99
ms.date: 05/21/2018
keywords:
- MarkingInterlockedQueuedIrps ルール (wdm)
topic_type:
- apiref
api_name:
- MarkingInterlockedQueuedIrps
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: eddaa1247f5be4925a42bb155b7c29316d2185ba
ms.sourcegitcommit: f663c383886d87ea762e419963ff427500cc5042
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67392044"
---
# <a name="markinginterlockedqueuedirps-rule-wdm"></a>MarkingInterlockedQueuedIrps ルール (wdm)


**MarkingInterlockedQueuedIrps**ルールでは、前に保留中、キューにそれをさらに処理するためのインタロックされた方法でと、ドライバーがその IRP を正しくマークことを指定します。

このルールは、ドライバーを呼び出すことを指定しますも[ **IoMarkIrpPending** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iomarkirppending)し呼び出します IRP をインタロックされたキューに追加するには、次の関数のいずれかの前に保留中として、IRP を正しくマークします。

-   [**ExInterlockedInsertHeadList**](https://msdn.microsoft.com/library/windows/hardware/ff545397)

-   [**ExInterlockedInsertTailList**](https://msdn.microsoft.com/library/windows/hardware/ff545402)

-   [**ExInterlockedPushEntryList**](https://msdn.microsoft.com/library/windows/hardware/ff545418)

ドライバーを呼び出す必要があります[ **IoMarkIrpPending** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iomarkirppending)インタロックされたキューに複数の処理が必要な IRP を追加する前にします。 それ以外の場合、IRP でしたデキューされた別のドライバーのルーチンで完了し、呼び出しの前に、システムによって解放**IoMarkIrpPending**原因となり、クラッシュが発生します。

詳細については、次を参照してください。 [**同期 IRP キャンセル**](https://docs.microsoft.com/windows-hardware/drivers/kernel/synchronizing-irp-cancellation)します。

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
<td align="left"><p>実行<a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/static-driver-verifier" data-raw-source="[Static Driver Verifier](https://docs.microsoft.com/windows-hardware/drivers/devtest/static-driver-verifier)">Static Driver Verifier</a>を指定し、 <strong>MarkingInterlockedQueuedIrps</strong>ルール。</p>
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

[**ExInterlockedInsertHeadList**](https://msdn.microsoft.com/library/windows/hardware/ff545397)
[**ExInterlockedInsertTailList** ](https://msdn.microsoft.com/library/windows/hardware/ff545402) 
 [ **ExInterlockedPushEntryList**](https://msdn.microsoft.com/library/windows/hardware/ff545418)
[**IoMarkIrpPending** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iomarkirppending) 
 [ **RemoveHeadList** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-removeheadlist)も参照してください
--------

[**MarkIrpPending**](wdm-markirppending.md)
[**IRP のキャンセルを同期します。** ](https://docs.microsoft.com/windows-hardware/drivers/kernel/synchronizing-irp-cancellation)
 

 






---
title: MarkingQueuedIrps ルール (wdm)
description: MarkingQueuedIrps ルールでは、ドライバーがさらに、スピン ロックを保持している場合にのみ処理が必要な IRP の IoMarkIrpPending を呼び出すことを指定します。 このルールは、ドライバーがドライバー管理キューに IRP を追加するときにのみ適用されます。
ms.assetid: 3a70ba52-c62f-4574-9a2e-4ba7aed82529
ms.date: 05/21/2018
keywords:
- MarkingQueuedIrps ルール (wdm)
topic_type:
- apiref
api_name:
- MarkingQueuedIrps
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 01f10ef35b097bb5acd9e7ec727db5ee2c1c3ece
ms.sourcegitcommit: f663c383886d87ea762e419963ff427500cc5042
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67392037"
---
# <a name="markingqueuedirps-rule-wdm"></a>MarkingQueuedIrps ルール (wdm)


**MarkingQueuedIrps**ルールでは、ドライバーを呼び出すことを指定します[ **IoMarkIrpPending** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iomarkirppending)の IRP をさらに、スピン ロックを保持している場合にのみ処理を必要とします。 このルールは、ドライバーがドライバー管理キューに IRP を追加するときにのみ適用されます。

具体的には、この規則に違反ドライバー場合にのみ*すべて*次のイベントが発生します。

-   ドライバー呼び出し[ **KeAcquireSpinLock** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-keacquirespinlock)または[ **KeAcquireInStackQueuedSpinLock** ](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff551899(v=vs.85))スピン ロックを取得します。

-   ドライバーは IRP をドライバー管理キューに追加する、次のルーチンのいずれかを呼び出します。
    -   [**InsertHeadList**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-insertheadlist)
    -   [**InsertTailList**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-inserttaillist)
    -   [**KeInsertDeviceQueue**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-keinsertdevicequeue)
    -   [**KeInsertQueueDpc**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-keinsertqueuedpc)
    -   [**KeInsertByKeyDeviceQueue**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-keinsertbykeydevicequeue)
-   ドライバー呼び出し[ **KeReleaseSpinLock** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-kereleasespinlock)または[ **KeReleaseInStackQueuedSpinLock** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-kereleaseinstackqueuedspinlock) を呼び出す前に、スピンロックを解除するには**IoMarkIrpPending**します。

-   ドライバーのステータスを返します\_IRP を保留します。

ドライバーを呼び出す必要があります**IoMarkIrpPending**スピン ロックを保持している場合にのみキューに置かれた IRP の。 それ以外の場合、IRP でしたデキューされた別のドライバーのルーチンで完了し、呼び出しの前に、システムによって解放**IoMarkIrpPending**原因となり、クラッシュが発生します。

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
<td align="left"><p>実行<a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/static-driver-verifier" data-raw-source="[Static Driver Verifier](https://docs.microsoft.com/windows-hardware/drivers/devtest/static-driver-verifier)">Static Driver Verifier</a>を指定し、 <strong>MarkingQueuedIrps</strong>ルール。</p>
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

[**InsertHeadList**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-insertheadlist)
[**保留**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iocalldriver)
[**IoMarkIrpPending** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iomarkirppending) 
 [ **KeAcquireInStackQueuedSpinLock**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff551899(v=vs.85))
[**KeAcquireSpinLock** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-keacquirespinlock)
 [ **KeInsertByKeyDeviceQueue**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-keinsertbykeydevicequeue)
[**KeInsertDeviceQueue** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-keinsertdevicequeue) 
 [ **KeInsertQueueDpc**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-keinsertqueuedpc)
[**KeReleaseInStackQueuedSpinLock** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-kereleaseinstackqueuedspinlock) 
[ **KeReleaseSpinLock**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-kereleasespinlock)
[**PoCallDriver** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-pocalldriver) 
 [ **RemoveHeadList**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-removeheadlist)
 

 






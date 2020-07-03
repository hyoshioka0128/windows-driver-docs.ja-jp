---
title: MarkingQueuedIrps ルール (wdm)
description: MarkingQueuedIrps ルールでは、スピンロックを保持しているときにのみさらに処理する必要がある IRP に対して、ドライバーが IoMarkIrpPending を呼び出すことを指定します。 この規則は、ドライバーによって管理されるキューに IRP を追加する場合にのみ適用されます。
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
ms.openlocfilehash: 432228b9c75956a899d952fd66f27905453b560a
ms.sourcegitcommit: 82a9be3b3584f991e5121f8f46a972e04185fa52
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/02/2020
ms.locfileid: "85917876"
---
# <a name="markingqueuedirps-rule-wdm"></a>MarkingQueuedIrps ルール (wdm)


**Markingqueuedirps**ルールでは、スピンロックを保持しているときにのみさらに処理する必要がある IRP に対して、ドライバーが[**Iomarkirppending**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iomarkirppending)を呼び出すことを指定します。 この規則は、ドライバーによって管理されるキューに IRP を追加する場合にのみ適用されます。

具体的には、次の*すべて*のイベントが発生した場合にのみ、ドライバーはこの規則に違反します。

-   ドライバーは、 [**KeAcquireSpinLock**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-keacquirespinlock)または[**KeAcquireInStackQueuedSpinLock**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff551899(v=vs.85))を呼び出して、スピンロックを取得します。

-   ドライバーは、次のいずれかのルーチンを呼び出して、IRP をドライバーで管理されたキューに追加します。
    -   [**埋め込みリスト**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-insertheadlist)
    -   [**InsertTailList**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-inserttaillist)
    -   [**KeInsertDeviceQueue**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-keinsertdevicequeue)
    -   [**KeInsertQueueDpc**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-keinsertqueuedpc)
    -   [**KeInsertByKeyDeviceQueue**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-keinsertbykeydevicequeue)
-   ドライバーは、 [**KeReleaseSpinLock**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-kereleasespinlock)または[**KeReleaseInStackQueuedSpinLock**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-kereleaseinstackqueuedspinlock)を呼び出して、 **iomarkirppending**を呼び出す前に、スピンロックを解放します。

-   ドライバーは、IRP の保留状態の状態を返し \_ ます。

ドライバーは、スピンロックを保持したまま、キューに入っている IRP に対して**Iomarkirppending**を呼び出す必要があります。 それ以外の場合、IRP は、別のドライバールーチンによってデキューされ、システムによって解放されてから、 **Iomarkirppending**が呼び出される前にクラッシュが発生します。

詳細については、「 [**IRP のキャンセルの同期**](https://docs.microsoft.com/windows-hardware/drivers/kernel/synchronizing-irp-cancellation)」を参照してください。

**ドライバーモデル: WDM**

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
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/static-driver-verifier" data-raw-source="[Static Driver Verifier](https://docs.microsoft.com/windows-hardware/drivers/devtest/static-driver-verifier)">静的ドライバー検証ツール</a>を実行し、 <strong>Markingqueuedirps</strong>ルールを指定します。</p>
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

[**埋め込みリスト**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-insertheadlist) 
[**IoCallDriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocalldriver) 
[**Iomarkirppending**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iomarkirppending) 
[**KeAcquireInStackQueuedSpinLock**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff551899(v=vs.85)) 
[**KeAcquireSpinLock**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-keacquirespinlock) 
[**Keinsertbykeydevicequeue**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-keinsertbykeydevicequeue) 
[**Keinsertdevicequeue**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-keinsertdevicequeue) 
[**KeInsertQueueDpc**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-keinsertqueuedpc) 
[**KeReleaseInStackQueuedSpinLock**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-kereleaseinstackqueuedspinlock) 
[**KeReleaseSpinLock**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-kereleasespinlock) 
[**Pocalldriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-pocalldriver) 
[**Removeヘッドホンの一覧**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-removeheadlist)
 

 






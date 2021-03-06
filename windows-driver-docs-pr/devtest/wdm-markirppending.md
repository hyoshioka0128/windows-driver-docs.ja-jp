---
title: MarkIrpPending ルール (wdm)
description: MarkIrpPending ルールでは、ドライバーのディスパッチ ルーチンが IoMarkIrpPending を呼び出すたびに、ドライバーが状態を返すように指定します\_ディスパッチ ルーチンが終了する保留中です。 無料の仕様の MarkIrpPending2 を参照してください。
ms.assetid: cbf5484e-2806-4df6-bdfb-98acfe5d214c
ms.date: 05/21/2018
keywords:
- MarkIrpPending ルール (wdm)
topic_type:
- apiref
api_name:
- MarkIrpPending
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 1cd019cd0640deb5b3b47db98279d899da1ee18f
ms.sourcegitcommit: f663c383886d87ea762e419963ff427500cc5042
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67392034"
---
# <a name="markirppending-rule-wdm"></a>MarkIrpPending ルール (wdm)


**MarkIrpPending**規則で指定されるたびに、ドライバーのディスパッチ ルーチンを呼び出すこと[ **IoMarkIrpPending**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iomarkirppending)、ドライバーは状態を返します\_保留中の場合ディスパッチ ルーチンを終了します。 参照してください[ **MarkIrpPending2** ](wdm-markirppending2.md)の無償の仕様。

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
<td align="left"><p>実行<a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/static-driver-verifier" data-raw-source="[Static Driver Verifier](https://docs.microsoft.com/windows-hardware/drivers/devtest/static-driver-verifier)">Static Driver Verifier</a>を指定し、 <strong>MarkIrpPending</strong>ルール。</p>
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

[**保留**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iocalldriver)
[**IoCompleteRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iocompleterequest)
[**IoMarkIrpPending** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iomarkirppending)
 [ **PoCallDriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-pocalldriver)
[**RemoveHeadList** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-removeheadlist)も参照してください
--------

[**MarkingInterlockedQueuedIrps**](wdm-markinginterlockedqueuedirps.md)
[**IRP のキャンセルを同期します。** ](https://docs.microsoft.com/windows-hardware/drivers/kernel/synchronizing-irp-cancellation)
 

 






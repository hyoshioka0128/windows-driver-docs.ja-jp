---
title: IrqlDispatch ルール (storport)
description: このルールは、次のルーチンが IRQL のディスパッチにのみ呼び出されることを確認します。\_レベル。
ms.assetid: 93ABD54D-4D63-495A-917B-A387C9353969
ms.date: 05/21/2018
keywords:
- IrqlDispatch ルール (storport)
topic_type:
- apiref
api_name:
- IrqlDispatch
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: afe90c19ac81c88c20531dc1b629020161ab396a
ms.sourcegitcommit: f663c383886d87ea762e419963ff427500cc5042
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67391918"
---
# <a name="irqldispatch-rule-storport"></a>IrqlDispatch ルール (storport)


このルールは、次のルーチンがでのみ呼び出されることを確認します。 **IRQL = ディスパッチ\_レベル**します。

-   AllocateAdapterChannel

-   FreeAdapterChannel

-   FreeMapRegisters

-   GetScatterGatherList

-   IoAllocateController

-   IoFreeController

-   います

-   KeAcquireSpinLockAtDpcLevel

-   KeInsertByKeyDeviceQueue

-   KeInsertDeviceQueue

-   KeReleaseSpinLockFromDpcLevel

-   KeRemoveByKeyDeviceQueue

-   KeRemoveDeviceQueue

-   PutScatterGatherList

|              |          |
|--------------|----------|
| ドライバー モデル | Storport |

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
<td align="left"><p>実行<a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/static-driver-verifier" data-raw-source="[Static Driver Verifier](https://docs.microsoft.com/windows-hardware/drivers/devtest/static-driver-verifier)">Static Driver Verifier</a>を指定し、 <strong>IrqlDispatch</strong>ルール。</p>
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

<a name="applies-to"></a>対象
----------

[**AllocateAdapterChannel**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-pallocate_adapter_channel)
[**FreeAdapterChannel**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-pfree_adapter_channel)
[**FreeMapRegisters** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-pfree_map_registers) 
 [ **GetScatterGatherList**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-pget_scatter_gather_list)
[**IoAllocateController** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddk/nf-ntddk-ioallocatecontroller)
 [ **IoFreeController**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddk/nf-ntddk-iofreecontroller)
[**います**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-iostartnextpacket) 
 [**KeAcquireSpinLockAtDpcLevel**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-keacquirespinlockatdpclevel)
[**KeInsertByKeyDeviceQueue** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-keinsertbykeydevicequeue) 
 [**KeInsertDeviceQueue**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-keinsertdevicequeue)
[**KeReleaseSpinLockFromDpcLevel** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-kereleasespinlockfromdpclevel) 
 [ **KeRemoveByKeyDeviceQueue**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-keremovebykeydevicequeue)
[**KeRemoveDeviceQueue** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-keremovedevicequeue) 
 [ **PutScatterGatherList**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-pput_scatter_gather_list)
 

 






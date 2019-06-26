---
title: IrqlDispatch ルール (wdm)
description: IrqlDispatch ルールでは、IRQL DISPATCH_LEVEL で実行されている場合にのみ、ドライバーが次の Ddi を呼び出すことを指定します。
ms.assetid: f72d4f27-b488-4d0a-97b7-9cb40f00e346
ms.date: 05/21/2018
keywords:
- IrqlDispatch ルール (wdm)
topic_type:
- apiref
api_name:
- IrqlDispatch
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: edddbe1703fe17367b315e6c5d4ee09c0a0ad18a
ms.sourcegitcommit: f663c383886d87ea762e419963ff427500cc5042
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67393909"
---
# <a name="irqldispatch-rule-wdm"></a>IrqlDispatch ルール (wdm)


**IrqlDispatch**ルールでは、IRQL で実行されている場合にのみ、ドライバーが次の Ddi を呼び出すことを指定します = ディスパッチ\_レベル。

-   [**FreeAdapterChannel**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-pfree_adapter_channel)

-   [**FreeMapRegisters**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-pfree_map_registers)

-   [**GetScatterGatherList**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-pget_scatter_gather_list)

-   [**IoAllocateAdapterChannel**](https://docs.microsoft.com/windows-hardware/drivers/kernel/mmcreatemdl)

-   [**IoAllocateController**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddk/nf-ntddk-ioallocatecontroller)

-   [**IoFreeController**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddk/nf-ntddk-iofreecontroller)

-   [**います**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-iostartnextpacket)

-   [**KeAcquireSpinLockAtDpcLevel**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-keacquirespinlockatdpclevel)

-   [**KeInsertByKeyDeviceQueue**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-keinsertbykeydevicequeue)

-   [**KeInsertDeviceQueue**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-keinsertdevicequeue)

-   [**KeReleaseSpinLockFromDpcLevel**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-kereleasespinlockfromdpclevel)

-   [**KeRemoveByKeyDeviceQueue**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-keremovebykeydevicequeue)

-   [**KeRemoveDeviceQueue**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-keremovedevicequeue)

-   [**PutScatterGatherList**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-pput_scatter_gather_list)

|              |     |
|--------------|-----|
| ドライバー モデル | WDM |

|                                   |                                                                                                                                                                                                                                         |
|-----------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| この規則で見つかったバグ チェック | [**0 xa-チェックをバグします。IRQL\_いない\_少ない\_または\_等しい**](https://docs.microsoft.com/windows-hardware/drivers/debugger/bug-check-0xa--irql-not-less-or-equal) 、 [**チェック 0xC4 のバグします。ドライバー\_VERIFIER\_検出\_違反**](https://docs.microsoft.com/windows-hardware/drivers/debugger/bug-check-0xc4--driver-verifier-detected-violation) (0x00020003) |

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

<table>
<colgroup>
<col width="100%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">実行時に</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>実行<a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/driver-verifier" data-raw-source="[Driver Verifier](https://docs.microsoft.com/windows-hardware/drivers/devtest/driver-verifier)">Driver Verifier</a>を選択し、 <a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/ddi-compliance-checking" data-raw-source="[DDI compliance checking](https://docs.microsoft.com/windows-hardware/drivers/devtest/ddi-compliance-checking)">DDI 準拠の検査</a>オプション。</p></td>
</tr>
</tbody>
</table>

 

<a name="applies-to"></a>適用対象
----------

[**AllocateAdapterChannel**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-pallocate_adapter_channel)
[**AllocateCommonBuffer** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-pallocate_common_buffer) 
 [ **BuildMdlFromScatterGatherList**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-pbuild_mdl_from_scatter_gather_list)
[**BuildScatterGatherList** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-pbuild_scatter_gather_list) 
 [ **FlushAdapterBuffers**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-pflush_adapter_buffers)
[**FreeAdapterChannel**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-pfree_adapter_channel)
[**FreeCommonBuffer** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-pfree_common_buffer) 
 [ **FreeMapRegisters**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-pfree_map_registers)
[**GetDmaAlignment** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-pget_dma_alignment)
 [ **GetScatterGatherList**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-pget_scatter_gather_list)
[**IoAllocateController** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddk/nf-ntddk-ioallocatecontroller) 
[ **IoFreeController**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddk/nf-ntddk-iofreecontroller)
[**います**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-iostartnextpacket) 
[ **IoWriteErrorLogEntry**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-iowriteerrorlogentry)
[**KeInsertByKeyDeviceQueue** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-keinsertbykeydevicequeue)
 [ **KeInsertDeviceQueue**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-keinsertdevicequeue)
[**KeRemoveByKeyDeviceQueue**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-keremovebykeydevicequeue) 
 [ **KeRemoveDeviceQueue**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-keremovedevicequeue)
[**MapTransfer** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-pmap_transfer) 
 [ **PutDmaAdapter**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-pput_dma_adapter)
[**PutScatterGatherList** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-pput_scatter_gather_list) 
 [ **ReadDmaCounter** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-pread_dma_counter)も参照してください
--------

[**ハードウェアの優先度を管理する**](https://docs.microsoft.com/windows-hardware/drivers/kernel/managing-hardware-priorities)
[**スピン ロックの使用中にエラーおよびデッドロックの防止**](https://docs.microsoft.com/windows-hardware/drivers/kernel/preventing-errors-and-deadlocks-while-using-spin-locks)
 

 






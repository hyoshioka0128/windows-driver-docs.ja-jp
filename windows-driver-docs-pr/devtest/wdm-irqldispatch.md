---
title: IrqlDispatch ルール (wdm)
description: IrqlDispatch ルールでは、ドライバーが IRQL DISPATCH_LEVEL で実行されている場合にのみ、次の DDIs を呼び出すように指定します。
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
ms.openlocfilehash: 02e495f881f6ad938a3f8eb1338c7c2b622beb04
ms.sourcegitcommit: 82a9be3b3584f991e5121f8f46a972e04185fa52
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/02/2020
ms.locfileid: "85916852"
---
# <a name="irqldispatch-rule-wdm"></a>IrqlDispatch ルール (wdm)


**Irqldispatch**ルールでは、ドライバーが IRQL = ディスパッチレベルで実行されている場合にのみ、次の DDIs を呼び出すように指定し \_ ます。

-   [**FreeAdapterChannel**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-pfree_adapter_channel)

-   [**FreeMapRegisters**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-pfree_map_registers)

-   [**GetScatterGatherList**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-pget_scatter_gather_list)

-   [**IoAllocateAdapterChannel**](https://docs.microsoft.com/windows-hardware/drivers/kernel/mmcreatemdl)

-   [**IoAllocateController**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/nf-ntddk-ioallocatecontroller)

-   [**IoFreeController**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/nf-ntddk-iofreecontroller)

-   [**IoStartNextPacket**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-iostartnextpacket)

-   [**KeAcquireSpinLockAtDpcLevel**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-keacquirespinlockatdpclevel)

-   [**KeInsertByKeyDeviceQueue**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-keinsertbykeydevicequeue)

-   [**KeInsertDeviceQueue**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-keinsertdevicequeue)

-   [**KeReleaseSpinLockFromDpcLevel**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-kereleasespinlockfromdpclevel)

-   [**KeRemoveByKeyDeviceQueue**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-keremovebykeydevicequeue)

-   [**KeRemoveDeviceQueue**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-keremovedevicequeue)

-   [**PutScatterGatherList**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-pput_scatter_gather_list)

**ドライバーモデル: WDM**

|                                   |                                                                                                                                                                                                                                         |
|-----------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| この規則で見つかったバグ チェック | [**バグチェックの 0xa: IRQL \_\_以下 \_ \_ **](https://docs.microsoft.com/windows-hardware/drivers/debugger/bug-check-0xa--irql-not-less-or-equal) 、[**バグチェック 0xc4: ドライバー \_ 検証ツールで \_ 検出された \_ 違反**](https://docs.microsoft.com/windows-hardware/drivers/debugger/bug-check-0xc4--driver-verifier-detected-violation)(0x00020003) |

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
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/static-driver-verifier" data-raw-source="[Static Driver Verifier](https://docs.microsoft.com/windows-hardware/drivers/devtest/static-driver-verifier)">静的ドライバー検証ツール</a>を実行し、 <strong>irqldispatch</strong>ルールを指定します。</p>
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

[**Allocateadapterchannel**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-pallocate_adapter_channel) 
[**Allocatecommonbuffer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-pallocate_common_buffer) 
[**BuildMdlFromScatterGatherList**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-pbuild_mdl_from_scatter_gather_list) 
[**BuildScatterGatherList**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-pbuild_scatter_gather_list) 
[**Flushadapterbuffers**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-pflush_adapter_buffers) 
[**Freeadapterchannel**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-pfree_adapter_channel) 
[**Freecommonbuffer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-pfree_common_buffer) 
[**FreeMapRegisters**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-pfree_map_registers) 
[**GetDmaAlignment**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-pget_dma_alignment) 
[**GetScatterGatherList**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-pget_scatter_gather_list) 
[**IoAllocateController**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/nf-ntddk-ioallocatecontroller) 
[**IoFreeController**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/nf-ntddk-iofreecontroller) 
[**Iostartnextpacket**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-iostartnextpacket) 
[**Iowriteerrorlogentry**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-iowriteerrorlogentry) 
[**Keinsertbykeydevicequeue**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-keinsertbykeydevicequeue) 
[**Keinsertdevicequeue**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-keinsertdevicequeue) 
[**Keremovebykeydevicequeue**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-keremovebykeydevicequeue) 
[**Keremovedevicequeue**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-keremovedevicequeue) 
[**Maptransfer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-pmap_transfer) 
[**PutDmaAdapter**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-pput_dma_adapter) 
[**PutScatterGatherList**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-pput_scatter_gather_list) 
[**ReadDmaCounter**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-pread_dma_counter)関連項目
--------

[**ハードウェアの優先順位**](https://docs.microsoft.com/windows-hardware/drivers/kernel/managing-hardware-priorities) 
 の管理[**スピンロックを使用しているときのエラーとデッドロックの防止**](https://docs.microsoft.com/windows-hardware/drivers/kernel/preventing-errors-and-deadlocks-while-using-spin-locks)
 

 






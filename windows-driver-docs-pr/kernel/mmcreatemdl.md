---
title: Windows カーネルの古いルーチン
description: Windows カーネルの古いルーチン
ms.assetid: 876f48be-1d8f-4c65-bc84-e35c31919c47
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 2e592898cd7c22aa8b117687ff5ba754dc1108d0
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72827839"
---
# <a name="windows-kernel-obsolete-routines"></a>Windows カーネルの古いルーチン


次の古いルーチンは、既存のバイナリをサポートするためにエクスポートされます。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>廃止されたルーチン</th>
<th>説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><strong>ExAcquireResourceExclusive</strong></td>
<td><p>代わりに<a href="https://msdn.microsoft.com/library/windows/hardware/ff544351" data-raw-source="[&lt;strong&gt;ExAcquireResourceExclusiveLite&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff544351)"><strong>ExAcquireResourceExclusiveLite</strong></a>を使用してください。</p></td>
</tr>
<tr class="even">
<td><strong>ExAcquireResourceShared</strong></td>
<td><p>代わりに<a href="https://msdn.microsoft.com/library/windows/hardware/ff544363" data-raw-source="[&lt;strong&gt;ExAcquireResourceSharedLite&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff544363)"><strong>ExAcquireResourceSharedLite</strong></a>を使用してください。</p></td>
</tr>
<tr class="odd">
<td><strong>ExAllocateFromZone</strong></td>
<td><p>代わりに、ルックアサイドリストを使用してください。 詳細については、「<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/index" data-raw-source="[Buffer Management](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)">バッファー管理</a>」を参照してください。</p></td>
</tr>
<tr class="even">
<td><strong>ExConvertExclusiveToShared</strong></td>
<td><p>代わりに<a href="https://msdn.microsoft.com/library/windows/hardware/ff544558" data-raw-source="[&lt;strong&gt;ExConvertExclusiveToSharedLite&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff544558)"><strong>ExConvertExclusiveToSharedLite</strong></a>を使用してください。</p></td>
</tr>
<tr class="odd">
<td><strong>ExDeleteResource</strong></td>
<td><p>代わりに<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-exdeleteresourcelite" data-raw-source="[&lt;strong&gt;ExDeleteResourceLite&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-exdeleteresourcelite)"><strong>ExDeleteResourceLite</strong></a>を使用してください。</p></td>
</tr>
<tr class="even">
<td><strong>ExExtendZone</strong></td>
<td><p>代わりに、ルックアサイドリストを使用してください。 詳細については、「<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/index" data-raw-source="[Buffer Management](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)">バッファー管理</a>」を参照してください。</p></td>
</tr>
<tr class="odd">
<td><strong>ExFreeToZone</strong></td>
<td><p>代わりに、ルックアサイドリストを使用してください。 詳細については、「<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/index" data-raw-source="[Buffer Management](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)">バッファー管理</a>」を参照してください。</p></td>
</tr>
<tr class="even">
<td><strong>Exinitializer ÷</strong></td>
<td><p>代わりに、 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-exinitializeresourcelite" data-raw-source="[&lt;strong&gt;ExInitializeResourceLite&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-exinitializeresourcelite)"><strong>Exinitializer Eresourcelite</strong></a>を使用してください。</p></td>
</tr>
<tr class="odd">
<td><strong>ExInitializeWorkItem</strong></td>
<td><p>代わりに<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioallocateworkitem" data-raw-source="[&lt;strong&gt;IoAllocateWorkItem&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioallocateworkitem)"><strong>Ioallocateworkitem</strong></a>を使用してください。</p></td>
</tr>
<tr class="even">
<td><strong>ExInitializeZone</strong></td>
<td><p>代わりに、ルックアサイドリストを使用してください。 詳細については、「<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/index" data-raw-source="[Buffer Management](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)">バッファー管理</a>」を参照してください。</p></td>
</tr>
<tr class="odd">
<td><strong>ExInterlockedAllocateFromZone</strong></td>
<td><p>代わりに、ルックアサイドリストを使用してください。 詳細については、「<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/index" data-raw-source="[Buffer Management](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)">バッファー管理</a>」を参照してください。</p></td>
</tr>
<tr class="even">
<td><strong>ExInterlockedDecrementLong</strong></td>
<td><p>代わりに<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-interlockeddecrement" data-raw-source="[&lt;strong&gt;InterlockedDecrement&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-interlockeddecrement)"><strong>InterlockedDecrement</strong></a>を使用してください。</p></td>
</tr>
<tr class="odd">
<td><strong>ExInterlockedExchangeAddLargeInteger</strong></td>
<td><p>2 64 ビット番号をアトミックに追加する方法の詳細については、「 <a href="https://go.microsoft.com/fwlink/p/?linkid=71056" data-raw-source="[InterlockedExchangeAdd64](https://go.microsoft.com/fwlink/p/?linkid=71056)">InterlockedExchangeAdd64</a>」を参照してください。</p></td>
</tr>
<tr class="even">
<td><strong>ExInterlockedExchangeUlong</strong></td>
<td><p>代わりに<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-interlockedexchange" data-raw-source="[&lt;strong&gt;InterlockedExchange&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-interlockedexchange)"><strong>InterlockedExchange</strong></a>を使用してください。</p></td>
</tr>
<tr class="odd">
<td><strong>ExInterlockedExtendZone</strong></td>
<td><p>代わりに、ルックアサイドリストを使用してください。 詳細については、「<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/index" data-raw-source="[Buffer Management](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)">バッファー管理</a>」を参照してください。</p></td>
</tr>
<tr class="even">
<td><strong>ExInterlockedFreeToZone</strong></td>
<td><p>代わりに、ルックアサイドリストを使用してください。 詳細については、「<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/index" data-raw-source="[Buffer Management](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)">バッファー管理</a>」を参照してください。</p></td>
</tr>
<tr class="odd">
<td><strong>ExInterlockedIncrementLong</strong></td>
<td><p>代わりに<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-interlockedincrement" data-raw-source="[&lt;strong&gt;InterlockedIncrement&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-interlockedincrement)"><strong>InterlockedIncrement</strong></a>を使用してください。</p></td>
</tr>
<tr class="even">
<td><strong>ExIsFullZone</strong></td>
<td><p>代わりに、ルックアサイドリストを使用してください。 詳細については、「<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/index" data-raw-source="[Buffer Management](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)">バッファー管理</a>」を参照してください。</p></td>
</tr>
<tr class="odd">
<td><strong>ExIsObjectInFirstZoneSegment</strong></td>
<td><p>代わりに、ルックアサイドリストを使用してください。 詳細については、「<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/index" data-raw-source="[Buffer Management](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)">バッファー管理</a>」を参照してください。</p></td>
</tr>
<tr class="even">
<td><strong>ExIsResourceAcquired</strong></td>
<td><p>代わりに<a href="https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff545466(v=vs.85)" data-raw-source="[&lt;strong&gt;ExIsResourceAcquiredLite&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff545466(v=vs.85))"><strong>ExIsResourceAcquiredLite</strong></a>を使用してください。</p></td>
</tr>
<tr class="odd">
<td><strong>ExIsResourceAcquiredExclusive</strong></td>
<td><p>代わりに<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-exisresourceacquiredexclusivelite" data-raw-source="[&lt;strong&gt;ExIsResourceAcquiredExclusiveLite&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-exisresourceacquiredexclusivelite)"><strong>ExIsResourceAcquiredExclusiveLite</strong></a>を使用してください。</p></td>
</tr>
<tr class="even">
<td><strong>ExIsResourceAcquiredShared</strong></td>
<td><p>代わりに<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-exisresourceacquiredsharedlite" data-raw-source="[&lt;strong&gt;ExIsResourceAcquiredSharedLite&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-exisresourceacquiredsharedlite)"><strong>ExIsResourceAcquiredSharedLite</strong></a>を使用してください。</p></td>
</tr>
<tr class="odd">
<td><strong>ExReleaseResource</strong></td>
<td><p>代わりに<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-exreleaseresourcelite" data-raw-source="[&lt;strong&gt;ExReleaseResourceLite&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-exreleaseresourcelite)"><strong>ExReleaseResourceLite</strong></a>を使用してください。</p></td>
</tr>
<tr class="even">
<td><strong>ExReleaseResourceForThread</strong></td>
<td><p>代わりに<a href="https://msdn.microsoft.com/library/windows/hardware/ff545585" data-raw-source="[&lt;strong&gt;ExReleaseResourceForThreadLite&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff545585)"><strong>ExReleaseResourceForThreadLite</strong></a>を使用してください。</p></td>
</tr>
<tr class="odd">
<td><strong>IoAllocateAdapterChannel</strong></td>
<td><p>代わりに、 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-pallocate_adapter_channel" data-raw-source="[&lt;strong&gt;AllocateAdapterChannel&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-pallocate_adapter_channel)"><strong>Allocateadapterchannel</strong></a>を使用してください。</p></td>
</tr>
<tr class="even">
<td><strong>Io割り当てリソース</strong></td>
<td><p>PnP デバイスのドライバーには、PnP マネージャーによってリソースが割り当てられます。 PnP マネージャーは、各<a href="https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-start-device" data-raw-source="[&lt;strong&gt;IRP_MN_START_DEVICE&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-start-device)"><strong>IRP_MN_START_DEVICE</strong></a>要求と共にリソースリストを渡します。 PnP マネージャーで列挙できないレガシデバイスをサポートする必要があるドライバーは、代わりに<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/nf-ntddk-ioreportdetecteddevice" data-raw-source="[&lt;strong&gt;IoReportDetectedDevice&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/nf-ntddk-ioreportdetecteddevice)"><strong>IoReportDetectedDevice</strong></a>と<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/nf-ntddk-ioreportresourcefordetection" data-raw-source="[&lt;strong&gt;IoReportResourceForDetection&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/nf-ntddk-ioreportresourcefordetection)"><strong>IoReportResourceForDetection</strong></a>を使用する必要があります。</p></td>
</tr>
<tr class="odd">
<td><strong>IoAttachDeviceByPointer</strong></td>
<td><p>代わりに<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioattachdevicetodevicestack" data-raw-source="[&lt;strong&gt;IoAttachDeviceToDeviceStack&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioattachdevicetodevicestack)"><strong>Ioattachdevicetodevicestack</strong></a>を使用してください。</p></td>
</tr>
<tr class="even">
<td><strong>Ioflのアダプターバッファー</strong></td>
<td><p>代わりに<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-pflush_adapter_buffers" data-raw-source="[&lt;strong&gt;FlushAdapterBuffers&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-pflush_adapter_buffers)"><strong>Flushadapterbuffers</strong></a>を使用してください。</p></td>
</tr>
<tr class="odd">
<td><strong>IoFreeAdapterChannel</strong></td>
<td><p>代わりに<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-pfree_adapter_channel" data-raw-source="[&lt;strong&gt;FreeAdapterChannel&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-pfree_adapter_channel)"><strong>Freeadapterchannel</strong></a>を使用してください。</p></td>
</tr>
<tr class="even">
<td><strong>IoFreeMapRegisters</strong></td>
<td><p>代わりに<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-pfree_map_registers" data-raw-source="[&lt;strong&gt;FreeMapRegisters&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-pfree_map_registers)"><strong>FreeMapRegisters</strong></a>を使用してください。</p></td>
</tr>
<tr class="odd">
<td><strong>IoMapTransfer</strong></td>
<td><p>代わりに<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-pmap_transfer" data-raw-source="[&lt;strong&gt;MapTransfer&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-pmap_transfer)"><strong>Maptransfer</strong></a>を使用してください。</p></td>
</tr>
<tr class="even">
<td><strong>IoQueryDeviceDescription</strong></td>
<td><p>このルーチンは、指定されたバス、コントローラー、または周辺機器オブジェクトに関するハードウェア構成情報を取得します。または、 <strong>\Registry\Machine\Hardware\Description</strong>ツリーからこれら3種類の任意の組み合わせを取得します。 ハードウェア構成情報を必要とするドライバーでは、 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iogetdeviceproperty" data-raw-source="[&lt;strong&gt;IoGetDeviceProperty&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iogetdeviceproperty)"><strong>Iogetdeviceproperty</strong></a>を使用する必要があります。</p></td>
</tr>
<tr class="odd">
<td><strong>IoReportResourceUsage</strong></td>
<td><p>このルーチンは、割り込みベクター、デバイスメモリ範囲、または<strong>\Registry\Machine\Hardware\ResourceMap</strong>ツリー内の特定の DMA コントローラーチャネルなどのハードウェアリソースを要求します。これにより、後で読み込まれるドライバーは同じものを使用できなくなります。参考. 新しいドライバーが、PnP で列挙されていないレガシデバイスをサポートする必要がある場合、ドライバーは<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/nf-ntddk-ioreportresourcefordetection" data-raw-source="[&lt;strong&gt;IoReportResourceForDetection&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/nf-ntddk-ioreportresourcefordetection)"><strong>IoReportResourceForDetection</strong></a>を呼び出してデバイスのリソースを要求する必要があります。</p></td>
</tr>
<tr class="even">
<td><strong>KeGetDcacheFillSize</strong></td>
<td><p>ドライバーは代わりに<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-pget_dma_alignment" data-raw-source="[&lt;strong&gt;GetDmaAlignment&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-pget_dma_alignment)"><strong>GetDmaAlignment</strong></a>を呼び出す必要があります。</p></td>
</tr>
<tr class="odd">
<td><strong>MmCreateMdl</strong></td>
<td><p>代わりに<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioallocatemdl" data-raw-source="[&lt;strong&gt;IoAllocateMdl&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioallocatemdl)"><strong>IoAllocateMdl</strong></a>を使用してください。</p></td>
</tr>
<tr class="even">
<td><strong>MmIsNonPagedSystemAddressValid</strong></td>
<td></td>
</tr>
</tbody>
</table>

 

## <a name="related-topics"></a>関連トピック
[**AllocateAdapterChannel**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-pallocate_adapter_channel)  
[バッファー管理](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)  
[**ExAcquireResourceExclusiveLite**](https://msdn.microsoft.com/library/windows/hardware/ff544351)  
[**ExAcquireResourceSharedLite**](https://msdn.microsoft.com/library/windows/hardware/ff544363)  
[**ExConvertExclusiveToSharedLite**](https://msdn.microsoft.com/library/windows/hardware/ff544558)  
[**ExDeleteResourceLite**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-exdeleteresourcelite)  
[**Ex/Eresourcelite**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-exinitializeresourcelite)  
[**ExIsResourceAcquiredExclusiveLite**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-exisresourceacquiredexclusivelite)  
[**ExIsResourceAcquiredSharedLite**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-exisresourceacquiredsharedlite)  
[**ExReleaseResourceForThreadLite**](https://msdn.microsoft.com/library/windows/hardware/ff545585)  
[**ExReleaseResourceLite**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-exreleaseresourcelite)  
[**InterlockedDecrement**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-interlockeddecrement)  
[**InterlockedExchange**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-interlockedexchange)  
[**InterlockedIncrement**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-interlockedincrement)  
[**FlushAdapterBuffers**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-pflush_adapter_buffers)  
[**FreeAdapterChannel**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-pfree_adapter_channel)  
[**FreeMapRegisters**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-pfree_map_registers)  
[**GetDmaAlignment**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-pget_dma_alignment)  
[InterlockedExchangeAdd64](https://go.microsoft.com/fwlink/p/?linkid=71056)  
[**IoAllocateMdl**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioallocatemdl)  
[**IoAllocateWorkItem**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioallocateworkitem)  
[**IoAttachDeviceToDeviceStack**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioattachdevicetodevicestack)  
[**IoGetDeviceProperty**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iogetdeviceproperty)  
[**IoReportDetectedDevice**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/nf-ntddk-ioreportdetecteddevice)  
[**IoReportResourceForDetection**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/nf-ntddk-ioreportresourcefordetection)  
[ **\_デバイスを起動\_IRP\_** ](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-start-device)  
[**MapTransfer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-pmap_transfer)  




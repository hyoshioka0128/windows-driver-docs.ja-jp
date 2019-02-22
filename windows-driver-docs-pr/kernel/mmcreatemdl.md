---
title: Windows カーネルの廃止ルーチン
description: Windows カーネルの廃止ルーチン
ms.assetid: 876f48be-1d8f-4c65-bc84-e35c31919c47
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 3c246e05794e8793a15c3bf30e5fd09b5130cacc
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56552881"
---
# <a name="windows-kernel-obsolete-routines"></a>Windows カーネルの廃止ルーチン


既存のバイナリをサポートするために、次の古いルーチンがエクスポートされます。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>古いルーチン</th>
<th>説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><strong>ExAcquireResourceExclusive</strong></td>
<td><p>使用<a href="https://msdn.microsoft.com/library/windows/hardware/ff544351" data-raw-source="[&lt;strong&gt;ExAcquireResourceExclusiveLite&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff544351)"> <strong>ExAcquireResourceExclusiveLite</strong> </a>代わりにします。</p></td>
</tr>
<tr class="even">
<td><strong>ExAcquireResourceShared</strong></td>
<td><p>使用<a href="https://msdn.microsoft.com/library/windows/hardware/ff544363" data-raw-source="[&lt;strong&gt;ExAcquireResourceSharedLite&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff544363)"> <strong>ExAcquireResourceSharedLite</strong> </a>代わりにします。</p></td>
</tr>
<tr class="odd">
<td><strong>ExAllocateFromZone</strong></td>
<td><p>ルック アサイド リストを使用してください。 詳細については、次を参照してください。<a href="https://msdn.microsoft.com/library/windows/hardware/ff540667" data-raw-source="[Buffer Management](https://msdn.microsoft.com/library/windows/hardware/ff540667)">バッファー管理</a>します。</p></td>
</tr>
<tr class="even">
<td><strong>ExConvertExclusiveToShared</strong></td>
<td><p>使用<a href="https://msdn.microsoft.com/library/windows/hardware/ff544558" data-raw-source="[&lt;strong&gt;ExConvertExclusiveToSharedLite&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff544558)"> <strong>ExConvertExclusiveToSharedLite</strong> </a>代わりにします。</p></td>
</tr>
<tr class="odd">
<td><strong>ExDeleteResource</strong></td>
<td><p>使用<a href="https://msdn.microsoft.com/library/windows/hardware/ff544578" data-raw-source="[&lt;strong&gt;ExDeleteResourceLite&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff544578)"> <strong>ExDeleteResourceLite</strong> </a>代わりにします。</p></td>
</tr>
<tr class="even">
<td><strong>ExExtendZone</strong></td>
<td><p>ルック アサイド リストを使用してください。 詳細については、次を参照してください。<a href="https://msdn.microsoft.com/library/windows/hardware/ff540667" data-raw-source="[Buffer Management](https://msdn.microsoft.com/library/windows/hardware/ff540667)">バッファー管理</a>します。</p></td>
</tr>
<tr class="odd">
<td><strong>ExFreeToZone</strong></td>
<td><p>ルック アサイド リストを使用してください。 詳細については、次を参照してください。<a href="https://msdn.microsoft.com/library/windows/hardware/ff540667" data-raw-source="[Buffer Management](https://msdn.microsoft.com/library/windows/hardware/ff540667)">バッファー管理</a>します。</p></td>
</tr>
<tr class="even">
<td><strong>ExInitializeResource</strong></td>
<td><p>使用<a href="https://msdn.microsoft.com/library/windows/hardware/ff545317" data-raw-source="[&lt;strong&gt;ExInitializeResourceLite&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff545317)"> <strong>ExInitializeResourceLite</strong> </a>代わりにします。</p></td>
</tr>
<tr class="odd">
<td><strong>ExInitializeWorkItem</strong></td>
<td><p>使用<a href="https://msdn.microsoft.com/library/windows/hardware/ff548276" data-raw-source="[&lt;strong&gt;IoAllocateWorkItem&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff548276)"> <strong>IoAllocateWorkItem</strong> </a>代わりにします。</p></td>
</tr>
<tr class="even">
<td><strong>ExInitializeZone</strong></td>
<td><p>ルック アサイド リストを使用してください。 詳細については、次を参照してください。<a href="https://msdn.microsoft.com/library/windows/hardware/ff540667" data-raw-source="[Buffer Management](https://msdn.microsoft.com/library/windows/hardware/ff540667)">バッファー管理</a>します。</p></td>
</tr>
<tr class="odd">
<td><strong>ExInterlockedAllocateFromZone</strong></td>
<td><p>ルック アサイド リストを使用してください。 詳細については、次を参照してください。<a href="https://msdn.microsoft.com/library/windows/hardware/ff540667" data-raw-source="[Buffer Management](https://msdn.microsoft.com/library/windows/hardware/ff540667)">バッファー管理</a>します。</p></td>
</tr>
<tr class="even">
<td><strong>ExInterlockedDecrementLong</strong></td>
<td><p>使用<a href="https://msdn.microsoft.com/library/windows/hardware/ff547871" data-raw-source="[&lt;strong&gt;InterlockedDecrement&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff547871)"> <strong>InterlockedDecrement</strong> </a>代わりにします。</p></td>
</tr>
<tr class="odd">
<td><strong>ExInterlockedExchangeAddLargeInteger</strong></td>
<td><p>2 つの 64 ビットの数値をアトミックに追加する方法の詳細については、次を参照してください。 <a href="https://go.microsoft.com/fwlink/p/?linkid=71056" data-raw-source="[InterlockedExchangeAdd64](https://go.microsoft.com/fwlink/p/?linkid=71056)">InterlockedExchangeAdd64</a>します。</p></td>
</tr>
<tr class="even">
<td><strong>ExInterlockedExchangeUlong</strong></td>
<td><p>使用<a href="https://msdn.microsoft.com/library/windows/hardware/ff547892" data-raw-source="[&lt;strong&gt;InterlockedExchange&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff547892)"> <strong>InterlockedExchange</strong> </a>代わりにします。</p></td>
</tr>
<tr class="odd">
<td><strong>ExInterlockedExtendZone</strong></td>
<td><p>ルック アサイド リストを使用してください。 詳細については、次を参照してください。<a href="https://msdn.microsoft.com/library/windows/hardware/ff540667" data-raw-source="[Buffer Management](https://msdn.microsoft.com/library/windows/hardware/ff540667)">バッファー管理</a>します。</p></td>
</tr>
<tr class="even">
<td><strong>ExInterlockedFreeToZone</strong></td>
<td><p>ルック アサイド リストを使用してください。 詳細については、次を参照してください。<a href="https://msdn.microsoft.com/library/windows/hardware/ff540667" data-raw-source="[Buffer Management](https://msdn.microsoft.com/library/windows/hardware/ff540667)">バッファー管理</a>します。</p></td>
</tr>
<tr class="odd">
<td><strong>ExInterlockedIncrementLong</strong></td>
<td><p>使用<a href="https://msdn.microsoft.com/library/windows/hardware/ff547910" data-raw-source="[&lt;strong&gt;InterlockedIncrement&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff547910)"> <strong>InterlockedIncrement</strong> </a>代わりにします。</p></td>
</tr>
<tr class="even">
<td><strong>ExIsFullZone</strong></td>
<td><p>ルック アサイド リストを使用してください。 詳細については、次を参照してください。<a href="https://msdn.microsoft.com/library/windows/hardware/ff540667" data-raw-source="[Buffer Management](https://msdn.microsoft.com/library/windows/hardware/ff540667)">バッファー管理</a>します。</p></td>
</tr>
<tr class="odd">
<td><strong>ExIsObjectInFirstZoneSegment</strong></td>
<td><p>ルック アサイド リストを使用してください。 詳細については、次を参照してください。<a href="https://msdn.microsoft.com/library/windows/hardware/ff540667" data-raw-source="[Buffer Management](https://msdn.microsoft.com/library/windows/hardware/ff540667)">バッファー管理</a>します。</p></td>
</tr>
<tr class="even">
<td><strong>ExIsResourceAcquired</strong></td>
<td><p>使用<a href="https://msdn.microsoft.com/library/windows/hardware/ff545466" data-raw-source="[&lt;strong&gt;ExIsResourceAcquiredLite&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff545466)"> <strong>ExIsResourceAcquiredLite</strong> </a>代わりにします。</p></td>
</tr>
<tr class="odd">
<td><strong>ExIsResourceAcquiredExclusive</strong></td>
<td><p>使用<a href="https://msdn.microsoft.com/library/windows/hardware/ff545458" data-raw-source="[&lt;strong&gt;ExIsResourceAcquiredExclusiveLite&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff545458)"> <strong>ExIsResourceAcquiredExclusiveLite</strong> </a>代わりにします。</p></td>
</tr>
<tr class="even">
<td><strong>ExIsResourceAcquiredShared</strong></td>
<td><p>使用<a href="https://msdn.microsoft.com/library/windows/hardware/ff545477" data-raw-source="[&lt;strong&gt;ExIsResourceAcquiredSharedLite&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff545477)"> <strong>ExIsResourceAcquiredSharedLite</strong> </a>代わりにします。</p></td>
</tr>
<tr class="odd">
<td><strong>ExReleaseResource</strong></td>
<td><p>使用<a href="https://msdn.microsoft.com/library/windows/hardware/ff545597" data-raw-source="[&lt;strong&gt;ExReleaseResourceLite&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff545597)"> <strong>ExReleaseResourceLite</strong> </a>代わりにします。</p></td>
</tr>
<tr class="even">
<td><strong>ExReleaseResourceForThread</strong></td>
<td><p>使用<a href="https://msdn.microsoft.com/library/windows/hardware/ff545585" data-raw-source="[&lt;strong&gt;ExReleaseResourceForThreadLite&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff545585)"> <strong>ExReleaseResourceForThreadLite</strong> </a>代わりにします。</p></td>
</tr>
<tr class="odd">
<td><strong>IoAllocateAdapterChannel</strong></td>
<td><p>使用<a href="https://msdn.microsoft.com/library/windows/hardware/ff540573" data-raw-source="[&lt;strong&gt;AllocateAdapterChannel&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff540573)"> <strong>AllocateAdapterChannel</strong> </a>代わりにします。</p></td>
</tr>
<tr class="even">
<td><strong>IoAssignResources</strong></td>
<td><p>PnP デバイスのドライバーは、各リソースの一覧を通過する PnP マネージャーでリソースを割り当てられている<a href="https://msdn.microsoft.com/library/windows/hardware/ff551749" data-raw-source="[&lt;strong&gt;IRP_MN_START_DEVICE&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff551749)"> <strong>IRP_MN_START_DEVICE</strong> </a>要求。 PnP マネージャーによって列挙できないレガシ デバイスをサポートする必要があるドライバーを使用する必要があります<a href="https://msdn.microsoft.com/library/windows/hardware/ff549597" data-raw-source="[&lt;strong&gt;IoReportDetectedDevice&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff549597)"> <strong>IoReportDetectedDevice</strong> </a>と<a href="https://msdn.microsoft.com/library/windows/hardware/ff549608" data-raw-source="[&lt;strong&gt;IoReportResourceForDetection&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff549608)"> <strong>IoReportResourceForDetection</strong> </a>代わりにします。</p></td>
</tr>
<tr class="odd">
<td><strong>IoAttachDeviceByPointer</strong></td>
<td><p>使用<a href="https://msdn.microsoft.com/library/windows/hardware/ff548300" data-raw-source="[&lt;strong&gt;IoAttachDeviceToDeviceStack&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff548300)"> <strong>IoAttachDeviceToDeviceStack</strong> </a>代わりにします。</p></td>
</tr>
<tr class="even">
<td><strong>IoFlushAdapterBuffers</strong></td>
<td><p>使用<a href="https://msdn.microsoft.com/library/windows/hardware/ff545917" data-raw-source="[&lt;strong&gt;FlushAdapterBuffers&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff545917)"> <strong>FlushAdapterBuffers</strong> </a>代わりにします。</p></td>
</tr>
<tr class="odd">
<td><strong>IoFreeAdapterChannel</strong></td>
<td><p>使用<a href="https://msdn.microsoft.com/library/windows/hardware/ff546507" data-raw-source="[&lt;strong&gt;FreeAdapterChannel&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff546507)"> <strong>FreeAdapterChannel</strong> </a>代わりにします。</p></td>
</tr>
<tr class="even">
<td><strong>IoFreeMapRegisters</strong></td>
<td><p>使用<a href="https://msdn.microsoft.com/library/windows/hardware/ff546513" data-raw-source="[&lt;strong&gt;FreeMapRegisters&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff546513)"> <strong>FreeMapRegisters</strong> </a>代わりにします。</p></td>
</tr>
<tr class="odd">
<td><strong>IoMapTransfer</strong></td>
<td><p>使用<a href="https://msdn.microsoft.com/library/windows/hardware/ff554402" data-raw-source="[&lt;strong&gt;MapTransfer&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff554402)"> <strong>MapTransfer</strong> </a>代わりにします。</p></td>
</tr>
<tr class="even">
<td><strong>IoQueryDeviceDescription</strong></td>
<td><p>このルーチンは、バス、コント ローラーまたは周辺のオブジェクトに関するハードウェアの構成情報を取得します。 または、これらの 3 つの任意の組み合わせから型の、 <strong>\Registry\Machine\Hardware\Description</strong>ツリー。 ハードウェア構成情報が必要なドライバーを使用する必要があります<a href="https://msdn.microsoft.com/library/windows/hardware/ff549203" data-raw-source="[&lt;strong&gt;IoGetDeviceProperty&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff549203)"> <strong>IoGetDeviceProperty</strong> </a>代わりにします。</p></td>
</tr>
<tr class="odd">
<td><strong>IoReportResourceUsage</strong></td>
<td><p>このルーチンは、割り込みベクター、デバイスのメモリ範囲で、特定の DMA コント ローラー チャネルなどのハードウェア リソースを要求、 <strong>\Registry\Machine\Hardware\ResourceMap</strong>ツリー、読み込まれた後でドライバーができないように同じリソースを使用しようとしてください。 新しいドライバーは、PnP 列挙可能なないレガシ デバイスをサポートする必要がある場合、ドライバーを呼び出す必要があります<a href="https://msdn.microsoft.com/library/windows/hardware/ff549608" data-raw-source="[&lt;strong&gt;IoReportResourceForDetection&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff549608)"> <strong>IoReportResourceForDetection</strong> </a>デバイスのリソースを要求します。</p></td>
</tr>
<tr class="even">
<td><strong>KeGetDcacheFillSize</strong></td>
<td><p>ドライバーを呼び出す必要があります<a href="https://msdn.microsoft.com/library/windows/hardware/ff546530" data-raw-source="[&lt;strong&gt;GetDmaAlignment&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff546530)"> <strong>GetDmaAlignment</strong> </a>代わりにします。</p></td>
</tr>
<tr class="odd">
<td><strong>MmCreateMdl</strong></td>
<td><p>使用<a href="https://msdn.microsoft.com/library/windows/hardware/ff548263" data-raw-source="[&lt;strong&gt;IoAllocateMdl&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff548263)"> <strong>IoAllocateMdl</strong> </a>代わりにします。</p></td>
</tr>
<tr class="even">
<td><strong>MmIsNonPagedSystemAddressValid</strong></td>
<td></td>
</tr>
</tbody>
</table>

 

## <a name="related-topics"></a>関連トピック
[**AllocateAdapterChannel**](https://msdn.microsoft.com/library/windows/hardware/ff540573)  
[バッファー管理](https://msdn.microsoft.com/library/windows/hardware/ff540667)  
[**ExAcquireResourceExclusiveLite**](https://msdn.microsoft.com/library/windows/hardware/ff544351)  
[**ExAcquireResourceSharedLite**](https://msdn.microsoft.com/library/windows/hardware/ff544363)  
[**ExConvertExclusiveToSharedLite**](https://msdn.microsoft.com/library/windows/hardware/ff544558)  
[**ExDeleteResourceLite**](https://msdn.microsoft.com/library/windows/hardware/ff544578)  
[**ExInitializeResourceLite**](https://msdn.microsoft.com/library/windows/hardware/ff545317)  
[**ExIsResourceAcquiredExclusiveLite**](https://msdn.microsoft.com/library/windows/hardware/ff545458)  
[**ExIsResourceAcquiredSharedLite**](https://msdn.microsoft.com/library/windows/hardware/ff545477)  
[**ExReleaseResourceForThreadLite**](https://msdn.microsoft.com/library/windows/hardware/ff545585)  
[**ExReleaseResourceLite**](https://msdn.microsoft.com/library/windows/hardware/ff545597)  
[**InterlockedDecrement**](https://msdn.microsoft.com/library/windows/hardware/ff547871)  
[**InterlockedExchange**](https://msdn.microsoft.com/library/windows/hardware/ff547892)  
[**InterlockedIncrement**](https://msdn.microsoft.com/library/windows/hardware/ff547910)  
[**FlushAdapterBuffers**](https://msdn.microsoft.com/library/windows/hardware/ff545917)  
[**FreeAdapterChannel**](https://msdn.microsoft.com/library/windows/hardware/ff546507)  
[**FreeMapRegisters**](https://msdn.microsoft.com/library/windows/hardware/ff546513)  
[**GetDmaAlignment**](https://msdn.microsoft.com/library/windows/hardware/ff546530)  
[InterlockedExchangeAdd64](https://go.microsoft.com/fwlink/p/?linkid=71056)  
[**IoAllocateMdl**](https://msdn.microsoft.com/library/windows/hardware/ff548263)  
[**IoAllocateWorkItem**](https://msdn.microsoft.com/library/windows/hardware/ff548276)  
[**IoAttachDeviceToDeviceStack**](https://msdn.microsoft.com/library/windows/hardware/ff548300)  
[**IoGetDeviceProperty**](https://msdn.microsoft.com/library/windows/hardware/ff549203)  
[**IoReportDetectedDevice**](https://msdn.microsoft.com/library/windows/hardware/ff549597)  
[**IoReportResourceForDetection**](https://msdn.microsoft.com/library/windows/hardware/ff549608)  
[**IRP\_MN\_START\_DEVICE**](https://msdn.microsoft.com/library/windows/hardware/ff551749)  
[**MapTransfer**](https://msdn.microsoft.com/library/windows/hardware/ff554402)  




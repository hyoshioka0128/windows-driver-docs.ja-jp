---
title: メモリ使用の規則セット (NDIS)
description: これらの規則を使用すると、ドライバーが正しく割り当てし、メモリを解放するのに NDIS 関数を呼び出すことを確認します。
ms.assetid: F28314C6-4B4D-479F-BB96-6850C8F98153
ms.date: 05/21/2018
ms.localizationpriority: medium
ms.openlocfilehash: e9de9dadaf10539fda1b9774d6b9c078814e0b01
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67354766"
---
# <a name="memory-usage-rule-set-ndis"></a>メモリ使用の規則セット (NDIS)


これらの規則を使用すると、ドライバーが正しく割り当てし、メモリを解放するのに NDIS 関数を呼び出すことを確認します。

## <a name="in-this-section"></a>このセクションの内容


<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">トピック</th>
<th align="left">説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><a href="ndis-ndisallocategenericobject.md" data-raw-source="[&lt;strong&gt;NdisAllocateGenericObject&lt;/strong&gt;](ndis-ndisallocategenericobject.md)"><strong>NdisAllocateGenericObject</strong></a></p></td>
<td align="left"><p><a href="ndis-ndisallocategenericobject.md" data-raw-source="[&lt;strong&gt;NdisAllocateGenericObject&lt;/strong&gt;](ndis-ndisallocategenericobject.md)"> <strong>NdisAllocateGenericObject</strong> </a>ルールを指定する<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisallocategenericobject" data-raw-source="[&lt;strong&gt;NdisAllocateGenericObject&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisallocategenericobject)"> <strong>NdisAllocateGenericObject</strong> </a>と<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisfreegenericobject" data-raw-source="[&lt;strong&gt;NdisFreeGenericObject&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisfreegenericobject)"> <strong>NdisFreeGenericObject</strong> </a>代替の順序で呼び出されます。 最終的な目標はすべてジェネリック オブジェクトが解放されるかどうかを確認するときに<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_halt" data-raw-source="[&lt;em&gt;MiniportHaltEx&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_halt)"> <em>MiniportHaltEx</em> </a>が終了します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="ndis-ndisallocatemdl.md" data-raw-source="[&lt;strong&gt;NdisAllocateMdl&lt;/strong&gt;](ndis-ndisallocatemdl.md)"><strong>NdisAllocateMdl</strong></a></p></td>
<td align="left"><p><a href="ndis-ndisallocatemdl.md" data-raw-source="[&lt;strong&gt;NdisAllocateMdl&lt;/strong&gt;](ndis-ndisallocatemdl.md)"> <strong>NdisAllocateMdl</strong> </a>ルールを指定する<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisallocatemdl" data-raw-source="[&lt;strong&gt;NdisAllocateMdl&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisallocatemdl)"> <strong>NdisAllocateMdl</strong> </a>と<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisfreemdl" data-raw-source="[&lt;strong&gt;NdisFreeMdl&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisfreemdl)"> <strong>NdisFreeMdl</strong></a>代替の順序で呼び出されます。 最終的な目標はすべて MDLs いることを確認するときに解放される<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_halt" data-raw-source="[&lt;em&gt;MiniportHaltEx&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_halt)"> <em>MiniportHaltEx</em> </a>が終了します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="ndis-ndisallocatememorywithtagpriority.md" data-raw-source="[&lt;strong&gt;NdisAllocateMemoryWithTagPriority&lt;/strong&gt;](ndis-ndisallocatememorywithtagpriority.md)"><strong>NdisAllocateMemoryWithTagPriority</strong></a></p></td>
<td align="left"><p><a href="ndis-ndisallocatememorywithtagpriority.md" data-raw-source="[&lt;strong&gt;NdisAllocateMemoryWithTagPriority&lt;/strong&gt;](ndis-ndisallocatememorywithtagpriority.md)"> <strong>NdisAllocateMemoryWithTagPriority</strong> </a>ルールでは、ドライバーを呼び出してはならないことを指定します<strong>NdisAllocateMemoryWithTagPriority</strong>提供せず、 <em>タグ</em>します。</p>
<p>すべてのメモリ割り当ては、カーネル デバッガーやドライバーの検証ツールが、個別に割り当てられたメモリ ブロックを識別することができますを確実に一意のプール タグを使用してください。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="ndis-ndisallocatenetbuffer.md" data-raw-source="[&lt;strong&gt;NdisAllocateNetBuffer&lt;/strong&gt;](ndis-ndisallocatenetbuffer.md)"><strong>NdisAllocateNetBuffer</strong></a></p></td>
<td align="left"><p><a href="ndis-ndisallocatenetbuffer.md" data-raw-source="[&lt;strong&gt;NdisAllocateNetBuffer&lt;/strong&gt;](ndis-ndisallocatenetbuffer.md)"> <strong>NdisAllocateNetBuffer</strong> </a>ルールを指定する<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisallocatenetbuffer" data-raw-source="[&lt;strong&gt;NdisAllocateNetBuffer&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisallocatenetbuffer)"> <strong>NdisAllocateNetBuffer</strong> </a>と<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisfreenetbuffer" data-raw-source="[&lt;strong&gt;NdisFreeNetBuffer&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisfreenetbuffer)"> <strong>NdisFreeNetBuffer</strong> </a>代替の順序で呼び出されます。 すべてのインスタンスを確認する最終目標は、 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_net_buffer" data-raw-source="[&lt;strong&gt;NET_BUFFER&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_net_buffer)"> <strong>NET_BUFFER</strong> </a>ときに解放される<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_halt" data-raw-source="[&lt;em&gt;MiniportHaltEx&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_halt)"> <em>MiniportHaltEx</em> </a>が終了します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="ndis-ndismfreesharedmemory.md" data-raw-source="[&lt;strong&gt;NdisMFreeSharedMemory&lt;/strong&gt;](ndis-ndismfreesharedmemory.md)"><strong>NdisMFreeSharedMemory</strong></a></p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismfreesharedmemory" data-raw-source="[&lt;strong&gt;NdisMFreeSharedMemory&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismfreesharedmemory)"><strong>NdisMFreeSharedMemory</strong> </a>から呼び出すことはできません、 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_shutdown" data-raw-source="[&lt;em&gt;MiniportShutdownEx&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_shutdown)"> <em>MiniportShutdownEx</em> </a>関数。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="ndis-ndismindicatestatusex.md" data-raw-source="[&lt;strong&gt;NdisMIndicateStatusEx&lt;/strong&gt;](ndis-ndismindicatestatusex.md)"><strong>NdisMIndicateStatusEx</strong></a></p></td>
<td align="left"><p>ドライバーを呼び出してはならない<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismindicatestatusex" data-raw-source="[&lt;strong&gt;NdisMIndicateStatusEx&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismindicatestatusex)"> <strong>NdisMIndicateStatusEx</strong> </a>から戻った後に、 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_halt" data-raw-source="[&lt;em&gt;MiniportHaltEx&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_halt)"> <em>MiniportHaltEx</em> </a>関数。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="ndis-ndismmapiospace.md" data-raw-source="[&lt;strong&gt;NdisMMapIoSpace&lt;/strong&gt;](ndis-ndismmapiospace.md)"><strong>NdisMMapIoSpace</strong></a></p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismmapiospace" data-raw-source="[&lt;strong&gt;NdisMMapIoSpace&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismmapiospace)"> <strong>NdisMMapIoSpace</strong> </a>関数のみのコンテキストで呼び出されます<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_initialize" data-raw-source="[&lt;em&gt;MiniportInitializeEx&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_initialize)"> <em>MiniportInitializeEx</em></a>します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="ndis-ndismregisterioportrange.md" data-raw-source="[&lt;strong&gt;NdisMRegisterIoPortRange&lt;/strong&gt;](ndis-ndismregisterioportrange.md)"><strong>NdisMRegisterIoPortRange</strong></a></p></td>
<td align="left"><p>ミニポート ドライバーは呼び出し<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismregisterioportrange" data-raw-source="[&lt;strong&gt;NdisMRegisterIoPortRange&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismregisterioportrange)"> <strong>NdisMRegisterIoPortRange</strong> </a>からその<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_initialize" data-raw-source="[&lt;em&gt;MiniportInitializeEx&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_initialize)"> <em>MiniportInitializeEx</em> </a>または MINIPORT_ADD_DEVICE 関数。 <em>MiniportInitializeEx</em> MINIPORT_ADD_DEVICE を呼び出す必要がありますまたは<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismsetminiportattributes" data-raw-source="[&lt;strong&gt;NdisMSetMiniportAttributes&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismsetminiportattributes)"> <strong>NdisMSetMiniportAttributes</strong> </a>呼び出す前に<strong>NdisMRegisterIoPortRange</strong>します。</p></td>
</tr>
</tbody>
</table>

 

**メモリ使用量のルールを選択するには、次のように設定します。**

1.  Microsoft Visual Studio で、ドライバーのプロジェクト (.vcxProj) を選択します。 **ドライバー**  メニューのをクリックして**Static Driver Verifier を起動しています**.

2.  をクリックして、**ルール**タブ。**規則セット**、 **MemoryUsage**します。

    Visual Studio の開発者コマンド プロンプト ウィンドウから既定のルールを選択するには、次のように指定します。 **MemoryUsage.sdv**で、 **/check**オプション。 例:

    ```
    msbuild /t:sdv /p:Inputs="/check:MemoryUsage.sdv" mydriver.VcxProj /p:Configuration="Win8 Release" /p:Platform=Win32
    ```

    詳細については、次を参照してください。[ドライバーで障害を検出する Static Driver Verifier を使用して](https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers)と[Static Driver Verifier のコマンド (MSBuild)](https://docs.microsoft.com/windows-hardware/drivers/devtest/-static-driver-verifier-commands--msbuild-)します。

 

 






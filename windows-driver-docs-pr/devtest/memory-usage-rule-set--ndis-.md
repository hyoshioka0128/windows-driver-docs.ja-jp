---
title: メモリ使用の規則セット (NDIS)
description: これらの規則を使用すると、ドライバーが正しく割り当てし、メモリを解放するのに NDIS 関数を呼び出すことを確認します。
ms.assetid: F28314C6-4B4D-479F-BB96-6850C8F98153
ms.date: 05/21/2018
ms.localizationpriority: medium
ms.openlocfilehash: 1ad6cddd87a98f608fa65eab78b4d5222c811fec
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56582648"
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
<td align="left"><p><a href="ndis-ndisallocategenericobject.md" data-raw-source="[&lt;strong&gt;NdisAllocateGenericObject&lt;/strong&gt;](ndis-ndisallocategenericobject.md)"> <strong>NdisAllocateGenericObject</strong> </a>ルールを指定する<a href="https://msdn.microsoft.com/library/windows/hardware/ff561603" data-raw-source="[&lt;strong&gt;NdisAllocateGenericObject&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff561603)"> <strong>NdisAllocateGenericObject</strong> </a>と<a href="https://msdn.microsoft.com/library/windows/hardware/ff561850" data-raw-source="[&lt;strong&gt;NdisFreeGenericObject&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff561850)"> <strong>NdisFreeGenericObject</strong> </a>代替の順序で呼び出されます。 最終的な目標はすべてジェネリック オブジェクトが解放されるかどうかを確認するときに<a href="https://msdn.microsoft.com/library/windows/hardware/ff559388" data-raw-source="[&lt;em&gt;MiniportHaltEx&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff559388)"> <em>MiniportHaltEx</em> </a>が終了します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="ndis-ndisallocatemdl.md" data-raw-source="[&lt;strong&gt;NdisAllocateMdl&lt;/strong&gt;](ndis-ndisallocatemdl.md)"><strong>NdisAllocateMdl</strong></a></p></td>
<td align="left"><p><a href="ndis-ndisallocatemdl.md" data-raw-source="[&lt;strong&gt;NdisAllocateMdl&lt;/strong&gt;](ndis-ndisallocatemdl.md)"> <strong>NdisAllocateMdl</strong> </a>ルールを指定する<a href="https://msdn.microsoft.com/library/windows/hardware/ff561605" data-raw-source="[&lt;strong&gt;NdisAllocateMdl&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff561605)"> <strong>NdisAllocateMdl</strong> </a>と<a href="https://msdn.microsoft.com/library/windows/hardware/ff562575" data-raw-source="[&lt;strong&gt;NdisFreeMdl&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff562575)"> <strong>NdisFreeMdl</strong></a>代替の順序で呼び出されます。 最終的な目標はすべて MDLs いることを確認するときに解放される<a href="https://msdn.microsoft.com/library/windows/hardware/ff559388" data-raw-source="[&lt;em&gt;MiniportHaltEx&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff559388)"> <em>MiniportHaltEx</em> </a>が終了します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="ndis-ndisallocatememorywithtagpriority.md" data-raw-source="[&lt;strong&gt;NdisAllocateMemoryWithTagPriority&lt;/strong&gt;](ndis-ndisallocatememorywithtagpriority.md)"><strong>NdisAllocateMemoryWithTagPriority</strong></a></p></td>
<td align="left"><p><a href="ndis-ndisallocatememorywithtagpriority.md" data-raw-source="[&lt;strong&gt;NdisAllocateMemoryWithTagPriority&lt;/strong&gt;](ndis-ndisallocatememorywithtagpriority.md)"> <strong>NdisAllocateMemoryWithTagPriority</strong> </a>ルールでは、ドライバーを呼び出してはならないことを指定します<strong>NdisAllocateMemoryWithTagPriority</strong>提供せず、 <em>タグ</em>します。</p>
<p>すべてのメモリ割り当ては、カーネル デバッガーやドライバーの検証ツールが、個別に割り当てられたメモリ ブロックを識別することができますを確実に一意のプール タグを使用してください。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="ndis-ndisallocatenetbuffer.md" data-raw-source="[&lt;strong&gt;NdisAllocateNetBuffer&lt;/strong&gt;](ndis-ndisallocatenetbuffer.md)"><strong>NdisAllocateNetBuffer</strong></a></p></td>
<td align="left"><p><a href="ndis-ndisallocatenetbuffer.md" data-raw-source="[&lt;strong&gt;NdisAllocateNetBuffer&lt;/strong&gt;](ndis-ndisallocatenetbuffer.md)"> <strong>NdisAllocateNetBuffer</strong> </a>ルールを指定する<a href="https://msdn.microsoft.com/library/windows/hardware/ff561607" data-raw-source="[&lt;strong&gt;NdisAllocateNetBuffer&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff561607)"> <strong>NdisAllocateNetBuffer</strong> </a>と<a href="https://msdn.microsoft.com/library/windows/hardware/ff562582" data-raw-source="[&lt;strong&gt;NdisFreeNetBuffer&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff562582)"> <strong>NdisFreeNetBuffer</strong> </a>代替の順序で呼び出されます。 すべてのインスタンスを確認する最終目標は、 <a href="https://msdn.microsoft.com/library/windows/hardware/ff568376" data-raw-source="[&lt;strong&gt;NET_BUFFER&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff568376)"> <strong>NET_BUFFER</strong> </a>ときに解放される<a href="https://msdn.microsoft.com/library/windows/hardware/ff559388" data-raw-source="[&lt;em&gt;MiniportHaltEx&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff559388)"> <em>MiniportHaltEx</em> </a>が終了します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="ndis-ndismfreesharedmemory.md" data-raw-source="[&lt;strong&gt;NdisMFreeSharedMemory&lt;/strong&gt;](ndis-ndismfreesharedmemory.md)"><strong>NdisMFreeSharedMemory</strong></a></p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff563589" data-raw-source="[&lt;strong&gt;NdisMFreeSharedMemory&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff563589)"><strong>NdisMFreeSharedMemory</strong> </a>から呼び出すことはできません、 <a href="https://msdn.microsoft.com/library/windows/hardware/ff559449" data-raw-source="[&lt;em&gt;MiniportShutdownEx&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff559449)"> <em>MiniportShutdownEx</em> </a>関数。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="ndis-ndismindicatestatusex.md" data-raw-source="[&lt;strong&gt;NdisMIndicateStatusEx&lt;/strong&gt;](ndis-ndismindicatestatusex.md)"><strong>NdisMIndicateStatusEx</strong></a></p></td>
<td align="left"><p>ドライバーを呼び出してはならない<a href="https://msdn.microsoft.com/library/windows/hardware/ff563600" data-raw-source="[&lt;strong&gt;NdisMIndicateStatusEx&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff563600)"> <strong>NdisMIndicateStatusEx</strong> </a>から戻った後に、 <a href="https://msdn.microsoft.com/library/windows/hardware/ff559388" data-raw-source="[&lt;em&gt;MiniportHaltEx&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff559388)"> <em>MiniportHaltEx</em> </a>関数。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="ndis-ndismmapiospace.md" data-raw-source="[&lt;strong&gt;NdisMMapIoSpace&lt;/strong&gt;](ndis-ndismmapiospace.md)"><strong>NdisMMapIoSpace</strong></a></p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff563613" data-raw-source="[&lt;strong&gt;NdisMMapIoSpace&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff563613)"> <strong>NdisMMapIoSpace</strong> </a>関数のみのコンテキストで呼び出されます<a href="https://msdn.microsoft.com/library/windows/hardware/ff559389" data-raw-source="[&lt;em&gt;MiniportInitializeEx&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff559389)"> <em>MiniportInitializeEx</em></a>します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="ndis-ndismregisterioportrange.md" data-raw-source="[&lt;strong&gt;NdisMRegisterIoPortRange&lt;/strong&gt;](ndis-ndismregisterioportrange.md)"><strong>NdisMRegisterIoPortRange</strong></a></p></td>
<td align="left"><p>ミニポート ドライバーは呼び出し<a href="https://msdn.microsoft.com/library/windows/hardware/ff563651" data-raw-source="[&lt;strong&gt;NdisMRegisterIoPortRange&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff563651)"> <strong>NdisMRegisterIoPortRange</strong> </a>からその<a href="https://msdn.microsoft.com/library/windows/hardware/ff559389" data-raw-source="[&lt;em&gt;MiniportInitializeEx&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff559389)"> <em>MiniportInitializeEx</em> </a>または MINIPORT_ADD_DEVICE 関数。 <em>MiniportInitializeEx</em> MINIPORT_ADD_DEVICE を呼び出す必要がありますまたは<a href="https://msdn.microsoft.com/library/windows/hardware/ff563672" data-raw-source="[&lt;strong&gt;NdisMSetMiniportAttributes&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff563672)"> <strong>NdisMSetMiniportAttributes</strong> </a>呼び出す前に<strong>NdisMRegisterIoPortRange</strong>します。</p></td>
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

    詳細については、次を参照してください。[ドライバーで障害を検出する Static Driver Verifier を使用して](https://msdn.microsoft.com/library/windows/hardware/hh454281)と[Static Driver Verifier のコマンド (MSBuild)](https://msdn.microsoft.com/library/windows/hardware/hh466459)します。

 

 






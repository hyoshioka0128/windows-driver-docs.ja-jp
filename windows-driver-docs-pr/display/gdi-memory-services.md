---
title: GDI メモリ サービス
description: GDI メモリ サービス
ms.assetid: 60b45f8f-766b-498c-a0c2-3e93ea4b43b9
keywords:
- GDI WDK Windows 2000 の表示、メモリのサービス
- グラフィックス ドライバー WDK Windows 2000 の表示、メモリのサービス
- 描画 WDK GDI やメモリのサービス
- WDK GDI のメモリ
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1a46856cbee659ad65a07c316f9fb4ad45511b8b
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56552990"
---
# <a name="gdi-memory-services"></a>GDI メモリ サービス


## <span id="ddk_gdi_memory_services_gg"></span><span id="DDK_GDI_MEMORY_SERVICES_GG"></span>


GDI は、割り当て、システム メモリ、ユーザーのメモリ、プライベート ユーザー メモリ、およびビデオのメモリを解放する機能のロックし、メモリの範囲をロック解除する機能など、ドライバー作成者にメモリに関連するいくつかのサービスを提供します。 次の表には、GDI メモリのサービスが一覧表示します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">関数</th>
<th align="left">説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff564176" data-raw-source="[&lt;strong&gt;EngAllocMem&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff564176)"><strong>EngAllocMem</strong></a></p></td>
<td align="left"><p>メモリのブロックを割り当てますを割り当てする前に呼び出し元が指定したタグを挿入します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff564177" data-raw-source="[&lt;strong&gt;EngAllocPrivateUserMem&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff564177)"><strong>EngAllocPrivateUserMem</strong></a></p></td>
<td align="left"><p>指定したプロセスのアドレス空間からユーザーがプライベート メモリのブロックを割り当てますを割り当てする前に呼び出し元が指定したタグを挿入します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff564178" data-raw-source="[&lt;strong&gt;EngAllocUserMem&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff564178)"><strong>EngAllocUserMem</strong></a></p></td>
<td align="left"><p>現在のプロセスのアドレス空間からのメモリ ブロックを割り当てますを割り当てする前に呼び出し元が指定したタグを挿入します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff564895" data-raw-source="[&lt;strong&gt;EngFreeMem&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff564895)"><strong>EngFreeMem</strong></a></p></td>
<td align="left"><p>によって割り当てられたシステム メモリのブロックを解放<a href="https://msdn.microsoft.com/library/windows/hardware/ff564176" data-raw-source="[&lt;strong&gt;EngAllocMem&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff564176)"> <strong>EngAllocMem</strong></a>します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff564907" data-raw-source="[&lt;strong&gt;EngFreePrivateUserMem&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff564907)"><strong>EngFreePrivateUserMem</strong></a></p></td>
<td align="left"><p>によって割り当てられたユーザーがプライベート メモリのブロックを解放<a href="https://msdn.microsoft.com/library/windows/hardware/ff564177" data-raw-source="[&lt;strong&gt;EngAllocPrivateUserMem&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff564177)"> <strong>EngAllocPrivateUserMem</strong></a>します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff564912" data-raw-source="[&lt;strong&gt;EngFreeUserMem&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff564912)"><strong>EngFreeUserMem</strong></a></p></td>
<td align="left"><p>によって割り当てられたメモリをユーザーのブロックを解放<a href="https://msdn.microsoft.com/library/windows/hardware/ff564178" data-raw-source="[&lt;strong&gt;EngAllocUserMem&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff564178)"> <strong>EngAllocUserMem</strong></a>します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff565011" data-raw-source="[&lt;strong&gt;EngSecureMem&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff565011)"><strong>EngSecureMem</strong></a></p></td>
<td align="left"><p>メモリ内で指定されたアドレス範囲をロックします。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff565454" data-raw-source="[&lt;strong&gt;EngUnsecureMem&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff565454)"><strong>EngUnsecureMem</strong></a></p></td>
<td align="left"><p>ロックダウンされているメモリ アドレスの範囲をロック解除します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff567267" data-raw-source="[&lt;strong&gt;HeapVidMemAllocAligned&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff567267)"><strong>HeapVidMemAllocAligned</strong></a></p></td>
<td align="left"><p>割り当て<em>オフスクリーン メモリ</em>DirectDraw ビデオ メモリのヒープ マネージャーを使用して、ディスプレイ ドライバー。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff570554" data-raw-source="[&lt;strong&gt;VidMemFree&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff570554)"><strong>VidMemFree</strong></a></p></td>
<td align="left"><p>ディスプレイ ドライバーによって割り当てられた画面外のメモリを解放<a href="https://msdn.microsoft.com/library/windows/hardware/ff567267" data-raw-source="[&lt;strong&gt;HeapVidMemAllocAligned&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff567267)"> <strong>HeapVidMemAllocAligned</strong></a>します。</p></td>
</tr>
</tbody>
</table>

 

 

 






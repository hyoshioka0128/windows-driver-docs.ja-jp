---
title: FCB リソース同期
description: FCB リソース同期
ms.assetid: 8355907e-e313-4e54-a63f-a82d9ce0d31b
keywords:
- FCB とリソースの同期、RDBSS WDK ファイル システム
- リダイレクトされたサブシステムの WDK のバッファリングをドライブのファイル システム、FCB とリソースの同期
- WDK RDBSS FCB とリソースの同期
- ページング I/O WDK RDBSS
- WDK RDBSS の同期
- ファイル制御ブロック構造 WDK RDBSS
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e964fc85743614da56816e66f9348819be860769
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63327437"
---
# <a name="fcb-resource-synchronization"></a>FCB リソース同期


## <span id="ddk_fcb_resource_synchronization_if"></span><span id="DDK_FCB_RESOURCE_SYNCHRONIZATION_IF"></span>


ミニ リダイレクター ドライバーへの関心のある同期リソースは、FCB で主に関連付けられています。 ページング I/O リソースと標準のリソースがあります。 ページング I/O リソースは、RDBSS によって内部的に管理されます。 ミニ リダイレクター ドライバーにアクセスできる唯一のリソースは、標準のリソースは、次の指定されたルーチンを使用してアクセスする必要があります。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">ルーチン</th>
<th align="left">説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff553363" data-raw-source="[&lt;strong&gt;RxAcquireExclusiveFcbResourceInMRx&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff553363)"><strong>RxAcquireExclusiveFcbResourceInMRx</strong></a></p></td>
<td align="left"><p>このルーチンは、排他モードで FCB のリソースを取得します。 このルーチンは FCB リソースが既に取得された場合は、無料の待機します。このルーチンでは、排他リソースが取得されるまで、コントロールは返されません。 このルーチンは、この FCB に関連付けられている RX_CONTEXT 構造が取り消された場合でも、FCB のリソースを取得します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff553372" data-raw-source="[&lt;strong&gt;RxAcquireSharedFcbResourceInMRx&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff553372)"><strong>RxAcquireSharedFcbResourceInMRx</strong></a></p></td>
<td align="left"><p>このルーチンは、共有モードで FCB のリソースを取得します。 このルーチンは排他的; 取得された以前の場合は、無料 FCB リソースの待機します。このルーチンでは、共有リソースが取得されるまで、コントロールは返されません。 このルーチンは、この FCB に関連付けられている RX_CONTEXT 構造が取り消された場合でも、FCB のリソースを取得します。</p></td>
</tr>
<tr class="odd">
<td align="left"><a href="https://msdn.microsoft.com/library/windows/hardware/ff553375" data-raw-source="[&lt;strong&gt;RxAcquireSharedFcbResourceInMRxEx&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff553375)"><strong>RxAcquireSharedFcbResourceInMRxEx</strong></a></td>
<td align="left"><p>このルーチンは、共有モードで FCB のリソースを取得します。 このルーチンは排他的; 取得された以前の場合は、無料 FCB リソースの待機します。このルーチンでは、共有リソースが取得されるまで、コントロールは返されません。 このルーチンは、この FCB に関連付けられている RX_CONTEXT 構造が取り消された場合でも、FCB のリソースを取得します。</p>
<p>このルーチンは、Windows Server 2003 Service Pack 1 (SP1) 以降にのみ使用できます。</p></td>
</tr>
<tr class="even">
<td align="left"><a href="https://msdn.microsoft.com/library/windows/hardware/ff554694" data-raw-source="[&lt;strong&gt;RxReleaseFcbResourceForThreadInMRx&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff554694)"><strong>RxReleaseFcbResourceForThreadInMRx</strong></a></td>
<td align="left"><p>このルーチンを使用して以前取得 FCB のリソースを解放する<a href="https://msdn.microsoft.com/library/windows/hardware/ff553375" data-raw-source="[&lt;strong&gt;RxAcquireSharedFcbResourceInMRxEx&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff553375)"> <strong>RxAcquireSharedFcbResourceInMRxEx</strong></a>します。</p>
<p>このルーチンは、Windows Server 2003 Service Pack 1 で使用できる以降のみです。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff554699" data-raw-source="[&lt;strong&gt;RxReleaseFcbResourceInMRx&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff554699)"><strong>RxReleaseFcbResourceInMRx</strong></a></p></td>
<td align="left"><p>このルーチンを使用して以前取得 FCB のリソースを解放する<a href="https://msdn.microsoft.com/library/windows/hardware/ff553363" data-raw-source="[&lt;strong&gt;RxAcquireExclusiveFcbResourceInMRx&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff553363)"> <strong>RxAcquireExclusiveFcbResourceInMRx</strong> </a>または<a href="https://msdn.microsoft.com/library/windows/hardware/ff553372" data-raw-source="[&lt;strong&gt;RxAcquireSharedFcbResourceInMRx&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff553372)"> <strong>RxAcquireSharedFcbResourceInMRx</strong></a>.</p></td>
</tr>
</tbody>
</table>

 

次のマクロは、現在のスレッドが FCB の標準リソースへのアクセスを持つかどうかを判断する rxprocs.h ヘッダー ファイルで定義されます。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">マクロ</th>
<th align="left">説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><strong>RxFcbAcquiredShared</strong> (<em>RXCONTEXT</em>, <em>FCB</em>)</p></td>
<td align="left"><p>このマクロは、現在のスレッドが共有モードで標準のリソースへのアクセスを持つかどうかを確認します。 このマクロを呼び出す、 <a href="https://msdn.microsoft.com/library/windows/hardware/ff545477" data-raw-source="[&lt;strong&gt;ExIsResourceAcquiredSharedLite&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff545477)"> <strong>ExIsResourceAcquiredSharedLite</strong> </a>ルーチン。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>RxIsFcbAcquiredShared</strong> (<em>FCB</em>)</p></td>
<td align="left"><p>このマクロは、現在のスレッドが共有モードで標準のリソースへのアクセスを持つかどうかを確認します。 このマクロを呼び出す、 <a href="https://msdn.microsoft.com/library/windows/hardware/ff545477" data-raw-source="[&lt;strong&gt;ExIsResourceAcquiredSharedLite&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff545477)"> <strong>ExIsResourceAcquiredSharedLite</strong> </a>ルーチン。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>RxIsFcbAcquiredExclusive</strong> (<em>FCB</em>)</p></td>
<td align="left"><p>このマクロは、現在のスレッドが排他モードで標準のリソースへのアクセスを持つかどうかを確認します。 このマクロを呼び出す、 <a href="https://msdn.microsoft.com/library/windows/hardware/ff545458" data-raw-source="[&lt;strong&gt;ExIsResourceAcquiredExclusiveLite&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff545458)"> <strong>ExIsResourceAcquiredExclusiveLite</strong> </a>ルーチン。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>RxIsFcbAcquired</strong> (<em>FCB</em>)</p></td>
<td align="left"><p>このマクロは、現在のスレッドが共有または排他モードで標準のリソースへのアクセスを持つかどうかを確認します。 このマクロを呼び出す、 <a href="https://msdn.microsoft.com/library/windows/hardware/ff545477" data-raw-source="[&lt;strong&gt;ExIsResourceAcquiredSharedLite&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff545477)"> <strong>ExIsResourceAcquiredSharedLite</strong> </a>と<a href="https://msdn.microsoft.com/library/windows/hardware/ff545458" data-raw-source="[&lt;strong&gt;ExIsResourceAcquiredExclusiveLite&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff545458)"> <strong>ExIsResourceAcquiredExclusiveLite</strong> </a>ルーチン。</p></td>
</tr>
</tbody>
</table>

 

 

 





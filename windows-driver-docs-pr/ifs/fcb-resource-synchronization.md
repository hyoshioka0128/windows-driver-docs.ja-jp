---
title: FCB リソース同期
description: FCB リソース同期
ms.assetid: 8355907e-e313-4e54-a63f-a82d9ce0d31b
keywords:
- RDBSS WDK ファイルシステム、FCB リソース同期
- リダイレクトされたドライブバッファリングサブシステム WDK ファイルシステム、FCB リソース同期
- FCB リソース同期 WDK RDBSS
- ページング i/o WDK RDBSS
- 同期 WDK RDBSS
- ファイル制御ブロック構造の WDK RDBSS
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: edcd3d8030a7d23b692edf9ab83472199ca23903
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841416"
---
# <a name="fcb-resource-synchronization"></a>FCB リソース同期


## <span id="ddk_fcb_resource_synchronization_if"></span><span id="DDK_FCB_RESOURCE_SYNCHRONIZATION_IF"></span>


ミニリダイレクタードライバーにとって重要な同期リソースは、主に FCB に関連付けられています。 ページング i/o リソースと通常のリソースがあります。 ページング i/o リソースは、RDBSS によって内部的に管理されます。 ミニリダイレクタードライバーからアクセスできる唯一のリソースは通常のリソースです。このリソースには、次の指定されたルーチンを使用してアクセスする必要があります。

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
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/mrxfcb/nf-mrxfcb-rxacquireexclusivefcbresourceinmrx" data-raw-source="[&lt;strong&gt;RxAcquireExclusiveFcbResourceInMRx&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/mrxfcb/nf-mrxfcb-rxacquireexclusivefcbresourceinmrx)"><strong>RxAcquireExclusiveFcbResourceInMRx</strong></a></p></td>
<td align="left"><p>このルーチンは、排他モードで FCB リソースを取得します。 このルーチンは、既に取得されている場合、FCB リソースが解放されるまで待機します。このルーチンは、排他的なリソースが取得されるまで制御を返しません。 このようなルーチンは、この FCB に関連付けられている RX_CONTEXT 構造体がキャンセルされている場合でも、FCB リソースを取得します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/mrxfcb/nf-mrxfcb-rxacquiresharedfcbresourceinmrx" data-raw-source="[&lt;strong&gt;RxAcquireSharedFcbResourceInMRx&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/mrxfcb/nf-mrxfcb-rxacquiresharedfcbresourceinmrx)"><strong>RxAcquireSharedFcbResourceInMRx</strong></a></p></td>
<td align="left"><p>このルーチンは、共有モードで FCB リソースを取得します。 このルーチンは、以前に排他的に取得された FCB リソースが解放されるまで待機します。このルーチンは、共有リソースが取得されるまで制御を返しません。 このようなルーチンは、この FCB に関連付けられている RX_CONTEXT 構造体がキャンセルされている場合でも、FCB リソースを取得します。</p></td>
</tr>
<tr class="odd">
<td align="left"><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/mrxfcb/nf-mrxfcb-rxacquiresharedfcbresourceinmrxex" data-raw-source="[&lt;strong&gt;RxAcquireSharedFcbResourceInMRxEx&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/mrxfcb/nf-mrxfcb-rxacquiresharedfcbresourceinmrxex)"><strong>RxAcquireSharedFcbResourceInMRxEx</strong></a></td>
<td align="left"><p>このルーチンは、共有モードで FCB リソースを取得します。 このルーチンは、以前に排他的に取得された FCB リソースが解放されるまで待機します。このルーチンは、共有リソースが取得されるまで制御を返しません。 このようなルーチンは、この FCB に関連付けられている RX_CONTEXT 構造体がキャンセルされている場合でも、FCB リソースを取得します。</p>
<p>このルーチンは、Windows Server 2003 Service Pack 1 (SP1) 以降でのみ使用できます。</p></td>
</tr>
<tr class="even">
<td align="left"><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/mrxfcb/nf-mrxfcb-rxreleasefcbresourceforthreadinmrx" data-raw-source="[&lt;strong&gt;RxReleaseFcbResourceForThreadInMRx&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/mrxfcb/nf-mrxfcb-rxreleasefcbresourceforthreadinmrx)"><strong>RxReleaseFcbResourceForThreadInMRx</strong></a></td>
<td align="left"><p>このルーチンは、 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/mrxfcb/nf-mrxfcb-rxacquiresharedfcbresourceinmrxex" data-raw-source="[&lt;strong&gt;RxAcquireSharedFcbResourceInMRxEx&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/mrxfcb/nf-mrxfcb-rxacquiresharedfcbresourceinmrxex)"><strong>RxAcquireSharedFcbResourceInMRxEx</strong></a>を使用して以前に取得した FCB リソースを解放します。</p>
<p>このルーチンは、Windows Server 2003 Service Pack 1 以降でのみ使用できます。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/mrxfcb/nf-mrxfcb-rxreleasefcbresourceinmrx" data-raw-source="[&lt;strong&gt;RxReleaseFcbResourceInMRx&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/mrxfcb/nf-mrxfcb-rxreleasefcbresourceinmrx)"><strong>RxReleaseFcbResourceInMRx</strong></a></p></td>
<td align="left"><p>このルーチンは、 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/mrxfcb/nf-mrxfcb-rxacquireexclusivefcbresourceinmrx" data-raw-source="[&lt;strong&gt;RxAcquireExclusiveFcbResourceInMRx&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/mrxfcb/nf-mrxfcb-rxacquireexclusivefcbresourceinmrx)"><strong>RxAcquireExclusiveFcbResourceInMRx</strong></a>または<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/mrxfcb/nf-mrxfcb-rxacquiresharedfcbresourceinmrx" data-raw-source="[&lt;strong&gt;RxAcquireSharedFcbResourceInMRx&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/mrxfcb/nf-mrxfcb-rxacquiresharedfcbresourceinmrx)"><strong>RxAcquireSharedFcbResourceInMRx</strong></a>を使用して以前に取得した FCB リソースを解放します。</p></td>
</tr>
</tbody>
</table>

 

次のマクロは、現在のスレッドが FCB 通常のリソースにアクセスできるかどうかを判断するために、rxprocs ヘッダーファイルで定義されています。

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
<td align="left"><p><strong>RxFcbAcquiredShared</strong> (<em>RXCONTEXT</em>、 <em>FCB</em>)</p></td>
<td align="left"><p>このマクロは、現在のスレッドが共有モードの通常のリソースにアクセスできるかどうかを確認します。 このマクロは、 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-exisresourceacquiredsharedlite" data-raw-source="[&lt;strong&gt;ExIsResourceAcquiredSharedLite&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-exisresourceacquiredsharedlite)"><strong>ExIsResourceAcquiredSharedLite</strong></a>ルーチンを呼び出します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>RxIsFcbAcquiredShared</strong> (<em>FCB</em>)</p></td>
<td align="left"><p>このマクロは、現在のスレッドが共有モードの通常のリソースにアクセスできるかどうかを確認します。 このマクロは、 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-exisresourceacquiredsharedlite" data-raw-source="[&lt;strong&gt;ExIsResourceAcquiredSharedLite&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-exisresourceacquiredsharedlite)"><strong>ExIsResourceAcquiredSharedLite</strong></a>ルーチンを呼び出します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>RxIsFcbAcquiredExclusive</strong> (<em>FCB</em>)</p></td>
<td align="left"><p>このマクロは、現在のスレッドが排他モードで通常のリソースにアクセスできるかどうかを確認します。 このマクロは、 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-exisresourceacquiredexclusivelite" data-raw-source="[&lt;strong&gt;ExIsResourceAcquiredExclusiveLite&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-exisresourceacquiredexclusivelite)"><strong>ExIsResourceAcquiredExclusiveLite</strong></a>ルーチンを呼び出します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>RxIsFcbAcquired</strong> (<em>FCB</em>)</p></td>
<td align="left"><p>このマクロは、現在のスレッドが共有モードまたは排他モードで通常のリソースにアクセスできるかどうかを確認します。 このマクロは、 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-exisresourceacquiredsharedlite" data-raw-source="[&lt;strong&gt;ExIsResourceAcquiredSharedLite&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-exisresourceacquiredsharedlite)"><strong>ExIsResourceAcquiredSharedLite</strong></a>および<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-exisresourceacquiredexclusivelite" data-raw-source="[&lt;strong&gt;ExIsResourceAcquiredExclusiveLite&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-exisresourceacquiredexclusivelite)"><strong>ExIsResourceAcquiredExclusiveLite</strong></a>ルーチンを呼び出します。</p></td>
</tr>
</tbody>
</table>

 

 

 





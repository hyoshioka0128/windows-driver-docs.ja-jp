---
title: プールの割り当てとフリー ルーチン
description: プールの割り当てとフリー ルーチン
ms.assetid: 757eebc0-ebd4-49a1-acea-6c27956b4b23
keywords:
- RDBSS WDK ファイルシステム、プールの割り当て
- リダイレクトされたドライブバッファリングサブシステム WDK ファイルシステム、プールの割り当て
- プールの割り当て (WDK RDBSS)
- RDBSS WDK ファイルシステム、無料のルーチン
- リダイレクトされたドライブバッファリングサブシステム WDK ファイルシステム、フリールーチン
- 無料のルーチン WDK RDBSS
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0c5f018913de323fd05a5f26660b52792c80bc53
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841030"
---
# <a name="pool-allocation-and-free-routines"></a>プールの割り当てとフリー ルーチン


## <span id="ddk_pool_allocation_and_free_functions_if"></span><span id="DDK_POOL_ALLOCATION_AND_FREE_FUNCTIONS_IF"></span>


RDBSS には、プール割り当てに使用する多くのルーチンが用意されています。 通常、これらのルーチンは、これらのルーチンを直接呼び出すのではなく、マクロを使用して呼び出されます。 これらのマクロは、リテールビルドとチェックビルドの違いを自動的に処理します。

チェックを行ったビルドでは、これらのルーチンは、通常のカーネル割り当ておよびフリールーチンのラッパーを追加するように設計されています。 プールの割り当てと解放のルーチンのラッパーは、追加のデバッグ情報を提供し、カーネルプールの割り当てと解放のルーチンを呼び出す前に、さまざまな種類のチェックと保護を実行するルーチンのセットを呼び出します。 ただし、これらの機能は、これらの割り当ておよびフリールーチンには現在実装されていませんが、今後のリリースで追加される可能性があります。

無料のビルドでは、これらのルーチンは、カーネルの割り当てとフリールーチン、 [**Exallocatepoolwithtag**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-exallocatepoolwithtag) 、および[**exfreepool**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/nf-ntddk-exfreepool)への直接呼び出しになります。

次の表に、RDBSS プールの割り当てとフリールーチンを示します。

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
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ifs/-rxallocatepoolwithtag" data-raw-source="[&lt;strong&gt;_RxAllocatePoolWithTag&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ifs/-rxallocatepoolwithtag)"><strong>_RxAllocatePoolWithTag</strong></a></p></td>
<td align="left"><p>このルーチンは、メモリの問題をキャッチするために、ブロックの先頭に4バイトのタグがあるプールからメモリを割り当てます。</p>
<p>このルーチンを直接使用するのではなく、 <strong>RxAllocatePoolWithTag</strong>マクロを呼び出すことをお勧めします。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ifs/-rxcheckmemoryblock" data-raw-source="[&lt;strong&gt;_RxCheckMemoryBlock&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ifs/-rxcheckmemoryblock)"><strong>_RxCheckMemoryBlock</strong></a></p></td>
<td align="left"><p>このルーチンは、メモリブロックに特別な RX_POOL_HEADER HEADER 署名があるかどうかをチェックします。 ネットワークミニリダイレクタードライバーは、ルーチンを使用するために割り当てられたメモリに、この特殊な署名ブロックを追加する必要があることに注意してください。</p>
<p>この特別なヘッダーブロックが実装されていないため、このルーチンは使用しないでください。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ifs/-rxfreepool" data-raw-source="[&lt;strong&gt;_RxFreePool&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ifs/-rxfreepool)"><strong>_RxFreePool</strong></a></p></td>
<td align="left"><p>このルーチンは、メモリプールを解放します。</p>
<p>このルーチンを直接使用するのではなく、 <strong>RxFreePool</strong>マクロを呼び出すことをお勧めします。</p></td>
</tr>
</tbody>
</table>

 

*Ntrxdef .h*ヘッダーファイルで定義されている多くのマクロは、これらのルーチンを呼び出します。 前の表に示したルーチンを直接呼び出すのではなく、通常は次のマクロを使用します。

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
<td align="left"><p><strong>RxAllocatePoolWithTag</strong> (<em>type</em>、 <em>size</em>、 <em>tag</em>)</p></td>
<td align="left"><p>Checked ビルドでは、このマクロは、メモリ trashing のインスタンスをキャッチするのに役立つ4バイトのタグを持つプールからメモリを割り当てます。</p>
<p>リテールビルドでは、このマクロは<strong>Exallocatepoolwithtag</strong>への直接の呼び出しになります。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>RxCheckMemoryBlock</strong> (<em>ptr</em>)</p></td>
<td align="left"><p>Checked ビルドでは、このマクロはメモリブロックに特別な RX_POOL_HEADER HEADER 署名があるかどうかをチェックします。</p>
<p>リテールビルドでは、このマクロは何も行いません。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>RxFreePool</strong> (<em>ptr</em>)</p></td>
<td align="left"><p>チェックされたビルドでは、このマクロはメモリプールを解放します。</p>
<p>リテールビルドでは、このマクロは<strong>Exfreepool</strong>への直接の呼び出しになります。</p></td>
</tr>
</tbody>
</table>

 

 

 





---
title: プールの割り当てとフリー ルーチン
description: プールの割り当てとフリー ルーチン
ms.assetid: 757eebc0-ebd4-49a1-acea-6c27956b4b23
keywords:
- RDBSS WDK ファイル システム、プールの割り当て
- リダイレクトされたサブシステムの WDK のバッファリングをドライブのファイル システム、プールの割り当て
- プール割り当て WDK RDBSS
- RDBSS WDK ファイル システムでは、無料のルーチン
- リダイレクトされたサブシステムの WDK のバッファリングをドライブのファイル システム、無料のルーチン
- 無料の WDK RDBSS ルーチン
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f868d30d8a92cdfe1894f68386e8cfb7da5c3a95
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67366787"
---
# <a name="pool-allocation-and-free-routines"></a>プールの割り当てとフリー ルーチン


## <span id="ddk_pool_allocation_and_free_functions_if"></span><span id="DDK_POOL_ALLOCATION_AND_FREE_FUNCTIONS_IF"></span>


RDBSS は、プールの割り当てに使用するルーチンを提供します。 通常、これらのルーチンは、これらのルーチンを直接呼び出すことではなく、マクロを使用すると呼ばれます。 マクロは、製品版でチェックされたビルド間の相違点を自動的に処理します。

チェックのビルドでは、これらのルーチンが標準カーネルの割り当てと解放ルーチン ラップするラッパーを追加する設計されました。 プールの割り当てと解放ルーチンのこれらのラッパーでは、追加のデバッグ情報を提供し、一連のチェックおよびカーネル プールの割り当てと解放ルーチンを呼び出す前に保護するためのさまざまな種類を実行するルーチンを呼び出します。 ただし、これらの機能はこれらの割り当てと無料のルーチンで現在実装されていませんが、今後のリリースで追加される可能性があります。

無料のビルドでは、これらのルーチンになるカーネルの割り当てと無料のルーチンへの直接呼び出し[ **exallocatepoolwithtag に**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-exallocatepoolwithtag)と[ **ExFreePool** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddk/nf-ntddk-exfreepool).

次の表には、RDBSS プールの割り当てと解放ルーチンが一覧表示します。

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
<td align="left"><p>このルーチンは、メモリの問題を把握するのに役立つ、ブロックの先頭 4 バイトのタグを使用して、プールからメモリを割り当てます。</p>
<p>推奨されます、 <strong>RxAllocatePoolWithTag</strong>このルーチンを直接使用する代わりにマクロが呼び出されます。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ifs/-rxcheckmemoryblock" data-raw-source="[&lt;strong&gt;_RxCheckMemoryBlock&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ifs/-rxcheckmemoryblock)"><strong>_RxCheckMemoryBlock</strong></a></p></td>
<td align="left"><p>このルーチンは、特別な RX_POOL_HEADER ヘッダーの署名のメモリ ブロックを確認します。 ルーチンを使用するには、ネットワークのミニ リダイレクター ドライバーはメモリにこの特別な署名ブロックを追加する必要がありますので注意が割り当てられます。</p>
<p>この特殊なヘッダー ブロックが実装されていないために、このルーチンを使用しない必要があります。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ifs/-rxfreepool" data-raw-source="[&lt;strong&gt;_RxFreePool&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ifs/-rxfreepool)"><strong>_RxFreePool</strong></a></p></td>
<td align="left"><p>このルーチンは、メモリ プールを解放します。</p>
<p>推奨されます、 <strong>RxFreePool</strong>このルーチンを直接使用する代わりにマクロが呼び出されます。</p></td>
</tr>
</tbody>
</table>

 

定義されているマクロは、数、 *ntrxdef.h*ヘッダー ファイルで、これらのルーチンを呼び出します。 直接の前の表に表示されているルーチンを呼び出す代わりに次のマクロは通常使用されます。

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
<td align="left"><p><strong>RxAllocatePoolWithTag</strong> (<em>型</em>、<em>サイズ</em>、<em>タグ</em>)</p></td>
<td align="left"><p>チェック済みのビルドでは、このマクロは、メモリの破壊のインスタンスを検出するのに役立つ、ブロックの先頭 4 バイトのタグを使用して、プールからメモリを割り当てます。</p>
<p>製品版ビルドでは、このマクロが、直接呼び出しを<strong>exallocatepoolwithtag に</strong>します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>RxCheckMemoryBlock</strong> (<em>ptr</em>)</p></td>
<td align="left"><p>チェック済みのビルドでは、このマクロは、特別な RX_POOL_HEADER ヘッダーの署名のメモリ ブロックを確認します。</p>
<p>製品版ビルドでこのマクロは何もしません。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>RxFreePool</strong> (<em>ptr</em>)</p></td>
<td align="left"><p>チェック済みのビルドでは、このマクロは、メモリ プールを解放します。</p>
<p>製品版ビルドでは、このマクロが、直接呼び出しを<strong>ExFreePool</strong>します。</p></td>
</tr>
</tbody>
</table>

 

 

 





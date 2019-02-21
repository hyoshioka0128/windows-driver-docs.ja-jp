---
title: プールの割り当てと解放ルーチン
description: プールの割り当てと解放ルーチン
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
ms.openlocfilehash: 1abe38b4e02dbaabd26b858824ad8332fa8e7d7c
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56537640"
---
# <a name="pool-allocation-and-free-routines"></a>プールの割り当てと解放ルーチン


## <span id="ddk_pool_allocation_and_free_functions_if"></span><span id="DDK_POOL_ALLOCATION_AND_FREE_FUNCTIONS_IF"></span>


RDBSS は、プールの割り当てに使用するルーチンを提供します。 通常、これらのルーチンは、これらのルーチンを直接呼び出すことではなく、マクロを使用すると呼ばれます。 マクロは、製品版でチェックされたビルド間の相違点を自動的に処理します。

チェックのビルドでは、これらのルーチンが標準カーネルの割り当てと解放ルーチン ラップするラッパーを追加する設計されました。 プールの割り当てと解放ルーチンのこれらのラッパーでは、追加のデバッグ情報を提供し、一連のチェックおよびカーネル プールの割り当てと解放ルーチンを呼び出す前に保護するためのさまざまな種類を実行するルーチンを呼び出します。 ただし、これらの機能はこれらの割り当てと無料のルーチンで現在実装されていませんが、今後のリリースで追加される可能性があります。

無料のビルドでは、これらのルーチンになるカーネルの割り当てと無料のルーチンへの直接呼び出し[ **exallocatepoolwithtag に**](https://msdn.microsoft.com/library/windows/hardware/ff544520)と[ **ExFreePool** ](https://msdn.microsoft.com/library/windows/hardware/ff544590).

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
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff557355" data-raw-source="[&lt;strong&gt;_RxAllocatePoolWithTag&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff557355)"><strong>_RxAllocatePoolWithTag</strong></a></p></td>
<td align="left"><p>このルーチンは、メモリの問題を把握するのに役立つ、ブロックの先頭 4 バイトのタグを使用して、プールからメモリを割り当てます。</p>
<p>推奨されます、 <strong>RxAllocatePoolWithTag</strong>このルーチンを直接使用する代わりにマクロが呼び出されます。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff557358" data-raw-source="[&lt;strong&gt;_RxCheckMemoryBlock&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff557358)"><strong>_RxCheckMemoryBlock</strong></a></p></td>
<td align="left"><p>このルーチンは、特別な RX_POOL_HEADER ヘッダーの署名のメモリ ブロックを確認します。 ルーチンを使用するには、ネットワークのミニ リダイレクター ドライバーはメモリにこの特別な署名ブロックを追加する必要がありますので注意が割り当てられます。</p>
<p>この特殊なヘッダー ブロックが実装されていないために、このルーチンを使用しない必要があります。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff557363" data-raw-source="[&lt;strong&gt;_RxFreePool&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff557363)"><strong>_RxFreePool</strong></a></p></td>
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

 

 

 





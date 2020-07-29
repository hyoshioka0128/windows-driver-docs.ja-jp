---
title: アドレスとアドレス範囲の構文
description: アドレスとアドレス範囲の構文
ms.assetid: 3d4f41f1-07ec-484d-a748-27fbbb9bd0b2
ms.date: 07/24/2020
ms.localizationpriority: medium
ms.openlocfilehash: 65fa76dd1e92c8e508f2af6ea5694fad637b1e73
ms.sourcegitcommit: 9102e34c3322d8697dbb6f9a1d78879147a73373
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/28/2020
ms.locfileid: "87264467"
---
# <a name="address-and-address-range-syntax"></a>アドレスとアドレス範囲の構文


## <span id="ddk_address_and_address_range_syntax_dbg"></span><span id="DDK_ADDRESS_AND_ADDRESS_RANGE_SYNTAX_DBG"></span>


デバッガーでアドレスを指定するには、いくつかの方法があります。

アドレスは常に*仮想アドレス*です。ただし、ドキュメントが別の種類のアドレスを示す場合を除きます。 ユーザーモードでは、デバッガーは、[現在のプロセス](controlling-processes-and-threads.md)のページディレクトリに従って仮想アドレスを解釈します。 カーネルモードでは、デバッガーは[プロセスコンテキスト](changing-contexts.md#process-context)によって指定されたプロセスのページディレクトリに従って仮想アドレスを解釈します。 *ユーザーモードアドレスコンテキスト*を直接設定することもできます。 ユーザーモードアドレスコンテキストの詳細については、「[**コンテキスト (ユーザーモードアドレスコンテキストの設定)**](-context--set-user-mode-address-context-.md)」を参照してください。

### <a name="span-idaddress_modes_and_segment_supportspanspan-idaddress_modes_and_segment_supportspanaddress-modes-and-segment-support"></a><span id="address_modes_and_segment_support"></span><span id="ADDRESS_MODES_AND_SEGMENT_SUPPORT"></span>アドレスモードとセグメントのサポート

X86 ベースのプラットフォームでは、CDB と KD は次のアドレス指定モードをサポートしています。 これらのモードは、プレフィックスによって区別されます。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">Prefix</th>
<th align="left">名前</th>
<th align="left">アドレスの種類</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>%</p></td>
<td align="left"><p>flat</p></td>
<td align="left"><p>32ビットアドレス (32 ビットセグメントを指す16ビットセレクターとも呼ばれます) と64ビットアドレス (64 ビットシステムの場合)。</p></td>
</tr>
<tr class="even">
<td align="left"><p>&</p></td>
<td align="left"><p>仮想86</p></td>
<td align="left"><p>実際のモードアドレス。 x86 ベースのみ。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>#</p></td>
<td align="left"><p>plain</p></td>
<td align="left"><p>実際のモードアドレス。 x86 ベースのみ。</p></td>
</tr>
</tbody>
</table>

 

Plain モードと virtual 86 モードの違いは、単純な16ビットアドレスでは、セグメント値をセレクターとして使用し、セグメント記述子を検索するという点です。 ただし、仮想86アドレスはセレクターを使用せず、代わりに下位 1 MB に直接マップします。

現在の既定のモードではないアドレス指定モードでメモリにアクセスする場合は、アドレスモードプレフィックスを使用して現在のアドレスモードをオーバーライドできます。

### <a name="span-idaddress_argumentsspanspan-idaddress_argumentsspanaddress-arguments"></a><span id="address_arguments"></span><span id="ADDRESS_ARGUMENTS"></span>アドレス引数

アドレス引数は、変数と関数の場所を指定します。 次の表では、CDB および KD で使用できるさまざまなアドレスの構文と意味について説明します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">構文</th>
<th align="left">意味</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>offset</p></td>
<td align="left"><p>現在の実行モードに対応する型を持つ、仮想メモリ領域内の絶対アドレス。 たとえば、現在の実行モードが16ビットの場合、オフセットは16ビットです。 実行モードが32ビットに分割されている場合、オフセットは32ビットのセグメント化されます。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>&</strong>[[セグメント:]] オフセット</p></td>
<td align="left"><p>実際のアドレス。 x86 ベースおよび x64 ベース。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>%</strong>セグメント: [[オフセット]]</p></td>
<td align="left"><p>32ビットまたは64ビットのセグメント化アドレス。 x86 ベースおよび x64 ベース。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>%</strong>[[オフセット]]</p></td>
<td align="left"><p>仮想メモリ空間内の絶対アドレス (32 ビットまたは64ビット)。 x86 ベースおよび x64 ベース。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>名前 [[ <strong>+</strong> | <strong>−</strong> ]] オフセット</p></td>
<td align="left"><p>32ビットまたは64ビットのフラットアドレス。 <em>名前</em>は任意のシンボルにすることができます。 <em>オフセット</em>オフセットを指定します。 このオフセットは、そのプレフィックスが示す任意のアドレスモードにすることができます。 既定のモードアドレスを指定するプレフィックスはありません。 オフセットは、正 (+) または負 (−) の値として指定できます。</p></td>
</tr>
</tbody>
</table>

 

セグメント記述子の情報を表示するには、 [**dg (表示セレクター)**](dg--display-selector-.md)コマンドを使用します。

MASM 式では、 **poi**演算子を使用して任意のポインターを逆参照することもできます。 たとえば、アドレス0x00123456 のポインターがアドレスの場所0x00420000 を指している場合、次の2つのコマンドは同等です。

```dbgcmd
0:000> dd 420000 
0:000> dd poi(123456) 
```

C++ の式では、ポインターは C++ のポインターのように動作します。 ただし、数値は整数として解釈されます。 実際の数値を deference する必要がある場合は、次の例に示すように、最初にキャストする必要があります。

```dbgcmd
0:000> dd *( (long*) 0x123456 ) 
```

一部の[疑似レジスタ](pseudo-register-syntax.md)には、現在のプログラムカウンターの場所など、一般的なアドレスも保持されます。

また、元のソースファイル名と行番号を指定して、アプリケーションのアドレスを指定することもできます。 この情報を指定する方法の詳細については、「 [Source Line 構文](source-line-syntax.md)」を参照してください。

### <a name="span-idaddress_rangesspanspan-idaddress_rangesspanaddress-ranges"></a><span id="address_ranges"></span><span id="ADDRESS_RANGES"></span>アドレス範囲

アドレス範囲は、アドレスのペア、またはアドレスとオブジェクトの数で指定できます。

アドレスのペアで範囲を指定するには、開始アドレスと終了アドレスを指定します。 たとえば、次の例は、アドレス0x00001000 から始まる8バイトの範囲を示しています。

```dbgcmd
0x00001000  0x00001007
```

アドレス範囲とオブジェクト数を指定するには、アドレス引数、文字 L (大文字または小文字)、および値引数を指定します。 アドレスは、開始アドレスを指定します。 値は、検査または表示するオブジェクトの数を指定します。 オブジェクトのサイズは、コマンドによって異なります。 たとえば、オブジェクトのサイズが1バイトの場合、次の例は、アドレス0x00001000 から始まる8バイトの範囲です。

```dbgcmd
0x00001000  L8
```

ただし、オブジェクトのサイズが二重の単語 (32 ビットまたは4バイト) の場合、次の2つの範囲はそれぞれ8バイトの範囲を指定します。

```dbgcmd
0x00001000  0x00001007
0x00001000  L2
```

値を指定するには、次の2つの方法があります (**L * * * サイズ*範囲指定子)。

-   **左右?** *サイズ*(疑問符付き) は **l * * * サイズ*と同じですが、 **l? を除きます。** *サイズ*では、デバッガーの自動範囲制限が削除されます。 通常、範囲の上限は 256 MB です。これは、範囲が大きいほど、文字種のエラーになるためです。 256 MB を超える範囲を指定する場合は、L を使用する必要があり**ます。** *サイズ*の構文。

-   **L** *サイズ*(ハイフン付き) は、指定さ*れたアドレスで終了する長さ*の範囲を指定します。 たとえば、 **8000万 L20**は0X80000000 から0x8000001F までの範囲を指定し、 **8000万 L-20**は 0X7fffffe0 ~ 0x7fffffff の範囲を指定します。

アドレス範囲を要求するコマンドの中には、引数として1つのアドレスを受け取るものがあります。 この場合、コマンドはいくつかの既定のオブジェクト数を使用して、範囲のサイズを計算します。 通常、アドレス範囲が最後のパラメーターであるコマンドは、この構文を許可します。 各コマンドの正確な構文と既定の範囲サイズについては、各コマンドのリファレンストピックを参照してください。

## <a name="see-also"></a>参照

メモリに関する情報を表示するには、 [! address](-address.md)コマンドを使用します。 メモリを検索するには、 [s (Search memory)](s--search-memory-.md)コマンドを使用します。 メモリの内容を表示するには、 [d、da、db、dc、dd、dd、df、dp、dq、du、dw (Display memory)](d--da--db--dc--dd--dd--df--dp--dq--du--dw--dw--dyb--dyd--display-memor.md)コマンドを使用します。 [メモリ] ウィンドウを使用してメモリを表示および編集する方法の詳細については[、「メモリウィンドウの使用](memory-window.md)」を参照してください。

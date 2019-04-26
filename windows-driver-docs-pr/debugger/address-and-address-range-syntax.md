---
title: アドレスとアドレス範囲の構文
description: アドレスとアドレス範囲の構文
ms.assetid: 3d4f41f1-07ec-484d-a748-27fbbb9bd0b2
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: ce680cc5b5fc66fe10dff5ca6b24844ed5653c04
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63354943"
---
# <a name="address-and-address-range-syntax"></a>アドレスとアドレス範囲の構文


## <span id="ddk_address_and_address_range_syntax_dbg"></span><span id="DDK_ADDRESS_AND_ADDRESS_RANGE_SYNTAX_DBG"></span>


デバッガーでアドレスを指定するいくつかの方法はあります。

アドレスは、常に*仮想アドレス*とき、ドキュメント具体的には別の種類のアドレスを除き、します。 ユーザー モードでデバッガーがに従って、ディレクトリの仮想アドレスを解釈し、[現在のプロセス](controlling-processes-and-threads.md)します。 カーネル モードでデバッガーがプロセスのページ ディレクトリに従って仮想アドレスを解釈する、[プロセス コンテキスト](changing-contexts.md#process-context)を指定します。 直接設定することができます、*ユーザー モード アドレス コンテキスト*します。 ユーザー モード アドレス コンテキストに関する詳細については、次を参照してください。 [ **.context (ユーザー モード アドレス コンテキストの設定)**](-context--set-user-mode-address-context-.md)します。

### <a name="span-idaddressmodesandsegmentsupportspanspan-idaddressmodesandsegmentsupportspanaddress-modes-and-segment-support"></a><span id="address_modes_and_segment_support"></span><span id="ADDRESS_MODES_AND_SEGMENT_SUPPORT"></span>アドレス モードとセグメントのサポート

KD、CDB は、x86 ベースのプラットフォームで、次のアドレス指定モードをサポートします。 これらのモードは、そのプレフィックスで識別されます。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">プレフィックス</th>
<th align="left">名前</th>
<th align="left">アドレスの種類</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>%</p></td>
<td align="left"><p>フラット</p></td>
<td align="left"><p>32 ビットのアドレス (32 ビットのセグメントを指す 16 ビット セレクターも) と 64 ビット システムで 64 ビットのアドレス。</p></td>
</tr>
<tr class="even">
<td align="left"><p>&amp;</p></td>
<td align="left"><p>仮想 86</p></td>
<td align="left"><p>リアル モードのアドレス。 x86 ベースのみです。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>#</p></td>
<td align="left"><p>プレーン</p></td>
<td align="left"><p>リアル モードのアドレス。 x86 ベースのみです。</p></td>
</tr>
</tbody>
</table>

 

プレーンなと仮想 86 モード間の違いは、プレーンな 16 ビットのアドレスはセレクターとしてセグメントの値を使用して、セグメントの記述子を検索にです。 仮想の 86 アドレスは、セレクターを使用しないと、代わりに低い 1 MB に直接マップされます。

現在の既定のモードではないアドレス指定モードを使用してメモリをアクセスする場合は、現在のアドレス モードをオーバーライドするモードのアドレス プレフィックスを使用できます。

### <a name="span-idaddressargumentsspanspan-idaddressargumentsspanaddress-arguments"></a><span id="address_arguments"></span><span id="ADDRESS_ARGUMENTS"></span>アドレスの引数

アドレスの引数は、変数と関数の場所を指定します。 次の表では、構文と KD、CDB で使用できるさまざまなアドレスの意味について説明します。

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
<td align="left"><p>現在の実行モードに対応する型での仮想メモリ空間で絶対アドレスです。 たとえば、現在の実行モードが 16 ビットの場合は、オフセットは 16 ビットです。 セグメント化された 32 ビットの実行モードには、オフセットは 32 ビットのセグメント化です。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>&amp;</strong>[セグメント:] のオフセット</p></td>
<td align="left"><p>実際のアドレス。 x86 ベースおよび x64 ベースです。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>%</strong>セグメント: [オフセット]</p></td>
<td align="left"><p>セグメント化された 32 ビットまたは 64 ビット アドレスです。 x86 ベースおよび x64 ベースです。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>%</strong>[オフセット]</p></td>
<td align="left"><p>仮想メモリ空間で絶対アドレス (32 ビットまたは 64 ビット)。 x86 ベースおよび x64 ベースです。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>名前 [ <strong> +</strong> | <strong>−</strong> ] のオフセット</p></td>
<td align="left"><p>フラットに、32 ビットまたは 64 ビットのアドレス。 <em>名前</em>任意の記号を指定できます。 <em>オフセット</em>オフセットを指定します。 このオフセットは、そのプレフィックスを示しますどのアドレス モードを指定できます。 プレフィックスは、既定のモードのアドレスがないを指定します。 オフセットは、正 (+) または負の値 (−) 値として指定できます。</p></td>
</tr>
</tbody>
</table>

 

使用して、 [ **dg (表示セレクター)** ](dg--display-selector-.md)セグメント記述子情報を表示するコマンド。

MASM の式で使用することも、 **poi**を任意のポインターを逆参照演算子。 たとえば、アドレス 0x00123456 でポインターが指すアドレス場所 0x00420000、次の 2 つのコマンドは同等です。

```dbgcmd
0:000> dd 420000 
0:000> dd poi(123456) 
```

C++ の式では、ポインターは、C++ のポインターのように動作します。 ただし、数値が整数として解釈されます。 ある場合に、実際の数、最初に、次の例はキャストする必要があります。

```dbgcmd
0:000> dd *( (long*) 0x123456 ) 
```

いくつか[擬似レジスタ](pseudo-register-syntax.md)もプログラム カウンターの現在の場所など、一般的なアドレスを保持します。

元のソース ファイル名と行番号を指定しても、アプリケーション内のアドレスを指定できます。 この情報を指定する方法の詳細については、次を参照してください。[ソース行構文](source-line-syntax.md)します。

### <a name="span-idaddressrangesspanspan-idaddressrangesspanaddress-ranges"></a><span id="address_ranges"></span><span id="ADDRESS_RANGES"></span>アドレス範囲

アドレスの範囲は、アドレスのペアをするか、アドレスとオブジェクトの数を指定できます。

アドレスのペアで範囲を指定するには、開始アドレスと終了アドレスを指定します。 たとえば、次の例では、アドレス 0x00001000 から始まる 8 バイトの範囲は。

```dbgcmd
0x00001000  0x00001007
```

アドレスの範囲をアドレスとオブジェクトの数を指定するには、アドレス引数、文字 (大文字または小文字)、L、および引数の値を指定します。 アドレスは、開始アドレスを指定します。 値は、検査または表示するオブジェクトの数を指定します。 オブジェクトのサイズは、コマンドに依存します。 たとえば、オブジェクトのサイズが 1 バイトの場合は、次の例はアドレス 0x00001000 から始まる 8 バイトの範囲。

```dbgcmd
0x00001000  L8
```

ただし、オブジェクトのサイズが (32 ビットまたは 4 バイト) は、ダブル ワードである場合は、次の 2 つ範囲は、8 バイトの範囲を提供します。

```dbgcmd
0x00001000  0x00001007
0x00001000  L2
```

値を指定するその他の 2 つの方法があります (、**L * * * サイズ*指定子の範囲)。

-   **L でしょうか。** *サイズ*と同じ意味 (疑問符) で **L * * * サイズ*ことを除いて、 **L でしょうか。** *サイズ*デバッガーの範囲の自動制限を削除します。 大きな範囲は、入力ミスがあるため、256 MB の範囲の制限がある一般に、します。 使用する必要がありますを 256 MB を超える範囲を指定する場合、 **L でしょうか。** *サイズ*構文。

-   **L-** *サイズ*(ハイフン) で、長さの範囲を指定します。*サイズ*指定したアドレスに終了します。 たとえば、 **80000000 L20**を通じて 0x8000001F、0x80000000 から範囲を指定しますおよび**80000000 L-20** 0x7fffffff 0x7FFFFFE0 から範囲を指定します。

アドレス範囲を要求するいくつかのコマンドでは、引数として 1 つのアドレスをそのまま使用します。 このような状況ではのコマンドは、範囲のサイズを計算するのにいくつか既定のオブジェクトの数を使用します。 通常、アドレス範囲は、最後のパラメーターのコマンドは、この構文を許可します。 正確な構文と各コマンドの既定の範囲のサイズは、各コマンドのリファレンス トピックを参照してください。

 

 






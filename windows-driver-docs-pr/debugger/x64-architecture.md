---
title: x64 アーキテクチャ
description: x64 アーキテクチャ
ms.assetid: 6c0d92d5-cb16-4909-bae5-39fc5c15f736
keywords:
- x64 プロセッサ、アーキテクチャ
- レジスタ、x64 プロセッサ
- x64 プロセッサを登録します
ms.date: 03/16/2018
ms.localizationpriority: medium
ms.openlocfilehash: c0b3f92c2864a6d855d545934d7d35439d1653ce
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63381913"
---
# <a name="x64-architecture"></a>x64 アーキテクチャ


## <span id="ddk_x64_architecture_dbg"></span><span id="DDK_X64_ARCHITECTURE_DBG"></span>


アーキテクチャの x86 の下位互換性のある拡張機能は、x64。 X86 と同じですが、従来の 32 ビット モードと新しい 64 ビット モードを提供します。

"X64"という用語には、AMD 64 と Intel64 の両方が含まれています。 命令セットは、同一の近くにです。

### <a name="span-idregistersspanspan-idregistersspanspan-idregistersspanregisters"></a><span id="Registers"></span><span id="registers"></span><span id="REGISTERS"></span>レジスタ

x64 では、x86 の 8 つの汎用レジスタを 64 ビットを拡張し、8 つの新しい 64 ビット レジスタを追加します。 64 ビット レジスタの 64 ビット拡張ではそのため、たとえば"r"で始まる名前がある**eax**呼びます**rax**します。 という名前の新しいレジスタ**r8**を通じて**r15**します。

下位 32 ビット、16 ビット、および各レジスタの 8 ビットは、オペランドでは、直接アドレス指定可能です。 このようなレジスタが含まれます**esi**が下位の 8 ビットは以前にアドレス指定可能でした。 次の表では、64 ビット レジスタの下位部分のアセンブリ言語の名前を指定します。

<table>
<colgroup>
<col width="25%" />
<col width="25%" />
<col width="25%" />
<col width="25%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">64 ビット レジスタ</th>
<th align="left">下位の 32 ビット</th>
<th align="left">下位 16 ビット</th>
<th align="left">下位 8 ビット</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><strong>rax</strong></p></td>
<td align="left"><p><strong>eax</strong></p></td>
<td align="left"><p><strong>Ax</strong></p></td>
<td align="left"><p><strong>Al</strong></p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>rbx</strong></p></td>
<td align="left"><p><strong>ebx</strong></p></td>
<td align="left"><p><strong>bx</strong></p></td>
<td align="left"><p><strong>bl</strong></p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>rcx</strong></p></td>
<td align="left"><p><strong>ecx</strong></p></td>
<td align="left"><p><strong>cx</strong></p></td>
<td align="left"><p><strong>cl</strong></p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>rdx</strong></p></td>
<td align="left"><p><strong>edx</strong></p></td>
<td align="left"><p><strong>dx</strong></p></td>
<td align="left"><p><strong>dl</strong></p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>rsi</strong></p></td>
<td align="left"><p><strong>esi</strong></p></td>
<td align="left"><p><strong>si</strong></p></td>
<td align="left"><p><strong>sil</strong></p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>rdi</strong></p></td>
<td align="left"><p><strong>edi</strong></p></td>
<td align="left"><p><strong>di</strong></p></td>
<td align="left"><p><strong>受け取りました</strong></p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>rbp</strong></p></td>
<td align="left"><p><strong>ebp</strong></p></td>
<td align="left"><p><strong>bp</strong></p></td>
<td align="left"><p><strong>bpl</strong></p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>rsp</strong></p></td>
<td align="left"><p><strong>esp</strong></p></td>
<td align="left"><p><strong>sp</strong></p></td>
<td align="left"><p><strong>spl</strong></p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>r8</strong></p></td>
<td align="left"><p><strong>r8d</strong></p></td>
<td align="left"><p><strong>r8w</strong></p></td>
<td align="left"><p><strong>r8b</strong></p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>r9</strong></p></td>
<td align="left"><p><strong>r9d</strong></p></td>
<td align="left"><p><strong>r9w</strong></p></td>
<td align="left"><p><strong>r9b</strong></p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>r10</strong></p></td>
<td align="left"><p><strong>r10d</strong></p></td>
<td align="left"><p><strong>r10w</strong></p></td>
<td align="left"><p><strong>r10b</strong></p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>r11</strong></p></td>
<td align="left"><p><strong>r11d</strong></p></td>
<td align="left"><p><strong>r11w</strong></p></td>
<td align="left"><p><strong>r11b</strong></p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>r12</strong></p></td>
<td align="left"><p><strong>r12d</strong></p></td>
<td align="left"><p><strong>r12w</strong></p></td>
<td align="left"><p><strong>r12b</strong></p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>r13</strong></p></td>
<td align="left"><p><strong>r13d</strong></p></td>
<td align="left"><p><strong>r13w</strong></p></td>
<td align="left"><p><strong>r13b</strong></p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>r14</strong></p></td>
<td align="left"><p><strong>r14d</strong></p></td>
<td align="left"><p><strong>r14w</strong></p></td>
<td align="left"><p><strong>r14b</strong></p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>r15</strong></p></td>
<td align="left"><p><strong>r15d</strong></p></td>
<td align="left"><p><strong>r15w</strong></p></td>
<td align="left"><p><strong>r15b</strong></p></td>
</tr>
</tbody>
</table>

 

操作は 32 ビット subregister への出力は、全体の 64 ビット レジスタに自動的にゼロ拡張されます。 8 ビットまたは 16 ビット subregisters を出力する操作は*いない*ゼロ拡張されます (これは、互換性のある x86 動作)。

上位の 8 ビット**ax**、 **bx**、 **cx**、および**dx**はまだとしてアドレス指定できる**ah**、 **bh**、 **ch**、 **dh**オペランドのすべての型では使用できませんが、します。

命令ポインター **eip**、および**フラグ**レジスタは、64 ビットに拡張されています (**rip**と**rflags**、それぞれ) もします。

X64 プロセッサには、浮動小数点レジスタのいくつかのセットも用意されています。

-   8 個の 80 ビット x87 を登録します。

-   8 個の 64 ビット MMX レジスタ。 (これらは x87 と重複を登録します)。

-   8 個の 128 ビット SSE レジスタの元のセットは、16 個に増加します。

### <a name="span-idcallingconventionsspanspan-idcallingconventionsspanspan-idcallingconventionsspancalling-conventions"></a><span id="Calling_Conventions"></span><span id="calling_conventions"></span><span id="CALLING_CONVENTIONS"></span>呼び出し規則

X86 とは異なり、C と C++ コンパイラは呼び出し規約を 1 つを x64 でのみサポートします。 この呼び出し規則は、x64 でレジスタの使用可能な数の増加の利点を受け取る。

-   最初の 4 つの整数またはポインター パラメーターが渡された、 **rcx**、 **rdx**、 **r8**、および**r9**を登録します。

-   最初の 4 つの浮動小数点パラメーターが渡される最初の 4 つの SSE レジスタに**xmm0**-**xmm3**します。

-   呼び出し元には、レジスタで渡される引数をスタックに領域が確保されます。 呼び出された関数では、この領域を使用して、スタック レジスタの内容の書き込み。

-   追加の引数はスタックで渡されます。

-   整数またはポインターの戻り値が返される、 **rax**で浮動小数点戻り値が返されるときに、登録**xmm0**します。

-   **rax**、 **rcx**、 **rdx**、 **r8**-**r11**は揮発性です。

-   **rbx**、 **rbp**、 **rdi**、 **rsi**、 **r12**-**r15**不揮発性には.

C++ の呼び出し規約は非常に似ています。、**この**ポインターは暗黙的な最初のパラメーターとして渡されます。 次の 3 つのパラメーターは、残りの部分がスタックに渡されるときに、レジスタに渡されます。

### <a name="span-idaddressingmodesspanspan-idaddressingmodesspanspan-idaddressingmodesspanaddressing-modes"></a><span id="Addressing_Modes"></span><span id="addressing_modes"></span><span id="ADDRESSING_MODES"></span>アドレッシング モード

64 ビット モードでアドレス指定モードに似ていますが、x86 と一致しません。

- 64 ビット レジスタを参照するは、64 ビットの有効桁数で自動的に実行されます。 (たとえば**mov rax、 \[rbx\]** から始まる 8 バイトの移動**rbx**に**rax**)。

- 特殊な形式の**mov** 64 ビットの即時定数または定数が追加されました命令アドレス。 その他のすべての手順では、即時の定数または定数のアドレスは引き続き 32 ビットです。

- x64 を提供する新しい**rip**-相対アドレス モード。 1 つの定数のアドレスを参照する手順についてからのオフセットとしてエンコードされます**rip**します。 たとえば、 **mov rax、 \[**  <em>addr</em> **\]** 命令に移動しますから始まる 8 バイト*addr*  + **rip**に**rax**します。

手順についてなど**jmp**、**呼び出す**、**プッシュ**、および**pop**、命令ポインターとスタック ポインターを暗黙的に参照します。64 ビット x64 に登録された時点とは、それらを扱います。

 
## <a name="see-also"></a>関連項目

[X86 64 Wikipedia](https://en.wikipedia.org/wiki/X86-64)

[AMD 64 の開発者向けリソース](https://developer.amd.com/resources/)


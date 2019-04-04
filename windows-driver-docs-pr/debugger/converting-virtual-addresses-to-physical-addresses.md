---
title: 仮想アドレスを物理アドレスに変換します。
description: 仮想アドレスを物理アドレスに変換します。
ms.assetid: 5b3d19df-09cc-4131-ae64-5ce64d986df3
keywords:
- 仮想アドレス
- 仮想アドレス、物理アドレスに変換します。
- 物理アドレス
- 物理アドレス、仮想アドレスからの変換
- アドレス
- 変換する物理仮想アドレス
- メモリ、仮想アドレス
- メモリ、物理アドレス
ms.date: 05/04/2018
ms.localizationpriority: medium
ms.openlocfilehash: e870d2322fc236b90131af0ac45166caee44f224
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56559873"
---
# <a name="converting-virtual-addresses-to-physical-addresses"></a>仮想アドレスを物理アドレスに変換します。

## <span id="ddk_converting_virtual_addresses_to_physical_addresses_dbg"></span><span id="DDK_CONVERTING_VIRTUAL_ADDRESSES_TO_PHYSICAL_ADDRESSES_DBG"></span>


ほとんどのデバッガー コマンドでは、その入力と出力として、物理アドレス、仮想アドレスを使用します。 ただし、物理アドレスを持つことが便利なことができる時間があります。

仮想アドレスを物理アドレスに変換する 2 つの方法があります: を使用して、 **! vtop**拡張機能を使用して、 **! pte**拡張機能。

Windows での仮想アドレスの概要については、[仮想アドレス空間](https://docs.microsoft.com/windows-hardware/drivers/gettingstarted/virtual-address-spaces)を参照してください。 


### <a name="span-idaddressconversionusingvtopspanspan-idaddressconversionusingvtopspanaddress-conversion-using-vtop"></a><span id="address_conversion_using__vtop"></span><span id="ADDRESS_CONVERSION_USING__VTOP"></span>変換を使用して対処! vtop

MyApp.exe プロセスが実行されていると、仮想アドレス 0x0012F980 を調査することは、ターゲット コンピューターをデバッグするいるとします。 ここで使用すると、プロシージャ、 **! vtop**対応する物理アドレスを決定する拡張機能。

**仮想アドレスに変換する物理アドレスを使用して、! vtop**

1.  16 進数で動作していることを確認します。 必要に応じて、現在のベースを設定する場合、 [ **N 16** ](n--set-number-base-.md)コマンド。

2.  確認、*バイト インデックス*のアドレス。 この数は仮想アドレスの最下位の 12 ビットです。 そのため、仮想アドレス 0x0012F980 は 0x980 のバイト インデックスを持ちます。

3.  確認、*ディレクトリ ベース*のアドレスを使用して、 [ **! プロセス**](-process.md)拡張機能。

    ```dbgcmd
    kd> !process 0 0
    **** NT ACTIVE PROCESS DUMP ****
    ....
    PROCESS ff779190  SessionId: 0  Cid: 04fc    Peb: 7ffdf000  ParentCid: 0394
     DirBase: 098fd000  ObjectTable: e1646b30  TableSize:   8.
        Image: MyApp.exe
    ```

4.  確認、*ページ フレーム番号*ディレクトリ ベースの。 これは後続の 3 つの 16 進数 0 なしの基本ディレクトリだけです。 ページ フレームの数が 0x098FD であるために、この例では、ディレクトリ情報は 0x098FD000、です。

5.  使用して、 [ **! vtop** ](-vtop.md)拡張機能。 この拡張機能の最初のパラメーターは、ページ フレームの数をする必要があります。 2 番目のパラメーターの **! vtop**仮想のアドレスを対象にする必要があります。

    ```dbgcmd
    kd> !vtop 98fd 12f980
    Pdi 0 Pti 12f
    0012f980 09de9000 pfn(09de9)
    ```

    最後の行に表示される 2 つ目の数字は、物理ページの先頭の物理アドレスです。

6.  ページの先頭のアドレスにバイトのインデックスを追加します。0x09DE9000 + 0x980 = 0x09DE9980 します。 これは、必要な物理アドレスです。

各アドレスのメモリを表示することによってこの計算が正しく行われたことを確認できます。 [ **! D\\**  * ](-db---dc---dd---dp---dq---du---dw.md)拡張機能は、指定した物理アドレスにメモリを表示します。

```dbgcmd
kd> !dc 9de9980
# 9de9980 6d206e49 726f6d65 00120079 0012f9f4 In memory.......
# 9de9990 0012f9f8 77e57119 77e8e618 ffffffff .....q.w...w....
# 9de99a0 77e727e0 77f6f13e 77f747e0 ffffffff .'.w>..w.G.w....
# 9de99b0 .....
```

[ **D\* (表示メモリ)** ](d--da--db--dc--dd--dd--df--dp--dq--du--dw--dw--dyb--dyd--display-memor.md)コマンドは仮想アドレスを使用して、引数として。

```dbgcmd
kd> dc 12f980
0012f980  6d206e49 726f6d65 00120079 0012f9f4  In memory.......
0012f990  0012f9f8 77e57119 77e8e618 ffffffff  .....q.w...w....
0012f9a0  77e727e0 77f6f13e 77f747e0 ffffffff  .'.w>..w.G.w....
0012f9b0  .....
```

結果が同じであるために、物理アドレス 0x09DE9980 は実際に仮想アドレス 0x0012F980 に対応することを示します。

### <a name="span-idaddressconversionusingptespanspan-idaddressconversionusingptespanaddress-conversion-using-pte"></a><span id="address_conversion_using__pte"></span><span id="ADDRESS_CONVERSION_USING__PTE"></span>変換を使用して対処! pte

ここでも、仮想、調査するいると仮定 MyApp.exe プロセスに属する 0x0012F980 に対処します。 ここでは、プロシージャを使用すると、 **! pte**対応する物理アドレスを決定する拡張機能。

**仮想アドレスに変換する物理アドレスを使用して、! pte**

1.  16 進数で動作していることを確認します。 必要に応じて、現在のベースを設定する場合、 [ **N 16** ](n--set-number-base-.md)コマンド。

2.  確認、*バイト インデックス*のアドレス。 この数は仮想アドレスの最下位の 12 ビットです。 そのため、仮想アドレス 0x0012F980 は 0x980 のバイト インデックスを持ちます。

3.  設定、[プロセス コンテキスト](changing-contexts.md#process-context)任意のプロセスに。

    ```dbgcmd
    kd> !process 0 0
    **** NT ACTIVE PROCESS DUMP ****
    ....
    PROCESS ff779190  SessionId: 0  Cid: 04fc    Peb: 7ffdf000  ParentCid: 0394
        DirBase: 098fd000  ObjectTable: e1646b30  TableSize:   8.
        Image: MyApp.exe

    kd> .process /p ff779190
    Implicit process is now ff779190
    .cache forcedecodeuser done
    ```

4.  使用して、 [ **! pte** ](-pte.md)引数として仮想アドレスを持つ拡張機能。 これには、2 つの列の情報が表示されます。 左側の列は、このアドレスのページ ディレクトリ エントリ (PDE) を説明します。右側の列には、そのページ テーブル エントリ (PTE) について説明します。

    ```dbgcmd
    kd> !pte 12f980
                   VA 0012f980
    PDE at   C0300000        PTE at C00004BC
    contains 0BA58067      contains 09DE9067
    pfn ba58 ---DA--UWV    pfn 9de9 ---DA--UWV
    ```

5.  右側の列の最後の行を確認します。 "Pfn 9de9"表記法が表示されます。 0x9DE9 数は、*ページ フレーム番号*(PFN) のこの PTE します。 0x1000 (たとえば、12 ビットを左にシフト) ページ フレームの数を乗算します。 0x09DE9000、結果は、ページの先頭の物理アドレスです。

6.  ページの先頭のアドレスにバイトのインデックスを追加します。0x09DE9000 + 0x980 = 0x09DE9980 します。 これは、必要な物理アドレスです。

これは、以前のメソッドによって取得した結果は同じです。

### <a name="span-idconvertingaddressesbyhandspanspan-idconvertingaddressesbyhandspanconverting-addresses-by-hand"></a><span id="converting_addresses_by_hand"></span><span id="CONVERTING_ADDRESSES_BY_HAND"></span>アドレスを手動で変換します。

ただし、 **! ptov**と**pte**拡張機能の仮想アドレスを物理アドレスに変換する最も簡単な方法を指定する、この変換は手動でも実行できます。 このプロセスの説明には、仮想メモリ アーキテクチャの詳細の一部のライトで詳しく説明します。

構造体のメモリ、プロセッサとハードウェアの構成に応じて、サイズによって異なります。 この例では、x86 から取得物理アドレス拡張 (PAE) を有効にしていないシステム。

0x0012F980 を使用して、もう一度仮想アドレスとして、まず手動でまたはを使用して、バイナリに変換する、 [ **(番号の形式の表示) .formats** ](-formats--show-number-formats-.md)コマンド。

```dbgcmd
kd> .formats 12f980
Evaluate expression:
  Hex:     0012f980
  Decimal: 1243520
  Octal:   00004574600
  Binary:  00000000 00010010 11111001 10000000
  Chars:   ....
  Time:    Thu Jan 15 01:25:20 1970
  Float:   low 1.74254e-039 high 0
  Double:  6.14381e-318
```

この仮想のアドレスは、3 つのフィールドの組み合わせです。 ビット 0 ~ 11 は、バイトのインデックスです。 ビット 12 ~ 21 は、ページのテーブルのインデックスです。 22 ~ 31 のビットは、ページのディレクトリのインデックスです。 フィールドを分離するには、次の必要があります。

```dbgcmd
0x0012F980  =  0y  00000000 00   010010 1111   1001 10000000
```

これは、仮想アドレスの 3 つの部分を公開します。

-   ディレクトリのページのインデックス = 0y0000000000 0x0 を =

-   ページ テーブルのインデックス = 0y0100101111 0x12F を =

-   バイト インデックス = 0y100110000000 0x980 を =

お使いのシステムの 3 つの追加情報、必要があります。

-   各 PTE のサイズ。 これは、非 PAE x86 システムでは 4 バイトです。

-   ページのサイズ。 これは、0x1000 バイトです。

-   PTE\_ベースの仮想アドレス。 非 PAE システムでは、これは 0xC0000000 です。

このデータを使用して、PTE 自体のアドレスを計算できます。

```dbgcmd
PTE address   =   PTE_BASE  
                + (page directory index) * PAGE_SIZE
                + (page table index) * sizeof(MMPTE)
              =   0xc0000000
                + 0x0   * 0x1000
                + 0x12F * 4
              =   0xC00004BC
```

これは、PTE のアドレスです。 PTE は、32 ビット DWORD です。 その内容を確認します。

```dbgcmd
kd> dd 0xc00004bc L1
c00004bc  09de9067
```

この PTE は 0x09DE9067 の値を持ちます。 これは、2 つのフィールドのされます。

-   PTE の下位の 12 ビットは、*状態フラグ*します。 この場合、これらのフラグが 0x067--を等しくまたはバイナリ、0y000001100111 でします。 状態フラグの詳細については、、 [ **! pte** ](-pte.md)リファレンス ページを参照してください。

-   PTE の上位 20 のビットが等しく、*ページ フレーム番号*(PFN) の PTE。 ここで、PFN は 0x09DE9 です。

物理ページの最初の物理アドレスは、0x1000 (左 12 ビットのシフト) を掛けた PFN です。 バイト インデックスは、このページのオフセットです。 したがって、探している物理アドレスは、0x09DE9000 + 0x980 = 0x09DE9980 です。 これは、以前の方法で取得した結果は同じです。

 

 






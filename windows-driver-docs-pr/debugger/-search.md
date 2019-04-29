---
title: '[検索]'
description: Search 拡張機能は、指定した条件に一致するポインター-サイズのデータの物理メモリのページを検索します。
ms.assetid: 5f9d4e50-c389-4309-8851-0f5069b1b66e
keywords:
- Windows のデバッグを検索します。
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- search
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 893752195106244a17279b41d2f25b6857581f52
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63338843"
---
# <a name="search"></a>!search


**! 検索**拡張機能は、指定した条件に一致するポインター-サイズのデータの物理メモリ内のページを検索します。

構文

```dbgcmd
!search [-s] [-p] Data [ Delta [ StartPFN [ EndPFN ]]] 
!search -?
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>パラメーター


<span id="_______-s______"></span><span id="_______-S______"></span> **-s**   
検索中に無視するシンボルのチェック エラーが発生します。 これが多すぎます「が正しくないシンボル カーネルを」エラーが発生する場合に便利です。

<span id="_______-p______"></span><span id="_______-P______"></span> **-p**   
値と、*データ*任意の符号拡張を禁止するには、32 ビット値として解釈されます。

<span id="_______Data______"></span><span id="_______data______"></span><span id="_______DATA______"></span> *データ*   
検索するデータを指定します。 *データ*(32 ビットまたは 64 ビット)、ターゲット システム上のポインターのサイズを指定する必要があります。 値と完全に一致*データ*が常に表示されます。 値に応じて他の一致が同様に、表示される*デルタ*; 詳細については、以下の「解説」を参照してください。

<span id="_______Delta______"></span><span id="_______delta______"></span><span id="_______DELTA______"></span> *デルタ*   
メモリ内の値との値の許容の違いを示す*データ*します。 詳細については、以下の「解説」を参照してください。

<span id="_______StartPFN______"></span><span id="_______startpfn______"></span><span id="_______STARTPFN______"></span> *StartPFN*   
検索対象の範囲の先頭のページのフレーム数 (PFN) を指定します。 これを省略した場合、最下位の物理的なページで、検索が開始されます。

<span id="_______EndPFN______"></span><span id="_______endpfn______"></span><span id="_______ENDPFN______"></span> *EndPFN*   
検索対象の範囲の最後のページのフレーム数 (PFN) を指定します。 これを省略した場合、検索は、最高の物理的なページで終了します。

<span id="_______-_______"></span> **-?**   
この拡張機能のデバッガー コマンド ウィンドウでヘルプを表示します。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL

Kdexts.dll

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>追加情報

表示し、物理メモリの検索方法の詳細について参照して[読み取りと書き込みメモリ](reading-and-writing-memory.md)します。

<a name="remarks"></a>注釈
-------

場合*StartPFN*と*EndPFN*は指定すると、これらが表示されます、先頭と範囲の最後のページ フレーム番号として物理メモリで検索します。 フレームのページ番号の詳細については、次を参照してください。[仮想のアドレスを物理アドレスを変換する](converting-virtual-addresses-to-physical-addresses.md)します。 場合*StartPFN*と*EndPFN*は省略すると、すべての物理メモリが検索されます。

すべてのヒットが表示されます。

**! 検索**拡張機能はの指定したページ範囲内のすべてのメモリを検索し、各 ULONG を調べる\_PTR 揃えの値。 次の条件の少なくとも 1 つを満たす値が表示されます。

-   値が一致する*データ*正確にします。

-   デルタが 0 または省略された場合。値が異なる*データ*ビットが 1 つ。

-   デルタが 0 以外の場合。値が異なる*データ*によって最大*デルタ*。 つまり、値が範囲内にある\[データ - デルタ、データとデルタ\]します。

-   デルタが 0 以外の場合。値は、1 つのビットで (データの差分) の範囲の最小値とは異なります。

ほとんどの場合、*データ*、興味のあるアドレスがすべて ULONG 指定\_PTR 規模のデータを指定することができます。

デバッガーの検索エンジンの構造は、すべてのメモリ (またはこれらの構造を格納している任意の範囲) を検索する場合、対象のコンピューター上のメモリ内にあるために、構造自体が配置される領域内の一致が表示されます。 これらの一致を排除する必要がある場合は、ランダムな値の検索を行うこれは、デバッガーの検索の構造がある場所に示します。

例をいくつか紹介します。 次は PFN 0x237D 0x80001230 ~ 0x80001238、包括的な値のメモリ ページを検索します。

```dbgcmd
kd> !search 80001234 4 237d 237d 
```

次は PFN 0x2370 に 0x237F 0x0F100F0F の 1 つのビット内にある値の範囲のメモリ ページを検索します。 完全一致は太字で示されます。他のユーザーは、1 つのビットで無効にします。

```dbgcmd
kd> !search 0f100f0f 0 2370 237f
Searching PFNs in range 00002370 - 0000237F for [0F100F0F - 0F100F0F]

Pfn      Offset   Hit      Va       Pte      
- - - - - - - - - - - - - - - - - - -
0000237B 00000368 0F000F0F 01003368 C0004014 
0000237C 00000100 0F100F0F 01004100 C0004014 
0000237D 000003A8 0F100F0F 010053A8 C0004014 
0000237D 000003C8 0F100F8F 010053C8 C0004014 
0000237D 000003E8 0F100F0F 010053E8 C0004014 
0000237D 00000408 0F100F0F 01005408 C0004014 
0000237D 00000428 0F100F8F 01005428 C0004014 
Search done.
```

表示内の列は次のとおりです。**Pfn**はページのページのフレーム数 (PFN)**オフセット**; そのページ上のオフセットです**ヒット**はそのアドレスの値です。**Va** (これが存在し、決定できます) 場合はこの物理アドレス; にマップされている仮想アドレスには**Pte**ページ テーブル エントリ (PTE) です。

物理アドレスを計算するには、3 つの 16 進数字 (12 ビット) のまま PFN をシフトし、オフセットを追加します。 たとえば、テーブルの最後の行には、仮想アドレス 0x0237D000 + 0x428 = 0x02347D428 です。

 

 






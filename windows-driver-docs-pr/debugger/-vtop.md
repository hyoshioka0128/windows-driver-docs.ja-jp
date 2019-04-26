---
title: vtop
description: Vtop 拡張機能では、仮想のアドレスを対応する物理アドレスに変換し、他のページ テーブルとページのディレクトリ情報を表示します。
ms.assetid: 41f4accc-3eb9-4406-a6cc-a05022166e14
keywords:
- Windows デバッグ vtop
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- vtop
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 343265d0d42a14ed1c0780ca66831e8112d60234
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63341780"
---
# <a name="vtop"></a>!vtop


**! Vtop**拡張機能は、対応する物理アドレスを仮想アドレスに変換し、他のページ テーブルとページのディレクトリ情報が表示されます。

構文

```dbgcmd
!vtop PFN VirtualAddress 
!vtop 0 VirtualAddress 
```

## <a name="span-idddkvtopdbgspanspan-idddkvtopdbgspanparameters"></a><span id="ddk__vtop_dbg"></span><span id="DDK__VTOP_DBG"></span>パラメーター


<span id="_______DirBase______"></span><span id="_______dirbase______"></span><span id="_______DIRBASE______"></span> *DirBase*   
プロセスの基本クラスをディレクトリを指定します。 各プロセスでは、独自の仮想アドレス空間があります。 使用して、 [ **! プロセス**](-process.md)拡張機能、プロセスのディレクトリの基数を判断します。

<span id="_______PFN______"></span><span id="_______pfn______"></span> *PFN*   
プロセスのディレクトリ ベースのページのフレーム数 (PFN) を指定します。

<span id="_______0______"></span> **0**   
により **! vtop**現在を使用する[プロセス コンテキスト](changing-contexts.md#process-context)アドレス変換します。

<span id="_______VirtualAddress______"></span><span id="_______virtualaddress______"></span><span id="_______VIRTUALADDRESS______"></span> *virtualAddress*   
そのページが必要な仮想アドレスを指定します。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL

Kdexts.dll

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>追加情報

これらの結果を実現するための他のメソッドでは、次を参照してください。[仮想のアドレスを物理アドレスを変換する](converting-virtual-addresses-to-physical-addresses.md)します。 参照してください[ **! ptov**](-ptov.md)します。 ページのテーブルとページのディレクトリについては、次を参照してください。 *Microsoft Windows internals 』*、Mark Russinovich と David Solomon します。

<a name="remarks"></a>注釈
-------

このコマンドを使用する、 [ **! プロセス**](-process.md)拡張機能、プロセスのディレクトリの基数を判断します。 (つまり、12 ビット数の右シフト) によって次の 3 つの後続の 16 進数 0 を削除することで、このディレクトリ ベースのページのフレーム数 (PFN) を確認できます。

以下に例を示します。

```dbgcmd
kd> !process 0 0
**** NT ACTIVE PROCESS DUMP ****
....
PROCESS ff779190  SessionId: 0  Cid: 04fc    Peb: 7ffdf000  ParentCid: 0394
 DirBase: 098fd000  ObjectTable: e1646b30  TableSize:   8.
    Image: MyApp.exe
```

0x098FD000 ディレクトリ ベースなので、その PFN は 0x098FD です。

```dbgcmd
kd> !vtop 98fd 12f980
Pdi 0 Pti 12f
0012f980 09de9000 pfn(09de9)
```

後続の 3 つのゼロは省略可能な方法に注意してください。 **! Vtop**拡張機能は、ページ directory インデックス (PDI)、ページ テーブルのインデックス (PTI)、最初に入力した仮想のアドレス、物理ページのページのフレーム数 (PFN) の先頭の物理アドレスが表示されます。ページ テーブル エントリ (PTE)。

仮想アドレス 0x0012F980 物理アドレスに変換する場合は、単に、最後の 3 つの 16 進数字 (0x980) を受け取り、物理アドレス (0x09DE9000) ページの先頭に追加する必要があります。 これは、物理アドレス 0x09DE9980 を与えます。

次の 3 つのゼロを削除し、完全なディレクトリを基本に渡すを忘れた場合 **! vtop** PFN ではなく、結果は通常なる正しい。 これはときに **! vtop**番号は PFN をするのには大きすぎて、その右-シフトが代わりに番号を使用して 12 ビット。

```dbgcmd
kd> !vtop 98fd 12f980
Pdi 0 Pti 12f
0012f980 09de9000 pfn(09de9)

kd> !vtop 98fd000 12f980
Pdi 0 Pti 12f
0012f980 09de9000 pfn(09de9)
```

ただし、これをお勧め、PFN を常に使用するため、この方法でいくつかのディレクトリの基本値は変換されません。

 

 






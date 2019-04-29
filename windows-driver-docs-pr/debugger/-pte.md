---
title: pte
description: Pte 拡張機能には、ページ テーブル エントリ (PTE) と指定したアドレスのディレクトリ エントリ (PDE) ページが表示されます。
ms.assetid: e5603e58-8d9f-4693-bca2-a319080187cc
keywords:
- ページ テーブル エントリ (PTE)
- PTE (ページ テーブル エントリ)
- ページのディレクトリ エントリ (PDE)
- PDE (ページのディレクトリ エントリ)
- Windows デバッグ pte
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- pte
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 212acb273718c10104b5467cf3d5c00daac45f37
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63334335"
---
# <a name="pte"></a>!pte


**! Pte**拡張機能は、ページ テーブル エントリ (PTE) と指定したアドレスのディレクトリ エントリ (PDE) ページが表示されます。

構文

```dbgcmd
!pte VirtualAddress 
!pte PTE 
!pte LiteralAddress 1 
```

## <a name="span-idddkptedbgspanspan-idddkptedbgspanparameters"></a><span id="ddk__pte_dbg"></span><span id="DDK__PTE_DBG"></span>パラメーター


<span id="_______VirtualAddress______"></span><span id="_______virtualaddress______"></span><span id="_______VIRTUALADDRESS______"></span> *virtualAddress*   
ページのテーブルが必要な仮想アドレスを指定します。

<span id="_______PTE______"></span><span id="_______pte______"></span> *PTE*   
実際の PTE のアドレスを指定します。

<span id="_______LiteralAddress_______1______"></span><span id="_______literaladdress_______1______"></span><span id="_______LITERALADDRESS_______1______"></span> *LiteralAddress* **** **1**   
実際の PTE または PDE のアドレスを指定します。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL

Kdexts.dll

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>追加情報

ページ テーブル、ページのディレクトリ、およびステータス ビットの説明については、次を参照してください。 *Microsoft Windows internals 』*、Mark Russinovich と David Solomon します。 

<a name="remarks"></a>注釈
-------

1 つのパラメーターを指定し、このパラメーターは、ページのテーブルが格納されているメモリの領域では、住所、デバッガーはこれを扱います、 *PTE*パラメーター。 このパラメーターは、目的の PTE の実際のアドレスとして扱われます、デバッガーがこの PTE と対応する PDE に表示されます。

1 つのパラメーターを指定し、このパラメーターは、このリージョン内のアドレスではありません、デバッガーはこれを扱います、 *VirtualAddress*パラメーター。 このアドレスのマッピングを保持する PDE、PTE が表示されます。

2 つのパラメーターが指定され、2 番目のパラメーターは、かどうか**1** (またはその他の小さい数値)、デバッガーは最初のパラメーターとして扱います*LiteralAddress*します。 このアドレスは PTE の実際のアドレスとも、PDE の実際のアドレスでは解釈され、対応する (および場合によって無効な) データが表示されます。

(x86 または x64 ターゲット コンピューターのみ)デバッガーは 2 つのパラメーターとして扱う場合、2 つのパラメーターが指定され、2 番目のパラメーターが、最初のものより大きい、 *StartAddress*と*EndAddress*します。 次に、コマンドは、指定したメモリ範囲でページごとに Pte を表示します。

すべてのシステム Pte についてを使用して、 [ **! sysptes** ](-sysptes.md)拡張機能。

これは、x86 から対象のコンピューター。

```dbgcmd
kd> !pte 801544f4
801544F4  - PDE at C0300800        PTE at C0200550
          contains 0003B163      contains 00154121
        pfn 3b G-DA--KWV    pfn 154 G--A--KRV
```

この例の最初の行では、調査中の仮想アドレスを言い換えます。 このアドレスの仮想物理マッピングに関する情報を含む、PDE と PTE の仮想アドレスを提供します。

2 行目は、PDE と PTE の実際の内容を示します。

3 行目は、次の内容を受け取り、ページ フレーム番号 (PFN) とステータス ビットに分割して、それらを分析します。

参照してください、 [ **! pfn** ](-pfn.md)拡張機能または[仮想のアドレスを物理アドレスを変換する](converting-virtual-addresses-to-physical-addresses.md)解釈して PFN を使用する方法についてのセクション。

X86 または x64 のターゲット コンピューターで、PDE と PTE ステータス ビットは、次の表に表示されます。 **! Pte**表示では、英大文字、ダッシュ、これらのビットを示すし、も情報を追加します。

<table>
<colgroup>
<col width="25%" />
<col width="25%" />
<col width="25%" />
<col width="25%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">ビット</th>
<th align="left">ときに表示される設定</th>
<th align="left">オフにすると表示</th>
<th align="left">意味</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>0x200</p></td>
<td align="left"><p>C</p></td>
<td align="left"><p>-</p></td>
<td align="left"><p>書き込み時にコピーします。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x100</p></td>
<td align="left"><p>G</p></td>
<td align="left"><p>-</p></td>
<td align="left"><p>グローバルです。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x80</p></td>
<td align="left"><p>L</p></td>
<td align="left"><p>-</p></td>
<td align="left"><p>ラージ ページ。 Pte ではなく、PDEs でのみ発生します。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x40</p></td>
<td align="left"><p>D</p></td>
<td align="left"><p>-</p></td>
<td align="left"><p>ダーティです。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x20</p></td>
<td align="left"><p>A</p></td>
<td align="left"><p>-</p></td>
<td align="left"><p>アクセスします。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x10</p></td>
<td align="left"><p>N</p></td>
<td align="left"><p>-</p></td>
<td align="left"><p>キャッシュを無効にします。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x8</p></td>
<td align="left"><p>T</p></td>
<td align="left"><p>-</p></td>
<td align="left"><p>ライトスルーされます。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x4</p></td>
<td align="left"><p>U</p></td>
<td align="left"><p>K</p></td>
<td align="left"><p>(ユーザー モードまたはカーネル モード) の所有者です。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x2</p></td>
<td align="left"><p>W</p></td>
<td align="left"><p>R</p></td>
<td align="left"><p>書き込み可能または読み取り専用です。 マルチプロセッサ コンピューターおよび任意のコンピューターだけでは、Windows Vista を実行しているまたはそれ以降。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x1</p></td>
<td align="left"><p>V</p></td>
<td align="left"></td>
<td align="left"><p>有効です。</p></td>
</tr>
<tr class="odd">
<td align="left"></td>
<td align="left"><p>E</p></td>
<td align="left"><p>-</p></td>
<td align="left"><p>実行可能ファイルのページです。 ハードウェアの実行/noexecute ビットをサポートしていないプラットフォームなどの多くの x86 システムでは、E は常に表示されます。</p></td>
</tr>
</tbody>
</table>

 

Itanium のターゲット コンピューターでは、PDE と PTE ステータス ビットは、PPE の若干異なります。 Itanium PPE ビットは次のとおりです。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">ときに表示される設定</th>
<th align="left">オフにすると表示</th>
<th align="left">意味</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>V</p></td>
<td align="left"></td>
<td align="left"><p>有効です。</p></td>
</tr>
<tr class="even">
<td align="left"><p>U</p></td>
<td align="left"><p>K</p></td>
<td align="left"><p>(ユーザー モードまたはカーネル モード) の所有者です。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>D</p></td>
<td align="left"><p>-</p></td>
<td align="left"><p>ダーティです。</p></td>
</tr>
<tr class="even">
<td align="left"><p>A</p></td>
<td align="left"><p>-</p></td>
<td align="left"><p>アクセスします。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>W</p></td>
<td align="left"><p>R</p></td>
<td align="left"><p>書き込み可能または読み取り専用です。 マルチプロセッサ コンピューターおよび任意のコンピューターだけでは、Windows Vista を実行しているまたはそれ以降。</p></td>
</tr>
<tr class="even">
<td align="left"><p>E</p></td>
<td align="left"><p>-</p></td>
<td align="left"><p>実行します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>C</p></td>
<td align="left"><p>-</p></td>
<td align="left"><p>書き込み時にコピーします。</p></td>
</tr>
</tbody>
</table>

 

 

 






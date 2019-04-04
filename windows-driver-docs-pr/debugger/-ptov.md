---
title: ptov
description: Ptov 拡張機能は、特定のプロセスの物理-バーチャル マップ全体を表示します。
ms.assetid: 82352d12-4e81-4746-9333-b2cc98eb7a9d
keywords:
- Windows デバッグ ptov
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- ptov
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 586f99d53184a7a0110ee06855beed897f1db97a
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56558053"
---
# <a name="ptov"></a>! ptov


**! Ptov**拡張機能は、特定のプロセスの物理-バーチャル マップ全体を表示します。

```dbgcmd
!ptov DirBase
```

## <a name="span-idddkptovdbgspanspan-idddkptovdbgspanparameters"></a><span id="ddk__ptov_dbg"></span><span id="DDK__PTOV_DBG"></span>パラメーター


<span id="_______DirBase______"></span><span id="_______dirbase______"></span><span id="_______DIRBASE______"></span> *DirBase*   
プロセスの基本クラスをディレクトリを指定します。 ディレクトリ情報を調べるには、 [ **! プロセス**](-process.md)コマンド、および DirBase に表示される値を確認します。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>Windows 2000</strong></p></td>
<td align="left"><p>Kdextx86.dll</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>Windows XP 以降</strong></p></td>
<td align="left"><p>Kdexts.dll</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>注釈
-------

次に例を示します。 最初に、使用[ **.process** ](-process--set-process-context-.md)と[ **! プロセス**](-process.md)現在のプロセスのディレクトリの基数を判断します。

```dbgcmd
1: kd> .process
Implicit process is now 852b4040
1: kd> !process 852b4040 1
PROCESS 852b4040  SessionId: none  Cid: 0004    Peb: 00000000  ParentCid: 0000
    DirBase: 00185000  ObjectTable: 83203000  HandleCount: 663.
    Image: System
    ...
```

この場合は、ディレクトリ ベースは、0x00185000 です。 このアドレスを渡す **! ptov**:

```dbgcmd
1: kd> !ptov 185000
X86PtoV: pagedir 185000, PAE enabled.
15e11000 10000
549e6000 20000
...
60a000 210000
40b000 211000
...
54ad3000 25f000
548d3000 260000
...
d71000 77510000
...
```

左側の列の数値は、このプロセスにマップされている各メモリ ページの物理アドレスです。 右側の列の数値は、マップ先の仮想アドレスです。

合計の表示は、非常に長いです。

64 ビットの例を次に示します。

```dbgcmd
3: kd> .process
Implicit process is now fffffa80`0361eb30
3: kd> !process fffffa80`0361eb30 1
PROCESS fffffa800361eb30
    SessionId: none  Cid: 0004    Peb: 00000000  ParentCid: 0000
    DirBase: 00187000  ObjectTable: fffff8a000002870  HandleCount: 919.
    Image: System
    ...
3: kd> !ptov 187000
Amd64PtoV: pagedir 187000
00000001`034fb000 1d0000
a757c000 1d1000
00000001`0103d000 1d2000
c041e000 1d3000
...
2ed6f000 fffff680`00001000
00000001`13939000 fffff680`00003000
ceefb000 fffff680`00008000
...
```

ディレクトリ ベースは、仮想アドレス変換で使用されている最初のテーブルの物理アドレスです。 このテーブルは、対象のオペレーティング システムとターゲットのオペレーティング システムの物理アドレス拡張 (PAE) が有効になっているかどうかのビット数に応じて、異なる名前を持っています。

64 ビットの Windows ディレクトリ ベースは、ページ マップ レベル 4 (PML4) テーブルの物理アドレスです。 32 ビットの Windows では、PAE を有効に、ディレクトリ ベースは、ページ ディレクトリ ポインター (PDP) テーブルの物理アドレスです。 32 ビットの Windows で無効になっている PAE、ディレクトリの bas はページ ディレクトリ (PD) テーブルの物理アドレス。

関連トピックについては、[ **! vtop** ](-vtop.md)と[仮想のアドレスを物理アドレスを変換する](converting-virtual-addresses-to-physical-addresses.md)を参照してください。 仮想アドレス変換の詳細については、*Microsoft Windows internals 』*、Mark Russinovich と David Solomon を参照してください。 (これらのリソースできない場合がありますのいくつかの言語および国。)

 

 






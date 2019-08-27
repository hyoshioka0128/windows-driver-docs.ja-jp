---
title: ptov
description: Ptov 拡張機能は、特定のプロセスの物理-仮想マップ全体を表示します。
ms.assetid: 82352d12-4e81-4746-9333-b2cc98eb7a9d
keywords:
- ptov Windows デバッグ
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- ptov
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 12c1db265f222894e8b89c851b76ca61b6107aba
ms.sourcegitcommit: 424c435700d8f8a85bdaa83e8ddaab9568c8d347
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/26/2019
ms.locfileid: "70025148"
---
# <a name="ptov"></a>!ptov


**! Ptov**拡張機能は、特定のプロセスの物理-仮想マップ全体を表示します。

```dbgcmd
!ptov DirBase
```

## <a name="span-idddk__ptov_dbgspanspan-idddk__ptov_dbgspanparameters"></a><span id="ddk__ptov_dbg"></span><span id="DDK__PTOV_DBG"></span>パラメータ


<span id="_______DirBase______"></span><span id="_______dirbase______"></span><span id="_______DIRBASE______"></span>*Dirbase*   
プロセスのディレクトリベースを指定します。 ディレクトリベースを特定するには、 [ **! process**](-process.md)コマンドを使用して、dirbase に対して表示される値を確認します。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>Windows 2000</strong></p></td>
<td align="left"><p>Kdextx86</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>Windows XP 以降</strong></p></td>
<td align="left"><p>Kdexts .dll</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>注釈
-------

次に例を示します。 まず、 [ **. process**](-process--set-process-context-.md)および[ **! process**](-process.md)を使用して、現在のプロセスのディレクトリベースを決定します。

```dbgcmd
1: kd> .process
Implicit process is now 852b4040
1: kd> !process 852b4040 1
PROCESS 852b4040  SessionId: none  Cid: 0004    Peb: 00000000  ParentCid: 0000
    DirBase: 00185000  ObjectTable: 83203000  HandleCount: 663.
    Image: System
    ...
```

この場合、ディレクトリベースは0x00185000 です。 このアドレスを **! ptov**に渡します。

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

左の列の数値は、このプロセスのマッピングを持つ各メモリページの物理アドレスです。 右側の列の数値は、マップされている仮想アドレスです。

合計表示は非常に長いです。

64ビットの例を次に示します。

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

ディレクトリベースは、仮想アドレス変換で使用される最初のテーブルの物理アドレスです。 このテーブルの名前は、ターゲットオペレーティングシステムのビット数と、ターゲットオペレーティングシステムに対して物理アドレス拡張 (PAE) が有効になっているかどうかによって異なります。

64ビット Windows の場合、ディレクトリベースはページマップレベル 4 (PML4) テーブルの物理アドレスです。 PAE が有効になっている32ビットの Windows の場合、ディレクトリベースはページディレクトリポインター (PDP) テーブルの物理アドレスです。 PAE が無効になっている32ビットの Windows では、ディレクトリ bas はページディレクトリ (PD) テーブルの物理アドレスです。

関連トピックについては、「 [ **! vtop**](-vtop.md) 」と「[仮想アドレスを物理アドレスに変換する](converting-virtual-addresses-to-physical-addresses.md)」を参照してください。 仮想アドレス変換の詳細については、「 *Microsoft Windows の内部*」 (Mark Russinovich と David ソロモン) を参照してください。

 

 






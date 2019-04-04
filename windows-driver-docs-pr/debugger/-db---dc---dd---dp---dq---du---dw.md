---
title: db, dc, dd, dp, dq, du, dw
description: Db、dc、dd、dp、dq、du、およびデータ ウェアハウスの拡張機能は、ターゲット コンピューター上の指定した物理アドレスにデータを表示します。
ms.assetid: d34eebb7-bc91-4bff-9787-d92f74195ee1
keywords:
- db 拡張機能
- dc の拡張機能
- dd の拡張機能
- 配布ポイントの拡張機能
- dq 拡張機能
- du extension
- dw の拡張機能
- メモリ、拡張機能の物理ディスプレイ (d)
- db では、dc、dd、dp、dq、du、dw Windows デバッグ
ms.date: 01/18/2017
topic_type:
- apiref
api_name:
- db, dc, dd, dp, dq, du, dw
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: ef7aeeb0f6597c7be3ae0e18c007e5dc7dd14fe8
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56558772"
---
# <a name="db-dc-dd-dp-dq-du-dw"></a>!db, !dc, !dd, !dp, !dq, !du, !dw


**! Db**、 **! dc**、 **! dd**、 **! dp**、 **! dq**、 **! du**、および **! dw**拡張機能は、ターゲット コンピューター上の指定した物理アドレスにデータを表示します。

これらの拡張機能のコマンドと混同しないで、 [ **d\* (表示メモリ)** ](d--da--db--dc--dd--dd--df--dp--dq--du--dw--dw--dyb--dyd--display-memor.md)コマンド、または、 [ **! ntsdexts.dp** ](-dp---ntsdexts-dp-.md)拡張機能コマンド。

```dbgcmd
!db [Caching] [-m] [PhysicalAddress] [L Size] 
!dc [Caching] [-m] [PhysicalAddress] [L Size] 
!dd [Caching] [-m] [PhysicalAddress] [L Size] 
!dp [Caching] [-m] [PhysicalAddress] [L Size] 
!dq [Caching] [-m] [PhysicalAddress] [L Size] 
!du [Caching] [-m] [PhysicalAddress] [L Size] 
!dw [Caching] [-m] [PhysicalAddress] [L Size] 
```

## <a name="span-idddkddbgspanspan-idddkddbgspanparameters"></a><span id="ddk__d__dbg"></span><span id="DDK__D__DBG"></span>パラメーター


<span id="_______Caching______"></span><span id="_______caching______"></span><span id="_______CACHING______"></span> *キャッシュ*   
次の値のいずれを指定できます。 *Caching*値は、角かっこで囲む必要があります。

<span id="_c_"></span><span id="_C_"></span>**\[c\]**  
キャッシュされたメモリから読み取られた場合は、この拡張機能をによりします。

<span id="_uc_"></span><span id="_UC_"></span>**\[uc\]**  
キャッシュされていないメモリから読み取られた場合は、この拡張機能をによりします。

<span id="_wc_"></span><span id="_WC_"></span>**\[wc\]**  
書き込み結合のメモリから読み取られた場合は、この拡張機能をによりします。

<span id="_______-m______"></span><span id="_______-M______"></span> **-m**   
により、一度に 1 つの単位を読み取られるメモリ。 たとえば、 **! db m** 8 ビットのチャンク単位でメモリの読み取りと **! dw m** 16 ビットのチャンク単位でメモリを読み取ります。 ハードウェアが 32 ビットの物理メモリの読み取りをサポートしていない場合がありますを使用するために必要な **-m**オプション。 このオプションでは、長さまたは表示の外観は影響しません - メモリへのアクセス方法にのみ影響します。

<span id="_______PhysicalAddress______"></span><span id="_______physicaladdress______"></span><span id="_______PHYSICALADDRESS______"></span> *PhysicalAddress*   
16 進形式で表示される最初の物理アドレスを指定します。 これが最初にこのコマンドを使用するときを省略した場合、アドレスの既定値は 0 にです。 これを以降の使用を省略すると、最後の表示が終了した位置の表示が開始されます。

<span id="_______L_______Size______"></span><span id="_______l_______size______"></span><span id="_______L_______SIZE______"></span> **L** **** *サイズ*   
表示するメモリのチャンクの数を指定します。 チャンクのサイズ、正確な拡張機能を使用します。

### <a name="span-iddllspanspan-iddllspanenvironment"></a><span id="DLL"></span><span id="dll"></span>環境

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>モード</strong></p></td>
<td align="left"><p>カーネル モード</p></td>
</tr>
</tbody>
</table>


### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>Kext.dll</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>追加情報

物理メモリに書き込むを使用して、 [ **! e\\**  * ](-eb---ed.md)拡張機能。 その他のメモリに関連するコマンドの説明とメモリの操作の概要については、[読み取りと書き込みメモリ](reading-and-writing-memory.md)を参照してください。

<a name="remarks"></a>注釈
-------

これらの拡張は各物理メモリの表示が、表示形式と既定の長さが異なります。

-   **! Db**拡張機能は、16 進数のバイト数と同等の ASCII 文字が表示されます。 既定の長さは 128 バイトです。

-   **! Dc**拡張機能は、DWORD の値と同等の ASCII 文字が表示されます。 既定の長さは 32 の Dword (128 総バイト数)。

-   **! Dd**拡張機能には、DWORD 値が表示されます。 既定の長さは 32 の Dword (128 総バイト数)。

-   **! Dp**拡張表示 ULONG\_PTR 値。 これらは、命令のサイズに応じて、32 ビットまたは 64 ビットのいずれかの単語です。 既定の長さは、128 の合計バイト数です。

-   **! Dq**拡張表示 ULONG64\_PTR 値。 これらは、32 ビット ワードです。 既定の長さは、128 の合計バイト数です。

-   **! Du**拡張機能は、UNICODE 文字を表示します。 既定の長さは 16 文字 (32 バイト)、または NULL 文字が検出されました。

-   **! Dw**拡張機能には、WORD の値が表示されます。 既定の長さは 64 Dword (128 総バイト数)。

その結果、2 つの個別の値が同じであるこれらの拡張機能を使用して*サイズ*最も可能性の高い結果を表示するメモリの総量で違いは。 などのコマンドを使用して **! db L 32** (16 進数のバイト単位) として表示されている 32 バイトの結果は、コマンド **! dd L 32** (DWORD 値) として表示されている 128 バイトになります。

キャッシュの属性のフラグが必要な例を次に示します。

```dbgcmd
kd> !dc e9000
physical memory read at e9000 failed
If you know the caching attributes used for the memory,
try specifying [c], [uc] or [wc], as in !dd [c] <params>.
WARNING: Incorrect use of these flags will cause unpredictable
processor corruption. This may immediately (or at any time in
the future until reboot) result in a system hang, incorrect data
being displayed or other strange crashes and corruption.

kd> !dc [c] e9000
#   e9000 000ea002 000ea002 000ea002 000ea002 ................
#   e9010 000ea002 000ea002 000ea002 000ea002 ................
```

 

 






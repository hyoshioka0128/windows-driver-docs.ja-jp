---
title: f、fp (メモリのフィル)
description: F と fp コマンドでは、繰り返しのパターンを持つ指定したメモリ範囲を入力します。これらのコマンドと混同しないで、~ (スレッドを凍結) F コマンド。
ms.assetid: 9ef4eb88-dc6f-4f0f-ac01-a6b0bb42b33e
keywords:
- f、fp (塗りつぶしメモリ) の Windows デバッグ
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- f, fp (Fill Memory)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 26cc71ffeb8e555fae92b5408a3adf823cb96cca
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56574120"
---
# <a name="f-fp-fill-memory"></a>f、fp (メモリのフィル)


**F**と**fp**コマンドは、繰り返しのパターンを持つ指定したメモリ範囲を入力します。

これらのコマンドと混同しないで、 [ **~ (スレッドを凍結) F** ](-f--freeze-thread-.md)コマンド。

```dbgcmd
f Range Pattern 
fp [MemoryType] PhysicalRange Pattern
```

## <a name="span-idddkcmdfillmemorydbgspanspan-idddkcmdfillmemorydbgspanparameters"></a><span id="ddk_cmd_fill_memory_dbg"></span><span id="DDK_CMD_FILL_MEMORY_DBG"></span>パラメーター


<span id="_______Range______"></span><span id="_______range______"></span><span id="_______RANGE______"></span> *範囲*   
仮想メモリを埋める範囲を指定します。 構文の詳細については、[アドレスとアドレス範囲の構文](address-and-address-range-syntax.md)を参照してください。

<span id="_______PhysicalRange______"></span><span id="_______physicalrange______"></span><span id="_______PHYSICALRANGE______"></span> *PhysicalRange*   
(カーネル モードのみ)入力の物理メモリの範囲を指定します。 構文*PhysicalRange*ですが、仮想メモリの範囲と同じシンボル名は許可されません。

<span id="_______MemoryType______"></span><span id="_______memorytype______"></span><span id="_______MEMORYTYPE______"></span> *MemoryType*   
(カーネル モードのみ)物理メモリは、次のいずれかの種類を指定します。

<span id="_c_"></span><span id="_C_"></span>**\[c\]**  
キャッシュされたメモリ。

<span id="_uc_"></span><span id="_UC_"></span>**\[uc\]**  
キャッシュされていないメモリ。

<span id="_wc_"></span><span id="_WC_"></span>**\[wc\]**  
メモリの書き込み結合します。

<span id="_______Pattern______"></span><span id="_______pattern______"></span><span id="_______PATTERN______"></span> *パターン*   
メモリの塗りつぶしに使用する 1 つまたは複数のバイト値を指定します。

### <a name="span-idenvironmentspanspan-idenvironmentspanspan-idenvironmentspanenvironment"></a><span id="Environment"></span><span id="environment"></span><span id="ENVIRONMENT"></span>環境

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>モード</strong></p></td>
<td align="left"><p></p>
<strong>f:</strong>ユーザー モードでは、カーネル モード<strong>fp:</strong>カーネル モードのみ</td>
</tr>
<tr class="even">
<td align="left"><p><strong>ターゲット</strong></p></td>
<td align="left"><p>ライブ、クラッシュ ダンプ</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>プラットフォーム</strong></p></td>
<td align="left"><p>all</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>追加情報

その他のメモリに関連するコマンドの説明とメモリの操作の概要については、[読み取りと書き込みメモリ](reading-and-writing-memory.md)を参照してください。

<a name="remarks"></a>コメント
-------

このコマンドで指定されたメモリ領域を塗りつぶす*範囲*、指定した*パターン*必要な回数だけ繰り返される。

*パターン*パラメーターの場合は、一連のバイトとして入力する必要があります。 これらは、ASCII 文字、または数値として入力できます。

数値の値は、現在の基数 (16、10、または 8) では数値として解釈されます。 既定の基数を変更するには、使用、 [ **n (設定数の基本)** ](n--set-number-base-.md)コマンド。 既定の基数を指定することによってオーバーライドできます、 **0 x**プレフィックス (16 進数)、 **0n**プレフィックス (10 進数)、 **0t**プレフィックス (8 進数)、または**0y**プレフィックス (バイナリ)。

**注**  既定の基数は C++ の式が使用されているときに動作が異なります。 詳細については、次を参照してください。、[を評価する式](evaluating-expressions.md)トピック。

 

ASCII 文字を使用している場合、各文字は単一引用符で囲む必要があります。 C スタイルのエスケープ文字 (など '\\0' または'\\n') は使用できません。

複数のバイトが指定されている場合は、スペースで区切る必要があります。

場合*パターン*バイト数より多い値の範囲、デバッガーは余分な値を無視します。

例をいくつか紹介します。 現在の基数が 16 であると仮定した場合、次のコマンドは複数回繰り返すパターン"ABC"で 0012FF5F を通じてメモリ ロケーション 0012FF40 を入力します。

```dbgcmd
0:000> f 0012ff40 L20 'A' 'B' 'C'
```

次のコマンドには、まったく同じ効果があります。

```dbgcmd
0:000> f 0012ff40 L20 41 42 43
```

次の例は、物理メモリの種類を使用する方法を示します (**c**、 **uc**、および**wc**) で、 **fp**カーネル モードでコマンド。

```dbgcmd
kd> fp [c] 0012ff40 L20 'A' 'B' 'C'
```

```dbgcmd
kd> fp [uc] 0012ff40 L20 'A' 'B' 'C'
```

```dbgcmd
kd> fp [wc] 0012ff40 L20 'A' 'B' 'C'
```

 

 






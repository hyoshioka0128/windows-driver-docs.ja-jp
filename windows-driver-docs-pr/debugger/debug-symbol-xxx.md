---
title: デバッグ\_シンボル\_XXX
description: デバッグ\_シンボル\_XXX 定数は、シンボルのフラグのビット セットを使用します。 (一部)、シンボルのグループ内のシンボルでシンボルのフラグがについて説明します。
ms.assetid: de1988f8-6a4d-43a3-856a-0543ecaaf06f
ms.date: 12/07/2017
topic_type:
- apiref
api_name:
- DEBUG_SYMBOL_EXPANDED
- DEBUG_SYMBOL_READ_ONLY
- DEBUG_SYMBOL_IS_ARRAY
- DEBUG_SYMBOL_IS_FLOAT
- DEBUG_SYMBOL_IS_ARGUMENT
- DEBUG_SYMBOL_IS_LOCAL
api_location:
- DbgEng.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.openlocfilehash: 4bb7f8916d775432b10917ce9b0028c29e49adef
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67366965"
---
# <a name="debugsymbolxxx"></a>デバッグ\_シンボル\_XXX


デバッグ\_シンボル\_*XXX*定数は、シンボルのフラグのビット セットを使用します。 (一部)、シンボルのグループ内のシンボルでシンボルのフラグがについて説明します。

シンボルの最下位ビット フラグ--ビットがデバッグで見つかった\_シンボル\_拡張\_レベル\_マスク--数値、記号、シンボルのグループ内の展開の深さを表すフォーム。 子のシンボルの深さは、常に 1 つ以上の親のシンボルの深さ。 たとえば、変数のフラグが含まれているシンボルの深さを検索する*フラグ*、次のステートメントを使用します。

```dbgcmd
depth = flags & DEBUG_SYMBOL_EXPANSION_LEVEL_MASK;
```

シンボルのフラグのビット セットの残りの部分は、次のビット フラグを含めることができます。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">定数</th>
<th align="left">説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><span id="DEBUG_SYMBOL_EXPANDED"></span><span id="debug_symbol_expanded"></span>
<strong>DEBUG_SYMBOL_EXPANDED</strong></td>
<td align="left"><p>シンボルの子は、シンボルのグループの一部です。</p></td>
</tr>
<tr class="even">
<td align="left"><span id="DEBUG_SYMBOL_READ_ONLY"></span><span id="debug_symbol_read_only"></span>
<strong>DEBUG_SYMBOL_READ_ONLY</strong></td>
<td align="left"><p>シンボルは、読み取り専用変数を表します。</p></td>
</tr>
<tr class="odd">
<td align="left"><span id="DEBUG_SYMBOL_IS_ARRAY"></span><span id="debug_symbol_is_array"></span>
<strong>DEBUG_SYMBOL_IS_ARRAY</strong></td>
<td align="left"><p>シンボルは、配列変数を表します。</p></td>
</tr>
<tr class="even">
<td align="left"><span id="DEBUG_SYMBOL_IS_FLOAT"></span><span id="debug_symbol_is_float"></span>
<strong>DEBUG_SYMBOL_IS_FLOAT</strong></td>
<td align="left"><p>シンボルは、浮動小数点変数を表します。</p></td>
</tr>
<tr class="odd">
<td align="left"><span id="DEBUG_SYMBOL_IS_ARGUMENT"></span><span id="debug_symbol_is_argument"></span>
<strong>DEBUG_SYMBOL_IS_ARGUMENT</strong></td>
<td align="left"><p>シンボルは、関数に渡される引数を表します。</p></td>
</tr>
<tr class="even">
<td align="left"><span id="DEBUG_SYMBOL_IS_LOCAL"></span><span id="debug_symbol_is_local"></span>
<strong>DEBUG_SYMBOL_IS_LOCAL</strong></td>
<td align="left"><p>シンボルは、スコープ内のローカル変数を表します。</p></td>
</tr>
</tbody>
</table>

<a name="requirements"></a>必要条件
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>Header</p></td>
<td align="left">DbgEng.h (DbgEng.h を含む)</td>
</tr>
</tbody>
</table>

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>参照してください。


[**デバッグ\_シンボル\_パラメーター**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/ns-dbgeng-_debug_symbol_parameters)

 

 







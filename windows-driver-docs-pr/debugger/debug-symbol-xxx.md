---
title: デバッグ\_シンボル\_XXX
description: シンボルフラグのビットセットには、DEBUG\_SYMBOL\_XXX 定数が使用されます。 シンボルフラグは、シンボルグループ内の記号を部分的に記述します。
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
ms.openlocfilehash: 6718007776f21cb51a89eb8f30785ec240efe051
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72837784"
---
# <a name="debug_symbol_xxx"></a>デバッグ\_シンボル\_XXX


シンボルフラグのビットセットには、DEBUG\_SYMBOL\_*XXX*定数が使用されます。 シンボルフラグは、シンボルグループ内の記号を部分的に記述します。

シンボルフラグの最下位ビット (デバッグ\_シンボル\_拡張\_レベル\_マスク) で見つかったビットは、シンボルグループ内のシンボルの拡張深度を表す数値を形成します。 子シンボルの深さは、常にその親シンボルの深さよりも1だけ大きくなります。 たとえば、変数*フラグ*に含まれるフラグを持つシンボルの深さを調べるには、次のステートメントを使用します。

```dbgcmd
depth = flags & DEBUG_SYMBOL_EXPANSION_LEVEL_MASK;
```

残りのシンボルフラグのビットセットには、次のビットフラグを含めることができます。

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
<td align="left"><p>シンボルの子は、シンボルグループに含まれています。</p></td>
</tr>
<tr class="even">
<td align="left"><span id="DEBUG_SYMBOL_READ_ONLY"></span><span id="debug_symbol_read_only"></span>
<strong>DEBUG_SYMBOL_READ_ONLY</strong></td>
<td align="left"><p>シンボルは、読み取り専用の変数を表します。</p></td>
</tr>
<tr class="odd">
<td align="left"><span id="DEBUG_SYMBOL_IS_ARRAY"></span><span id="debug_symbol_is_array"></span>
<strong>DEBUG_SYMBOL_IS_ARRAY</strong></td>
<td align="left"><p>シンボルは配列変数を表します。</p></td>
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

<a name="requirements"></a>要件
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>Header</p></td>
<td align="left">DbgEng .h (DbgEng .h を含む)</td>
</tr>
</tbody>
</table>

## <a name="span-idsee_alsospansee-also"></a><span id="see_also"></span>関連項目


[**デバッグ\_シンボル\_パラメーター**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/ns-dbgeng-_debug_symbol_parameters)

 

 







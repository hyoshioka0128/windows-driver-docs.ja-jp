---
title: DBG\_DUMP\_XXX
description: DBG\_DUMP\_XXX
ms.assetid: d34ecf95-3aea-4850-a2de-76f239e8b8a0
ms.date: 12/07/2017
keywords:
- DBG_DUMP_XXX Windows のデバッグ
topic_type:
- apiref
api_name:
- DBG_DUMP_XXX
api_location:
- wdbgexts.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.openlocfilehash: cec17542dc42a26d5514b54e6b08ff560f93d5a7
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72837804"
---
# <a name="dbg_dump_xxx"></a>DBG\_DUMP\_XXX


## <span id="ddk_dbg_dump_xxx_dbx"></span><span id="DDK_DBG_DUMP_XXX_DBX"></span>


DBG\_DUMP\_PARAM 構造体の**Options**メンバーは、DBG\_Dump\_*XXX*ビットフラグを使用して、 [**IG\_ダンプ\_シンボル\_情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdbgexts/ns-wdbgexts-_sym_dump_param)[**Ioctl**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdbgexts/nc-wdbgexts-pwindbg_ioctl_routine)の動作を制御します。運用.

次のフラグを使用できます。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">Flag</th>
<th align="left">効果</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>DBG_DUMP_NO_INDENT</p></td>
<td align="left"><p>出力では、メンバーはインデントされません。</p></td>
</tr>
<tr class="even">
<td align="left"><p>DBG_DUMP_NO_OFFSET</p></td>
<td align="left"><p>オフセットは印刷されません。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>DBG_DUMP_VERBOSE</p></td>
<td align="left"><p>詳細出力。</p></td>
</tr>
<tr class="even">
<td align="left"><p>DBG_DUMP_CALL_FOR_EACH</p></td>
<td align="left"><p>コールバック関数は、メンバーごとに呼び出されます。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>DBG_DUMP_LIST</p></td>
<td align="left"><p>シンボルはリンクリスト内のエントリであり、IG_DUMP_SYMBOL_INFO <strong>Ioctl</strong>操作はこのリストを反復処理します。 リスト内の次の項目を指すメンバーの説明は、SYM_DUMP_PARAM 構造体の<strong>Linklist</strong>メンバーによって指定されます。</p></td>
</tr>
<tr class="even">
<td align="left"><p>DBG_DUMP_NO_PRINT</p></td>
<td align="left"><p>何も出力されません (コールバック関数だけが呼び出され、データのコピーが実行されます)。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>DBG_DUMP_GET_SIZE_ONLY</p></td>
<td align="left"><p><strong>Ioctl</strong>操作は、シンボルのサイズのみを返します。メンバー情報を出力したり、コールバック関数を呼び出したりすることはありません。</p></td>
</tr>
<tr class="even">
<td align="left"><p>DBG_DUMP_COMPACT_OUT</p></td>
<td align="left"><p>各メンバーの後に改行は出力されません。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>DBG_DUMP_ARRAY</p></td>
<td align="left"><p>記号は配列です。 配列内の要素の数は、SYM_DUMP_PARAM 構造体のメンバー <strong>Listlink&gt;サイズ</strong>によって指定されます。</p></td>
</tr>
<tr class="even">
<td align="left"><p>DBG_DUMP_ADDRESS_OF_FIELD</p></td>
<td align="left"><p><strong>Addr</strong>の値は実際には、SYM_DUMP_PARAM 構造体のメンバー <strong>listlink-&gt;fName</strong>で、シンボルの先頭ではありません。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>DBG_DUMP_ADDRESS_AT_END</p></td>
<td align="left"><p><strong>Addr</strong>の値は、実際にはシンボルの先頭ではなく、シンボルの末尾のアドレスです。</p></td>
</tr>
<tr class="even">
<td align="left"><p>DBG_DUMP_COPY_TYPE_DATA</p></td>
<td align="left"><p>シンボルの値は、メンバー <strong>Pbuffer</strong>にコピーされます。 これは、プリミティブ型 (たとえば、ULONG や PVOID) に対してのみ使用できます。構造体では使用できません。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>DBG_DUMP_READ_PHYSICAL</p></td>
<td align="left"><p>シンボルの値は、ターゲットの物理メモリから直接読み込まれます。</p></td>
</tr>
<tr class="even">
<td align="left"><p>DBG_DUMP_FUNCTION_FORMAT</p></td>
<td align="left"><p>関数の型を持つシンボルを書式設定すると、関数の形式が使用されます (たとえば、<code>function(arg1, arg2, ...)</code></p></td>
</tr>
<tr class="odd">
<td align="left"><p>DBG_DUMP_BLOCK_RECURSE</p></td>
<td align="left"><p>入れ子構造体を使用して再帰的に実行します。ただし、ポインターには従いません。</p></td>
</tr>
</tbody>
</table>

 

さらに、マクロ DBG\_DUMP\_繰り返し\_レベル (*レベル*) の結果をビットセットに追加して、再帰する構造の深さを指定できます。 *レベル*0 から15までの数値を指定できます。

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
<td align="left">Wdbgexts (wdbgexts .h、Wdbgexts .h、または Dbgeng .h を含む)</td>
</tr>
</tbody>
</table>

## <a name="span-idsee_alsospansee-also"></a><span id="see_also"></span>関連項目


[**IG\_ダンプ\_シンボル\_情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdbgexts/ns-wdbgexts-_sym_dump_param)

[**Ioctl**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdbgexts/nc-wdbgexts-pwindbg_ioctl_routine)

 

 







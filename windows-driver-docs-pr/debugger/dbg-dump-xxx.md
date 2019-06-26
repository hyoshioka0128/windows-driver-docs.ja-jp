---
title: DBG\_ダンプ\_XXX
description: DBG\_ダンプ\_XXX
ms.assetid: d34ecf95-3aea-4850-a2de-76f239e8b8a0
ms.date: 12/07/2017
keywords:
- デバッグ DBG_DUMP_XXX Windows
topic_type:
- apiref
api_name:
- DBG_DUMP_XXX
api_location:
- wdbgexts.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.openlocfilehash: 5bbcf11ad55aa35858ef903d7aea2c77693acb86
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67361448"
---
# <a name="dbgdumpxxx"></a>DBG\_ダンプ\_XXX


## <span id="ddk_dbg_dump_xxx_dbx"></span><span id="DDK_DBG_DUMP_XXX_DBX"></span>


DBG\_ダンプ\_*XXX*ビット フラグを使って、**オプション**、SYM のメンバー\_ダンプ\_の動作を制御するパラメーターの構造体[**IG\_ダンプ\_シンボル\_情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdbgexts/ns-wdbgexts-_sym_dump_param)[**Ioctl** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdbgexts/nc-wdbgexts-pwindbg_ioctl_routine)操作。

次のフラグは、存在することができます。

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
<td align="left"><p>メンバーは、出力にインデントされません。</p></td>
</tr>
<tr class="even">
<td align="left"><p>DBG_DUMP_NO_OFFSET</p></td>
<td align="left"><p>オフセットは印刷されません。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>DBG_DUMP_VERBOSE</p></td>
<td align="left"><p>詳細な出力。</p></td>
</tr>
<tr class="even">
<td align="left"><p>DBG_DUMP_CALL_FOR_EACH</p></td>
<td align="left"><p>コールバック関数は、各メンバーに対して呼び出されます。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>DBG_DUMP_LIST</p></td>
<td align="left"><p>シンボルは、リンクされたリストで、IG_DUMP_SYMBOL_INFO エントリ<strong>Ioctl</strong>操作はこのリストに対して反復処理します。 一覧の次の項目を指すメンバーの説明が指定された、 <strong>linkList</strong> SYM_DUMP_PARAM 構造体のメンバー。</p></td>
</tr>
<tr class="even">
<td align="left"><p>DBG_DUMP_NO_PRINT</p></td>
<td align="left"><p>(コールバック関数を呼び出すし、データのコピーが実行される) だけは、何も出力されません。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>DBG_DUMP_GET_SIZE_ONLY</p></td>
<td align="left"><p><strong>Ioctl</strong>操作は、のみのシンボルのサイズを返します。 メンバーの情報または呼び出しのコールバック関数は印刷されません。</p></td>
</tr>
<tr class="even">
<td align="left"><p>DBG_DUMP_COMPACT_OUT</p></td>
<td align="left"><p>各メンバーの後に改行文字は印刷されません。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>DBG_DUMP_ARRAY</p></td>
<td align="left"><p>シンボルは、配列です。 配列内の要素の数が、メンバーで指定された<strong>listLink -&gt;サイズ</strong>SYM_DUMP_PARAM 構造体の。</p></td>
</tr>
<tr class="even">
<td align="left"><p>DBG_DUMP_ADDRESS_OF_FIELD</p></td>
<td align="left"><p>値<strong>addr</strong>メンバーのアドレスでは実際には、 <strong>listLink -&gt;fName</strong> SYM_DUMP_PARAM 構造とシンボルの先頭ではありません。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>DBG_DUMP_ADDRESS_AT_END</p></td>
<td align="left"><p>値<strong>addr</strong>は実際には、シンボルの終了とシンボルの先頭ではないアドレスです。</p></td>
</tr>
<tr class="even">
<td align="left"><p>DBG_DUMP_COPY_TYPE_DATA</p></td>
<td align="left"><p>シンボルの値がメンバーにコピーされます<strong>pBuffer</strong>します。 これはのみ使用できますのプリミティブ型は--の ULONG または PVOID--では使用できません構造体。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>DBG_DUMP_READ_PHYSICAL</p></td>
<td align="left"><p>シンボルの値については、ターゲットの物理メモリから直接読み取ります。</p></td>
</tr>
<tr class="even">
<td align="left"><p>DBG_DUMP_FUNCTION_FORMAT</p></td>
<td align="left"><p>関数型を持つシンボルを書式設定時に関数の形式が適用されます、たとえば、 <code>function(arg1, arg2, ...)</code></p></td>
</tr>
<tr class="odd">
<td align="left"><p>DBG_DUMP_BLOCK_RECURSE</p></td>
<td align="left"><p>入れ子になった構造で再帰処理します。ポインターに従っていません。</p></td>
</tr>
</tbody>
</table>

 

また、DBG マクロの結果\_ダンプ\_RECUR\_レベル (*レベル*) 構造体を再帰の深さを指定するビット セットに追加できます。 *レベル*0 ~ 15 の数値を指定できます。

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
<td align="left">Wdbgexts.h (Wdbgexts.h、Wdbgexts.h、Dbgeng.h など)</td>
</tr>
</tbody>
</table>

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>参照してください。


[**IG\_ダンプ\_シンボル\_情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdbgexts/ns-wdbgexts-_sym_dump_param)

[**Ioctl**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdbgexts/nc-wdbgexts-pwindbg_ioctl_routine)

 

 







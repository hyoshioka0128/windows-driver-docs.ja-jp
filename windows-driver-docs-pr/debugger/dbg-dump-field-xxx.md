---
title: DBG\_ダンプ\_フィールド\_XXX
description: DBG\_ダンプ\_フィールド\_XXX
ms.assetid: c168c1b7-c4ef-4a70-9060-611b86120635
ms.date: 12/07/2017
keywords:
- デバッグ DBG_DUMP_FIELD_XXX Windows
topic_type:
- apiref
api_name:
- DBG_DUMP_FIELD_XXX
api_location:
- wdbgexts.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.openlocfilehash: 801f794c62a429485a550f72dd53ec9c9f86caa1
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63376116"
---
# <a name="dbgdumpfieldxxx"></a>DBG\_ダンプ\_フィールド\_XXX


## <span id="ddk_dbg_dump_xxx_dbx"></span><span id="DDK_DBG_DUMP_XXX_DBX"></span>


DBG\_ダンプ\_フィールド\_*XXX*ビット フラグを使って、**方法は限られて**のメンバー、 [**フィールド\_情報** ](https://msdn.microsoft.com/library/windows/hardware/ff545316)の動作を制御する構造体、 [ **IG\_ダンプ\_シンボル\_情報**](https://msdn.microsoft.com/library/windows/hardware/ff550906) [ **Ioctl** ](https://msdn.microsoft.com/library/windows/hardware/ff551084)操作。

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
<td align="left"><p>DBG_DUMP_FIELD_CALL_BEFORE_PRINT</p></td>
<td align="left"><p>コールバック関数は、メンバーを印刷する前に呼び出されます。</p></td>
</tr>
<tr class="even">
<td align="left"><p>DBG_DUMP_FIELD_NO_CALLBACK_REQ</p></td>
<td align="left"><p>コールバック関数は呼び出されません。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>DBG_DUMP_FIELD_RECUR_ON_THIS</p></td>
<td align="left"><p>メンバーの submembers が処理されます。</p></td>
</tr>
<tr class="even">
<td align="left"><p>DBG_DUMP_FIELD_FULL_NAME</p></td>
<td align="left"><p><strong>fName</strong>メンバーが処理するため、一致するプレフィックスがあるだけではなく、完全に一致する必要があります。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>DBG_DUMP_FIELD_ARRAY</p></td>
<td align="left"><p>配列メンバーの配列要素を出力します。</p></td>
</tr>
<tr class="even">
<td align="left"><p>DBG_DUMP_FIELD_COPY_FIELD_DATA</p></td>
<td align="left"><p>メンバーの値にコピーされます<strong>pBuffer</strong>します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>DBG_DUMP_FIELD_RETURN_ADDRESS</p></td>
<td align="left"><p>コールバック中または<strong>Ioctl</strong> 、FIELD_INFO を返します<strong>。アドレス</strong>メンバーには、シンボルのメンバーのアドレスが含まれています。</p>
<p>場合は、型、FIELD_INFO のアドレスが指定されていません。<strong>アドレス</strong>型の先頭からメンバーの合計のオフセットが含まれています。</p></td>
</tr>
<tr class="even">
<td align="left"><p>DBG_DUMP_FIELD_SIZE_IN_BITS</p></td>
<td align="left"><p>ビット フィールドでは、バイトではなくビット単位のオフセットとサイズを返します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>DBG_DUMP_FIELD_NO_PRINT</p></td>
<td align="left"><p>(コールバック関数が呼び出されたおよびデータのコピーが実行される) のみ、このメンバーは印刷されません。</p></td>
</tr>
<tr class="even">
<td align="left"><p>DBG_DUMP_FIELD_DEFAULT_STRING DBG_DUMP_FIELD_WCHAR_STRING DBG_DUMP_FIELD_MULTI_STRING DBG_DUMP_FIELD_GUID_STRING</p></td>
<td align="left"><p>メンバーが、ポインターの場合は、文字列、ANSI 文字列、WCHAR 文字列、複数行文字列、または GUID として出力されます。</p></td>
</tr>
</tbody>
</table>

 

また、DBG マクロの結果\_ダンプ\_RECUR\_レベル (*レベル*) 構造体を再帰の深さを指定するビット セットに追加できます。 *レベル*0 ~ 15 の数値を指定できます。

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
<td align="left">Wdbgexts.h (Wdbgexts.h、Wdbgexts.h、Dbgeng.h など)</td>
</tr>
</tbody>
</table>

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>参照してください。


[**IG\_ダンプ\_シンボル\_情報**](https://msdn.microsoft.com/library/windows/hardware/ff550906)

[**Ioctl**](https://msdn.microsoft.com/library/windows/hardware/ff551084)

[**フィールド\_情報**](https://msdn.microsoft.com/library/windows/hardware/ff545316)

 

 







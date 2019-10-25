---
title: DBG\_\_フィールド\_XXX にダンプします
description: DBG\_\_フィールド\_XXX にダンプします
ms.assetid: c168c1b7-c4ef-4a70-9060-611b86120635
ms.date: 12/07/2017
keywords:
- DBG_DUMP_FIELD_XXX Windows のデバッグ
topic_type:
- apiref
api_name:
- DBG_DUMP_FIELD_XXX
api_location:
- wdbgexts.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.openlocfilehash: 8493e16e28a046291f78cac60a7671eaeb9017f3
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72837799"
---
# <a name="dbg_dump_field_xxx"></a>DBG\_\_フィールド\_XXX にダンプします


## <span id="ddk_dbg_dump_xxx_dbx"></span><span id="DDK_DBG_DUMP_XXX_DBX"></span>


DBG\_DUMP\_FIELD\_*XXX*ビットフラグは、[**フィールド\_info**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdbgexts/ns-wdbgexts-_field_info)構造体の**foptions**メンバーによって使用されます。これにより、 [**IG\_DUMP\_SYMBOL\_INFO**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdbgexts/ns-wdbgexts-_sym_dump_param) [**の動作が制御されます。Ioctl**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdbgexts/nc-wdbgexts-pwindbg_ioctl_routine)操作。

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
<td align="left"><p>DBG_DUMP_FIELD_CALL_BEFORE_PRINT</p></td>
<td align="left"><p>コールバック関数は、メンバーを出力する前に呼び出されます。</p></td>
</tr>
<tr class="even">
<td align="left"><p>DBG_DUMP_FIELD_NO_CALLBACK_REQ</p></td>
<td align="left"><p>コールバック関数は呼び出されません。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>DBG_DUMP_FIELD_RECUR_ON_THIS</p></td>
<td align="left"><p>メンバーのサブメンバーが処理されます。</p></td>
</tr>
<tr class="even">
<td align="left"><p>DBG_DUMP_FIELD_FULL_NAME</p></td>
<td align="left"><p><strong>fName</strong>は、一致するプレフィックスを持つだけでなく、メンバーを処理するために完全に一致する必要があります。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>DBG_DUMP_FIELD_ARRAY</p></td>
<td align="left"><p>配列メンバーの配列要素を出力します。</p></td>
</tr>
<tr class="even">
<td align="left"><p>DBG_DUMP_FIELD_COPY_FIELD_DATA</p></td>
<td align="left"><p>メンバーの値が<strong>Pbuffer</strong>にコピーされます。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>DBG_DUMP_FIELD_RETURN_ADDRESS</p></td>
<td align="left"><p>コールバック時または<strong>Ioctl</strong>が戻るときに、FIELD_INFO が返されます。<strong>アドレス</strong>メンバーには、シンボルのメンバーのアドレスが含まれます。</p>
<p>型にアドレスが指定されていない場合は、FIELD_INFO になります。<strong>アドレス</strong>には、型の先頭からのメンバーのオフセットの合計が含まれます。</p></td>
</tr>
<tr class="even">
<td align="left"><p>DBG_DUMP_FIELD_SIZE_IN_BITS</p></td>
<td align="left"><p>ビットフィールドの場合は、オフセットとサイズをバイト単位ではなくビット単位で返します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>DBG_DUMP_FIELD_NO_PRINT</p></td>
<td align="left"><p>このメンバーを出力しません (コールバック関数だけが呼び出され、データのコピーが実行されます)。</p></td>
</tr>
<tr class="even">
<td align="left"><p>DBG_DUMP_FIELD_DEFAULT_STRING DBG_DUMP_FIELD_WCHAR_STRING DBG_DUMP_FIELD_MULTI_STRING DBG_DUMP_FIELD_GUID_STRING</p></td>
<td align="left"><p>メンバーがポインターの場合は、文字列、ANSI 文字列、WCHAR 文字列、複数の文字列、または GUID として出力されます。</p></td>
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

[**フィールド\_情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdbgexts/ns-wdbgexts-_field_info)

 

 







---
title: デバッグ\_要求\_EXT\_型指定された\_データ\_ANSI
description: デバッグ\_要求\_EXT\_型指定された\_データ\_ANSI
ms.assetid: ac883bc8-3956-4bc3-a11e-b6e036305329
keywords:
- デバッグ DEBUG_REQUEST_EXT_TYPED_DATA_ANSI Windows
topic_type:
- apiref
api_name:
- DEBUG_REQUEST_EXT_TYPED_DATA_ANSI
api_type:
- NA
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5eb1fa0a3759f9c822b33f0af56def5bb288a716
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67361438"
---
# <a name="debugrequestexttypeddataansi"></a>デバッグ\_要求\_EXT\_型指定された\_データ\_ANSI


デバッグ\_要求\_EXT\_型指定された\_データ\_ANSI [**要求**](request.md)操作は、別のさまざまなを実行します。型指定されたデータの解釈を支援するサブ操作。

**Parameters**

<span id="InBuffer"></span><span id="inbuffer"></span><span id="INBUFFER"></span>*InBuffer*  
指定します、 [ **EXT\_型指定された\_データ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdbgexts/ns-wdbgexts-_ext_typed_data)を実行するサブ操作を決定する構造体。 この EXT\_型指定された\_データ構造には (省略可能) その他のデータとそのサブ操作の入力パラメーターが含まれています。 追加のデータが含まれている*InBuffer* 、EXT 後\_型指定された\_データ構造体。 サイズ*InBuffer* 、EXT を格納しているバッファーの合計サイズは、\_型指定された\_データ構造とデータを追加します。 参照してください**EXT\_型指定された\_データ**この構造体と、追加のデータを含める方法の詳細について。

次のサブ操作がサポートされています。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">サブ操作</th>
<th align="left">説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><a href="ext-tdop-copy.md" data-raw-source="[&lt;strong&gt;EXT_TDOP_COPY&lt;/strong&gt;](ext-tdop-copy.md)"><strong>EXT_TDOP_COPY</strong></a></p></td>
<td align="left"><p>型指定されたデータの説明のコピーを作成します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="ext-tdop-release.md" data-raw-source="[&lt;strong&gt;EXT_TDOP_RELEASE&lt;/strong&gt;](ext-tdop-release.md)"><strong>EXT_TDOP_RELEASE</strong></a></p></td>
<td align="left"><p>型指定されたデータの説明を解放します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="ext-tdop-set-from-expr.md" data-raw-source="[&lt;strong&gt;EXT_TDOP_SET_FROM_EXPR&lt;/strong&gt;](ext-tdop-set-from-expr.md)"><strong>EXT_TDOP_SET_FROM_EXPR</strong></a></p></td>
<td align="left"><p>式の値を返します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="ext-tdop-set-from-u64-expr.md" data-raw-source="[&lt;strong&gt;EXT_TDOP_SET_FROM_U64_EXPR&lt;/strong&gt;](ext-tdop-set-from-u64-expr.md)"><strong>EXT_TDOP_SET_FROM_U64_EXPR</strong></a></p></td>
<td align="left"><p>式の値を返します。 省略可能なアドレスは、式のパラメーターとして指定できます。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="ext-tdop-get-field.md" data-raw-source="[&lt;strong&gt;EXT_TDOP_GET_FIELD&lt;/strong&gt;](ext-tdop-get-field.md)"><strong>EXT_TDOP_GET_FIELD</strong></a></p></td>
<td align="left"><p>構造体のメンバーを返します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="ext-tdop-evaluate.md" data-raw-source="[&lt;strong&gt;EXT_TDOP_EVALUATE&lt;/strong&gt;](ext-tdop-evaluate.md)"><strong>EXT_TDOP_EVALUATE</strong></a></p></td>
<td align="left"><p>式の値を返します。 オプションの値は、式のパラメーターとして指定できます。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="ext-tdop-get-type-name.md" data-raw-source="[&lt;strong&gt;EXT_TDOP_GET_TYPE_NAME&lt;/strong&gt;](ext-tdop-get-type-name.md)"><strong>EXT_TDOP_GET_TYPE_NAME</strong></a></p></td>
<td align="left"><p>型指定されたデータの種類の名前を返します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="ext-tdop-output-type-name.md" data-raw-source="[&lt;strong&gt;EXT_TDOP_OUTPUT_TYPE_NAME&lt;/strong&gt;](ext-tdop-output-type-name.md)"><strong>EXT_TDOP_OUTPUT_TYPE_NAME</strong></a></p></td>
<td align="left"><p>型指定されたデータの種類の名前を出力します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="ext-tdop-output-simple-value.md" data-raw-source="[&lt;strong&gt;EXT_TDOP_OUTPUT_SIMPLE_VALUE&lt;/strong&gt;](ext-tdop-output-simple-value.md)"><strong>EXT_TDOP_OUTPUT_SIMPLE_VALUE</strong></a></p></td>
<td align="left"><p>型指定されたデータの値を出力します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="ext-tdop-output-full-value.md" data-raw-source="[&lt;strong&gt;EXT_TDOP_OUTPUT_FULL_VALUE&lt;/strong&gt;](ext-tdop-output-full-value.md)"><strong>EXT_TDOP_OUTPUT_FULL_VALUE</strong></a></p></td>
<td align="left"><p>型と型指定されたデータの値を出力します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="ext-tdop-has-field.md" data-raw-source="[&lt;strong&gt;EXT_TDOP_HAS_FIELD&lt;/strong&gt;](ext-tdop-has-field.md)"><strong>EXT_TDOP_HAS_FIELD</strong></a></p></td>
<td align="left"><p>指定したメンバーが、構造に含まれるかどうかを決定します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="ext-tdop-get-field-offset.md" data-raw-source="[&lt;strong&gt;EXT_TDOP_GET_FIELD_OFFSET&lt;/strong&gt;](ext-tdop-get-field-offset.md)"><strong>EXT_TDOP_GET_FIELD_OFFSET</strong></a></p></td>
<td align="left"><p>構造体のメンバーのオフセットを返します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="ext-tdop-get-array-element.md" data-raw-source="[&lt;strong&gt;EXT_TDOP_GET_ARRAY_ELEMENT&lt;/strong&gt;](ext-tdop-get-array-element.md)"><strong>EXT_TDOP_GET_ARRAY_ELEMENT</strong></a></p></td>
<td align="left"><p>配列から要素を返します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="ext-tdop-get-dereference.md" data-raw-source="[&lt;strong&gt;EXT_TDOP_GET_DEREFERENCE&lt;/strong&gt;](ext-tdop-get-dereference.md)"><strong>EXT_TDOP_GET_DEREFERENCE</strong></a></p></td>
<td align="left"><p>指す値を返す、ポインターを逆参照します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="ext-tdop-get-type-size.md" data-raw-source="[&lt;strong&gt;EXT_TDOP_GET_TYPE_SIZE&lt;/strong&gt;](ext-tdop-get-type-size.md)"><strong>EXT_TDOP_GET_TYPE_SIZE</strong></a></p></td>
<td align="left"><p>指定した型指定されたデータのサイズを返します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="ext-tdop-output-type-definition.md" data-raw-source="[&lt;strong&gt;EXT_TDOP_OUTPUT_TYPE_DEFINITION&lt;/strong&gt;](ext-tdop-output-type-definition.md)"><strong>EXT_TDOP_OUTPUT_TYPE_DEFINITION</strong></a></p></td>
<td align="left"><p>指定された型指定されたデータの型の定義を出力します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="ext-tdop-get-pointer-to.md" data-raw-source="[&lt;strong&gt;EXT_TDOP_GET_POINTER_TO&lt;/strong&gt;](ext-tdop-get-pointer-to.md)"><strong>EXT_TDOP_GET_POINTER_TO</strong></a></p></td>
<td align="left"><p>指定された型指定されたデータへのポインターを表す新しい型指定されたデータの説明を返します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="ext-tdop-set-from-type-id-and-u64.md" data-raw-source="[&lt;strong&gt;EXT_TDOP_SET_FROM_TYPE_ID_AND_U64&lt;/strong&gt;](ext-tdop-set-from-type-id-and-u64.md)"><strong>EXT_TDOP_SET_FROM_TYPE_ID_AND_U64</strong></a></p></td>
<td align="left"><p>型とメモリの場所から型指定されたデータの説明を作成します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="ext-tdop-set-ptr-from-type-id-and-u64.md" data-raw-source="[&lt;strong&gt;EXT_TDOP_SET_PTR_FROM_TYPE_ID_AND_U64&lt;/strong&gt;](ext-tdop-set-ptr-from-type-id-and-u64.md)"><strong>EXT_TDOP_SET_PTR_FROM_TYPE_ID_AND_U64</strong></a></p></td>
<td align="left"><p>指定された型の指定したメモリ位置へのポインターを表す型指定されたデータの説明を作成します。</p></td>
</tr>
</tbody>
</table>

 

<span id="OutBuffer"></span><span id="outbuffer"></span><span id="OUTBUFFER"></span>*OutBuffer*  
受信、 [ **EXT\_型指定された\_データ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdbgexts/ns-wdbgexts-_ext_typed_data)出力パラメーターと、サブ操作の他のデータを含む構造体。 同様*InBuffer*、サイズの*OutBuffer* 、EXT を格納しているバッファーの合計サイズは、\_型指定された\_データ構造とその他のデータ。

デバッグ\_要求\_EXT\_型指定された\_データ\_ANSI 操作が最初にコピーする*InBuffer*に*OutBuffer*し内容を変更*OutBuffer*か所で。 つまり、 *OutBuffer* 、EXT の入力パラメーターが設定されます\_型指定された\_データとその他のデータで提供されていた*InBuffer*します。 またのサイズ*OutBuffer*のサイズ以上の容量である必要があります*InBuffer*します。

### <a name="span-idreturnvaluespanspan-idreturnvaluespanspan-idreturnvaluespanreturn-value"></a><span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>戻り値

<span id="S_OK"></span><span id="s_ok"></span>S\_OK  
操作が正常に完了しました。

このメソッドはエラー値を返すこともできます。 参照してください[**戻り値**](https://docs.microsoft.com/windows-hardware/drivers/debugger/hresult-values)の詳細。

この操作によって返される値にも格納されて、**状態**のメンバー *OutBuffer*します。

<a name="remarks"></a>注釈
-------

デバッグによって実行されるサブ操作\_要求\_EXT\_型指定された\_データ\_ANSI [**要求**](request.md)操作が決定されますによって、**操作**のメンバー、 [ **EXT\_型指定された\_データ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdbgexts/ns-wdbgexts-_ext_typed_data)構造体は、値を受け取り、 [**EXT\_TDOP** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdbgexts/ne-wdbgexts-_ext_tdop)列挙体。

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>参照してください。


[**EXT\_型指定された\_データ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdbgexts/ns-wdbgexts-_ext_typed_data)

[**EXT\_TDOP**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdbgexts/ne-wdbgexts-_ext_tdop)

[**要求**](request.md)

 

 







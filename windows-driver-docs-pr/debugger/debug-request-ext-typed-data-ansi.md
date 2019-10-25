---
title: '\_要求\_EXT\_型指定された\_データ\_ANSI'
description: '\_要求\_EXT\_型指定された\_データ\_ANSI'
ms.assetid: ac883bc8-3956-4bc3-a11e-b6e036305329
keywords:
- DEBUG_REQUEST_EXT_TYPED_DATA_ANSI Windows のデバッグ
topic_type:
- apiref
api_name:
- DEBUG_REQUEST_EXT_TYPED_DATA_ANSI
api_type:
- NA
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 676cb449a0804ef2e4395750923e711cd7e7346c
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72837797"
---
# <a name="debug_request_ext_typed_data_ansi"></a>\_要求\_EXT\_型指定された\_データ\_ANSI


デバッグ\_要求\_EXT\_型指定された\_データ\_ANSI[**要求**](request.md)操作は、型指定されたデータの解釈を補助するさまざまなサブ操作を実行します。

**Parameters**

<span id="InBuffer"></span><span id="inbuffer"></span><span id="INBUFFER"></span>*InBuffer*  
実行するサブ操作を決定する、型指定された[ **\_\_データ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdbgexts/ns-wdbgexts-_ext_typed_data)構造体を指定します。 この EXT\_型指定された\_データ構造体には、そのサブ操作の入力パラメーターと、任意の (省略可能な) 追加データが含まれています。 追加のデータは、EXT\_型指定\_データ構造体の後に*Inbuffer*に含まれます。 *Inbuffer*のサイズは、データ構造\_型指定された EXT\_、および追加データを含むバッファーの合計サイズです。 この構造の詳細と追加データを含める方法については、「 **EXT\_型指定**された\_データ」を参照してください。

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
<td align="left"><p>式の値を返します。 オプションのアドレスは、式のパラメーターとして指定できます。</p></td>
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
<td align="left"><p>型指定されたデータの型名を返します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="ext-tdop-output-type-name.md" data-raw-source="[&lt;strong&gt;EXT_TDOP_OUTPUT_TYPE_NAME&lt;/strong&gt;](ext-tdop-output-type-name.md)"><strong>EXT_TDOP_OUTPUT_TYPE_NAME</strong></a></p></td>
<td align="left"><p>型指定されたデータの型名を出力します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="ext-tdop-output-simple-value.md" data-raw-source="[&lt;strong&gt;EXT_TDOP_OUTPUT_SIMPLE_VALUE&lt;/strong&gt;](ext-tdop-output-simple-value.md)"><strong>EXT_TDOP_OUTPUT_SIMPLE_VALUE</strong></a></p></td>
<td align="left"><p>型指定されたデータの値を出力します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="ext-tdop-output-full-value.md" data-raw-source="[&lt;strong&gt;EXT_TDOP_OUTPUT_FULL_VALUE&lt;/strong&gt;](ext-tdop-output-full-value.md)"><strong>EXT_TDOP_OUTPUT_FULL_VALUE</strong></a></p></td>
<td align="left"><p>型指定されたデータの型と値を出力します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="ext-tdop-has-field.md" data-raw-source="[&lt;strong&gt;EXT_TDOP_HAS_FIELD&lt;/strong&gt;](ext-tdop-has-field.md)"><strong>EXT_TDOP_HAS_FIELD</strong></a></p></td>
<td align="left"><p>指定したメンバーが構造体に格納されているかどうかを判断します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="ext-tdop-get-field-offset.md" data-raw-source="[&lt;strong&gt;EXT_TDOP_GET_FIELD_OFFSET&lt;/strong&gt;](ext-tdop-get-field-offset.md)"><strong>EXT_TDOP_GET_FIELD_OFFSET</strong></a></p></td>
<td align="left"><p>構造体内のメンバーのオフセットを返します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="ext-tdop-get-array-element.md" data-raw-source="[&lt;strong&gt;EXT_TDOP_GET_ARRAY_ELEMENT&lt;/strong&gt;](ext-tdop-get-array-element.md)"><strong>EXT_TDOP_GET_ARRAY_ELEMENT</strong></a></p></td>
<td align="left"><p>配列から要素を返します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="ext-tdop-get-dereference.md" data-raw-source="[&lt;strong&gt;EXT_TDOP_GET_DEREFERENCE&lt;/strong&gt;](ext-tdop-get-dereference.md)"><strong>EXT_TDOP_GET_DEREFERENCE</strong></a></p></td>
<td align="left"><p>ポインターを逆参照し、ポインターが指す値を返します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="ext-tdop-get-type-size.md" data-raw-source="[&lt;strong&gt;EXT_TDOP_GET_TYPE_SIZE&lt;/strong&gt;](ext-tdop-get-type-size.md)"><strong>EXT_TDOP_GET_TYPE_SIZE</strong></a></p></td>
<td align="left"><p>指定した型指定されたデータのサイズを返します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="ext-tdop-output-type-definition.md" data-raw-source="[&lt;strong&gt;EXT_TDOP_OUTPUT_TYPE_DEFINITION&lt;/strong&gt;](ext-tdop-output-type-definition.md)"><strong>EXT_TDOP_OUTPUT_TYPE_DEFINITION</strong></a></p></td>
<td align="left"><p>指定した型指定されたデータの型の定義を出力します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="ext-tdop-get-pointer-to.md" data-raw-source="[&lt;strong&gt;EXT_TDOP_GET_POINTER_TO&lt;/strong&gt;](ext-tdop-get-pointer-to.md)"><strong>EXT_TDOP_GET_POINTER_TO</strong></a></p></td>
<td align="left"><p>指定した型指定されたデータへのポインターを表す、型指定された新しいデータの説明を返します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="ext-tdop-set-from-type-id-and-u64.md" data-raw-source="[&lt;strong&gt;EXT_TDOP_SET_FROM_TYPE_ID_AND_U64&lt;/strong&gt;](ext-tdop-set-from-type-id-and-u64.md)"><strong>EXT_TDOP_SET_FROM_TYPE_ID_AND_U64</strong></a></p></td>
<td align="left"><p>型とメモリの場所から型指定されたデータの説明を作成します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="ext-tdop-set-ptr-from-type-id-and-u64.md" data-raw-source="[&lt;strong&gt;EXT_TDOP_SET_PTR_FROM_TYPE_ID_AND_U64&lt;/strong&gt;](ext-tdop-set-ptr-from-type-id-and-u64.md)"><strong>EXT_TDOP_SET_PTR_FROM_TYPE_ID_AND_U64</strong></a></p></td>
<td align="left"><p>指定した型を使用して、指定したメモリ位置へのポインターを表す型指定されたデータの説明を作成します。</p></td>
</tr>
</tbody>
</table>

 

<span id="OutBuffer"></span><span id="outbuffer"></span><span id="OUTBUFFER"></span>*OutBuffer*  
出力パラメーターとサブ操作の追加データを含む、型指定された[**EXT\_\_データ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdbgexts/ns-wdbgexts-_ext_typed_data)構造体を受け取ります。 *Inbuffer*の場合と同様に、 *outbuffer*のサイズは、データ構造\_型指定された EXT\_、および追加データを含むバッファーの合計サイズです。

デバッグ\_要求\_EXT\_型指定された\_データ\_ANSI 操作では、最初に*inbuffer*を*outbuffer*にコピーしてから、 *outbuffer*の内容を変更します。 これは、入力された EXT\_\_型の入力パラメーターと、 *inbuffer*で提供されたその他のデータの入力パラメーターを使用して、 *outbuffer*に値が設定されることを意味します。 また、 *Outbuffer*のサイズは、少なくとも*inbuffer*のサイズと同じ大きさである必要があります。

### <a name="span-idreturn_valuespanspan-idreturn_valuespanspan-idreturn_valuespanreturn-value"></a><span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>戻り値

<span id="S_OK"></span><span id="s_ok"></span>\_OK  
操作は成功しました。

このメソッドは、エラー値を返すこともできます。 詳細については、「[**戻り値**](https://docs.microsoft.com/windows-hardware/drivers/debugger/hresult-values)」を参照してください。

この操作によって返される値は、 *Outbuffer*の**Status**メンバーにも格納されます。

<a name="remarks"></a>注釈
-------

\_EXT\_型指定された\_データ\_ANSI[**要求**](request.md)操作によっ\_て実行されるサブ操作は、型指定された[**ext\_データ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdbgexts/ns-wdbgexts-_ext_typed_data)構造体の**操作**メンバーによって決定されます。 [**EXT\_TDOP**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdbgexts/ne-wdbgexts-_ext_tdop)列挙体の値を取得します。

## <a name="span-idsee_alsospansee-also"></a><span id="see_also"></span>関連項目


[**EXT\_型指定された\_データ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdbgexts/ns-wdbgexts-_ext_typed_data)

[**EXT\_TDOP**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdbgexts/ne-wdbgexts-_ext_tdop)

[**申請**](request.md)

 

 







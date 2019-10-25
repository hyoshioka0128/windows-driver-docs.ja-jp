---
title: EXT\_TDOP\_\_フィールド\_のオフセットを取得します
description: EXT\_TDOP\_、DEBUG\_要求の\_フィールド\_OFFSET サブ操作で、型指定された\_データ\_データ\_ANSI 要求操作は、構造内のメンバーのオフセットを返します。
ms.assetid: 2703d518-1bc3-42a2-9a22-f9ea88a12c05
keywords:
- EXT_TDOP_GET_FIELD_OFFSET Windows のデバッグ
topic_type:
- apiref
api_name:
- EXT_TDOP_GET_FIELD_OFFSET
api_type:
- NA
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: a2b1b59ef256d9f1739f797efd2f33c772a563ae
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72826468"
---
# <a name="ext_tdop_get_field_offset"></a>EXT\_TDOP\_\_フィールド\_のオフセットを取得します


EXT\_TDOP\_、DEBUG\_要求の\_フィールド\_OFFSET サブ操作 (型指定された[ **\_データ\_データ\_ANSI**](debug-request-ext-typed-data-ansi.md)[**要求**](request.md)操作では、メンバーのオフセットが返されます。データ.

**Parameters**

<span id="Operation"></span><span id="operation"></span><span id="OPERATION"></span>**運用**  
このサブ操作の\_フィールド\_オフセットを取得\_には、EXT\_TDOP に設定します。

<span id="InData"></span><span id="indata"></span><span id="INDATA"></span>**InData**  
オフセットが要求されているメンバーを含む構造体のインスタンスを表す型指定されたデータを指定します。

<span id="InStrIndex"></span><span id="instrindex"></span><span id="INSTRINDEX"></span>**InStrIndex**  
オフセットが要求されるメンバーの名前を指定します。 名前はドットで区切られたパスであり、サブメンバーを含めることができます。 たとえば、 **mymember. mysubmember**です。 このドット区切りパスのポインターは、自動的に逆参照されます。 ただし、通常の C ポインター逆参照演算子 ( **-&gt;** ) の代わりに、ここではドット演算子 ( **.** ) を使用する必要があります。

<span id="Out32"></span><span id="out32"></span><span id="OUT32"></span>**Out32**  
構造体のインスタンス内のメンバーのオフセットを受け取ります。 これは、構造体のインスタンスの先頭とメンバーの間のバイト数です。

<span id="Status"></span><span id="status"></span><span id="STATUS"></span>**オンライン**  
このサブ操作によって返されたステータスコードを受け取ります。 これは、[**要求**](request.md)によって返される値と同じです。

<a name="remarks"></a>注釈
-------

EXT\_TDOP\_取得\_フィールド\_オフセットは、 [**ext\_TDOP**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdbgexts/ne-wdbgexts-_ext_tdop)列挙の値です。

このサブ操作のパラメーターは、 [**EXT\_型指定**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdbgexts/ns-wdbgexts-_ext_typed_data)された\_データ構造体のメンバーです。 前の Parameters セクションに記載されていない EXT\_\_型のメンバーは、このサブ操作では使用されず、0に設定する必要があります。 前の Parameters セクションのメンバーの説明では、メンバーがどのように使用されるかを指定します。 詳細については、「 **EXT\_型指定**された\_データ」を参照してください。

## <a name="span-idsee_alsospansee-also"></a><span id="see_also"></span>関連項目


[ **\_要求\_EXT\_型指定された\_データ\_ANSI**](debug-request-ext-typed-data-ansi.md)

[**EXT\_TDOP**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdbgexts/ne-wdbgexts-_ext_tdop)

[**EXT\_型指定された\_データ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdbgexts/ns-wdbgexts-_ext_typed_data)

[**申請**](request.md)

 

 







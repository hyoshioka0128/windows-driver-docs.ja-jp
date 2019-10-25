---
title: EXT\_TDOP\_\_フィールドを取得します
description: EXT\_TDOP\_デバッグ\_要求の\_フィールドのサブ操作を取得\_データ\_ANSI 要求操作は、指定された構造体のメンバーを表す型指定されたデータの説明を返します。
ms.assetid: c91c0ecf-c093-4585-a6b5-6bda91899ec3
keywords:
- EXT_TDOP_GET_FIELD Windows のデバッグ
topic_type:
- apiref
api_name:
- EXT_TDOP_GET_FIELD
api_type:
- NA
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: a31a6261242ddb00639cf9bcac9489bed850431c
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72826462"
---
# <a name="ext_tdop_get_field"></a>EXT\_TDOP\_\_フィールドを取得します


EXT\_TDOP\_デバッグ\_要求の\_フィールドのサブ操作を取得\_[**データ\_ANSI**](debug-request-ext-typed-data-ansi.md)[**要求**](request.md)操作のメンバーを表す型指定されたデータの説明を返します。指定された構造体。

**Parameters**

<span id="Operation"></span><span id="operation"></span><span id="OPERATION"></span>**運用**  
このサブ操作の\_フィールドを取得\_には、EXT\_TDOP に設定します。

<span id="InData"></span><span id="indata"></span><span id="INDATA"></span>**InData**  
メンバーを必要とする構造体を記述する、型指定された[ **\_データのデバッグ\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdbgexts/ns-wdbgexts-_debug_typed_data)のインスタンスを指定します。

<span id="OutData"></span><span id="outdata"></span><span id="OUTDATA"></span>**OutData**  
要求されたメンバーの型指定された[ **\_データ\_、デバッグ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdbgexts/ns-wdbgexts-_debug_typed_data)のインスタンスを受信します。

<span id="InStrIndex"></span><span id="instrindex"></span><span id="INSTRINDEX"></span>**InStrIndex**  
要求されたメンバーの名前を指定します。 メンバーの名前はドットで区切られたパスであり、サブメンバーを含めることができ**ます。たとえば、mymember. mysubmember**です。 このドット区切りパスのポインターは、自動的に逆参照されます。 ただし、通常の C ポインター逆参照演算子 ( **-&gt;** ) の代わりに、ここではドット演算子 ( **.** ) を使用する必要があります。

<span id="Status"></span><span id="status"></span><span id="STATUS"></span>**オンライン**  
このサブ操作によって返されたステータスコードを受け取ります。 これは、[**要求**](request.md)によって返される値と同じです。

<a name="remarks"></a>注釈
-------

EXT\_TDOP\_取得\_フィールドは、 [**ext\_tdop**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdbgexts/ne-wdbgexts-_ext_tdop)列挙の値です。

このサブ操作のパラメーターは、 [**EXT\_型指定**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdbgexts/ns-wdbgexts-_ext_typed_data)された\_データ構造体のメンバーです。 前の Parameters セクションに記載されていない EXT\_\_型のメンバーは、このサブ操作では使用されず、0に設定する必要があります。 前の Parameters セクションのメンバーの説明では、メンバーがどのように使用されるかを指定します。 詳細については、「 **EXT\_型指定**された\_データ」を参照してください。

## <a name="span-idsee_alsospansee-also"></a><span id="see_also"></span>関連項目


[ **\_要求\_EXT\_型指定された\_データ\_ANSI**](debug-request-ext-typed-data-ansi.md)

[**EXT\_TDOP**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdbgexts/ne-wdbgexts-_ext_tdop)

[**EXT\_型指定された\_データ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdbgexts/ns-wdbgexts-_ext_typed_data)

[**申請**](request.md)

 

 







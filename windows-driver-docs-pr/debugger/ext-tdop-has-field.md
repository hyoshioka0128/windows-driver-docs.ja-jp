---
title: EXT\_TDOP\_に\_フィールドがあります
description: EXT\_TDOP\_には、デバッグ\_要求のフィールドのサブ操作が\_ます。型指定された\_データ\_、ANSI 要求操作によって、構造体に指定されたメンバーが含まれているかどうかが判断されます。\_\_
ms.assetid: c1486aff-63d3-4ceb-8dce-45a9c5835c99
keywords:
- EXT_TDOP_HAS_FIELD Windows のデバッグ
topic_type:
- apiref
api_name:
- EXT_TDOP_HAS_FIELD
api_type:
- NA
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 823a524bfb7f71986caec66646f6a97e13c56066
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838769"
---
# <a name="ext_tdop_has_field"></a>EXT\_TDOP\_に\_フィールドがあります


EXT\_TDOP\_には、[**デバッグ\_要求**](debug-request-ext-typed-data-ansi.md)のフィールドのサブ操作が\_ます。型指定された\_データ\_、ANSI[**要求**](request.md)操作によって、構造体に指定されたメンバーが含まれているかどうかが判断されます。\_\_

**パラメーター**

<span id="Operation"></span><span id="operation"></span><span id="OPERATION"></span>**運用**  
このサブ操作の\_フィールドを持つ\_には、EXT\_TDOP を設定します。

<span id="InData"></span><span id="indata"></span><span id="INDATA"></span>**InData**  
メンバーが存在するかどうかをチェックする型指定されたデータを指定します。 型指定されたデータは、最初に、構造体のインスタンスを表しているかどうかを確認します。次に、構造体が、指定されたメンバーを含んでいるかどうかを確認します。

<span id="InStrIndex"></span><span id="instrindex"></span><span id="INSTRINDEX"></span>**InStrIndex**  
メンバーの名前を指定します。 名前はドットで区切られたパスであり、サブメンバーを含めることができ**ます。たとえば、mymember. mysubmember**です。 このドット区切りパスのポインターは、自動的に逆参照されます。 ただし、通常の C ポインター逆参照演算子 ( **-&gt;** ) の代わりに、ここではドット演算子 ( **.** ) を使用する必要があります。

<span id="Status"></span><span id="status"></span><span id="STATUS"></span>**オンライン**  
このサブ操作によって返されたステータスコードを受け取ります。 これは、[**要求**](request.md)によって返される値と同じです。

型指定されたデータにメンバーが含まれている場合、 **Status**は S\_OK を受け取ります。 型指定されたデータにメンバーが含まれていない場合、 **Status**は E\_nointerface を受け取ります。 その他のエラー値も返される場合があります。

<a name="remarks"></a>解説
-------

EXT\_TDOP\_には、 [**ext\_tdop**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdbgexts/ne-wdbgexts-_ext_tdop)列挙型の値\_フィールドがあります。

このサブ操作のパラメーターは、 [**EXT\_型指定**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdbgexts/ns-wdbgexts-_ext_typed_data)された\_データ構造体のメンバーです。 前の Parameters セクションに記載されていない EXT\_\_型のメンバーは、このサブ操作では使用されず、0に設定する必要があります。 前の Parameters セクションのメンバーの説明では、メンバーがどのように使用されるかを指定します。 詳細については、「 **EXT\_型指定**された\_データ」を参照してください。

## <a name="span-idsee_alsospansee-also"></a><span id="see_also"></span>関連項目


[ **\_要求\_EXT\_型指定された\_データ\_ANSI**](debug-request-ext-typed-data-ansi.md)

[**EXT\_TDOP**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdbgexts/ne-wdbgexts-_ext_tdop)

[**EXT\_型指定された\_データ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdbgexts/ns-wdbgexts-_ext_typed_data)

[**Request**](request.md)

 

 







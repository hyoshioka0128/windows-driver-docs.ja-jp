---
title: EXT\_TDOP\_\_配列\_要素を取得します
description: EXT\_TDOP\_、デバッグ\_要求の\_配列\_要素のサブ操作\_データ\_ANSI 要求操作では、配列から要素を返します。
ms.assetid: 67c87b14-3580-4507-884e-b02576ce7be2
keywords:
- EXT_TDOP_GET_ARRAY_ELEMENT Windows のデバッグ
topic_type:
- apiref
api_name:
- EXT_TDOP_GET_ARRAY_ELEMENT
api_type:
- NA
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: dc33b51ff92029743dfe6086bed78ac87278c031
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72826510"
---
# <a name="ext_tdop_get_array_element"></a>EXT\_TDOP\_\_配列\_要素を取得します


EXT\_TDOP\_、デバッグ\_要求の\_配列\_要素のサブ操作[ **\_データ\_ANSI**](debug-request-ext-typed-data-ansi.md)[**要求**](request.md)操作では、配列から要素を返します。

**Parameters**

<span id="Operation"></span><span id="operation"></span><span id="OPERATION"></span>**運用**  
このサブ操作の\_配列\_要素を取得\_には、EXT\_TDOP に設定します。

<span id="InData"></span><span id="indata"></span><span id="INDATA"></span>**InData**  
要素が要求されている配列を指定します。 **Indata**では、ポインターを指定することもできます。この場合、配列として扱われます。

<span id="OutData"></span><span id="outdata"></span><span id="OUTDATA"></span>**OutData**  
要求された要素を配列から受け取ります。

<span id="In64"></span><span id="in64"></span><span id="IN64"></span>**In64**  
配列内の要素のインデックスを指定します。

<span id="Status"></span><span id="status"></span><span id="STATUS"></span>**オンライン**  
このサブ操作によって返されたステータスコードを受け取ります。 これは、[**要求**](request.md)によって返される値と同じです。

<a name="remarks"></a>注釈
-------

EXT\_TDOP\_\_配列の取得\_要素は、 [**ext\_tdop**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdbgexts/ne-wdbgexts-_ext_tdop)列挙の値です。

このサブ操作のパラメーターは、 [**EXT\_型指定**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdbgexts/ns-wdbgexts-_ext_typed_data)された\_データ構造体のメンバーです。 前の Parameters セクションに記載されていない EXT\_\_型のメンバーは、このサブ操作では使用されず、0に設定する必要があります。 前の Parameters セクションのメンバーの説明では、メンバーがどのように使用されるかを指定します。 詳細については、「 **EXT\_型指定**された\_データ」を参照してください。

## <a name="span-idsee_alsospansee-also"></a><span id="see_also"></span>関連項目


[ **\_要求\_EXT\_型指定された\_データ\_ANSI**](debug-request-ext-typed-data-ansi.md)

[**EXT\_TDOP**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdbgexts/ne-wdbgexts-_ext_tdop)

[**EXT\_型指定された\_データ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdbgexts/ns-wdbgexts-_ext_typed_data)

[**申請**](request.md)

 

 







---
title: EXT\_TDOP\_取得\_逆参照
description: EXT\_TDOP\_は、DEBUG\_要求の\_逆参照サブ操作を取得します。型指定された\_データ\_、ANSI 要求操作はポインターを逆参照し、それが指す値を返します。
ms.assetid: 0b5eed03-4241-4038-8950-12c82c2d086f
keywords:
- EXT_TDOP_GET_DEREFERENCE Windows のデバッグ
topic_type:
- apiref
api_name:
- EXT_TDOP_GET_DEREFERENCE
api_type:
- NA
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2bef65e09540480d41536f659e46b4c92be52abd
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72826490"
---
# <a name="ext_tdop_get_dereference"></a>EXT\_TDOP\_取得\_逆参照


EXT\_TDOP\_は、DEBUG\_要求の\_逆参照サブ操作を取得し\_[**データ型指定**](debug-request-ext-typed-data-ansi.md)された\_データ\_、ANSI[**要求**](request.md)操作はポインターを逆参照し、その値を返します。宛先。

**Parameters**

<span id="Operation"></span><span id="operation"></span><span id="OPERATION"></span>**運用**  
このサブ操作の\_逆参照を取得\_には、EXT\_TDOP に設定します。

<span id="InData"></span><span id="indata"></span><span id="INDATA"></span>**InData**  
逆参照するポインターを指定します。 **Indata**では配列を指定することもできます。この場合、配列内の最初の要素が返されます。

<span id="OutData"></span><span id="outdata"></span><span id="OUTDATA"></span>**OutData**  
が指す値を受け取ります。

<span id="Status"></span><span id="status"></span><span id="STATUS"></span>**オンライン**  
このサブ操作によって返されたステータスコードを受け取ります。 これは、[**要求**](request.md)によって返される値と同じです。

<a name="remarks"></a>注釈
-------

EXT\_TDOP\_取得\_逆参照は、 [**ext\_tdop**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdbgexts/ne-wdbgexts-_ext_tdop)列挙の値です。

このサブ操作のパラメーターは、 [**EXT\_型指定**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdbgexts/ns-wdbgexts-_ext_typed_data)された\_データ構造体のメンバーです。 前の Parameters セクションに記載されていない EXT\_\_型のメンバーは、このサブ操作では使用されず、0に設定する必要があります。 前の Parameters セクションのメンバーの説明では、メンバーがどのように使用されるかを指定します。 詳細については、「 **EXT\_型指定**された\_データ」を参照してください。

## <a name="span-idsee_alsospansee-also"></a><span id="see_also"></span>関連項目


[ **\_要求\_EXT\_型指定された\_データ\_ANSI**](debug-request-ext-typed-data-ansi.md)

[**EXT\_TDOP**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdbgexts/ne-wdbgexts-_ext_tdop)

[**EXT\_型指定された\_データ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdbgexts/ns-wdbgexts-_ext_typed_data)

[**申請**](request.md)

 

 







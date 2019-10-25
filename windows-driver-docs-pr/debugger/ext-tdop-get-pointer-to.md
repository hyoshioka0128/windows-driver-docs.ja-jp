---
title: EXT\_TDOP\_\_ポインター\_を取得します。
description: EXT\_TDOP\_、デバッグ\_要求のサブ操作に対する\_ポインター\_を取得します。 ANSI 要求操作では、型指定されたデータ型の新しい説明が返されます。指定された型指定されたデータ。
ms.assetid: 05db8e07-b94f-4cf3-b01b-a918b737ecf4
keywords:
- EXT_TDOP_GET_POINTER_TO Windows のデバッグ
topic_type:
- apiref
api_name:
- EXT_TDOP_GET_POINTER_TO
api_type:
- NA
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: c7ce87048a728ce33c0d722741499d34dd583230
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72826449"
---
# <a name="ext_tdop_get_pointer_to"></a>EXT\_TDOP\_\_ポインター\_を取得します。


EXT\_TDOP\_、[**デバッグ\_要求**](debug-request-ext-typed-data-ansi.md)のサブ操作に対する\_ポインター\_を取得します\_データ\_ANSI[**要求**](request.md)操作は、型指定された新しいデータの説明を返します。指定した型指定されたデータへのポインターを表します。

**Parameters**

<span id="Operation"></span><span id="operation"></span><span id="OPERATION"></span>**運用**  
このサブ操作に対して\_ポインター\_を取得\_には、EXT\_TDOP に設定します。

<span id="InData"></span><span id="indata"></span><span id="INDATA"></span>**InData**  
ポインターが返される元の型指定されたデータの説明を指定します。

<span id="OutData"></span><span id="outdata"></span><span id="OUTDATA"></span>**OutData**  
**Indata**によって指定された型指定されたデータへのポインターを表す、型指定されたデータの記述を受け取ります。

<span id="Status"></span><span id="status"></span><span id="STATUS"></span>**オンライン**  
このサブ操作によって返されたステータスコードを受け取ります。 これは、[**要求**](request.md)によって返される値と同じです。

<a name="remarks"></a>注釈
-------

EXT\_TDOP\_を取得\_ポインター\_は、 [**ext\_tdop**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdbgexts/ne-wdbgexts-_ext_tdop)列挙の値です。

このサブ操作のパラメーターは、 [**EXT\_型指定**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdbgexts/ns-wdbgexts-_ext_typed_data)された\_データ構造体のメンバーです。 前の Parameters セクションに記載されていない EXT\_\_型のメンバーは、このサブ操作では使用されず、0に設定する必要があります。 前の Parameters セクションのメンバーの説明では、メンバーがどのように使用されるかを指定します。 詳細については、「 **EXT\_型指定**された\_データ」を参照してください。

## <a name="span-idsee_alsospansee-also"></a><span id="see_also"></span>関連項目


[ **\_要求\_EXT\_型指定された\_データ\_ANSI**](debug-request-ext-typed-data-ansi.md)

[**EXT\_TDOP**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdbgexts/ne-wdbgexts-_ext_tdop)

[**EXT\_型指定された\_データ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdbgexts/ns-wdbgexts-_ext_typed_data)

[**申請**](request.md)

 

 







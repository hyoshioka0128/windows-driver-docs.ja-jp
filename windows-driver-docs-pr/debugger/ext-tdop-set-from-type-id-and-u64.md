---
title: EXT\_TDOP\_\_型\_ID\_および\_U64 から\_を設定します。
description: EXT\_TDOP\_、\_型\_ID\_と\_U64 サブ操作 (DEBUG\_REQUEST\_EXT\_型指定された\_データ\_ANSI 要求) の\_を設定します。操作は、データ型とメモリ位置から型指定されたデータの説明を作成します。
ms.assetid: 5b1ee241-6f35-4bbf-b4e0-3cefa5a39dde
keywords:
- EXT_TDOP_SET_FROM_TYPE_ID_AND_U64 Windows のデバッグ
topic_type:
- apiref
api_name:
- EXT_TDOP_SET_FROM_TYPE_ID_AND_U64
api_type:
- NA
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 64dafc6b88eeef4307a5df3445e60d89bd51981c
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838766"
---
# <a name="ext_tdop_set_from_type_id_and_u64"></a>EXT\_TDOP\_\_型\_ID\_および\_U64 から\_を設定します。


EXT\_TDOP\_、\_型\_ID\_と\_U64 サブ操作 ( [**DEBUG\_request\_EXT\_型指定された\_データ\_ANSI**](debug-request-ext-typed-data-ansi.md)[**要求**](request.md)) の\_を設定します。操作は、データ型とメモリ位置から型指定されたデータの説明を作成します。

**パラメーター**

<span id="Operation"></span><span id="operation"></span><span id="OPERATION"></span>**運用**  
このサブ操作に対して\_型\_ID\_および\_U64 から\_を設定\_には、EXT\_TDOP を設定します。

<span id="Flags"></span><span id="flags"></span><span id="FLAGS"></span>**示す**  
型指定されたデータの値が存在するターゲットのメモリを示すビットフラグを指定します。 これらのフラグの詳細については、「 [**EXT\_型指定**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdbgexts/ns-wdbgexts-_ext_typed_data)された\_データ」を参照してください。

<span id="InData"></span><span id="indata"></span><span id="INDATA"></span>**InData**  
型とメモリの場所を指定します。 この[**デバッグ\_型指定**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdbgexts/ns-wdbgexts-_debug_typed_data)された\_データ構造体のインスタンスを手動で作成し、必要なメンバーを設定できます。 次のメンバーが使用されます。

<span id="ModBase"></span><span id="modbase"></span><span id="MODBASE"></span>**ModBase**  
型を含むモジュールのベースアドレスのターゲットの仮想メモリ内の場所を指定します。

<span id="Offset"></span><span id="offset"></span><span id="OFFSET"></span>**影**  
ターゲットのデータのメモリ内の場所を指定します。 **オフセット**は、物理メモリアドレスであることを指定する**フラグにフラグ**が**存在する場合**を除き、仮想メモリアドレスです。

<span id="TypeId"></span><span id="typeid"></span><span id="TYPEID"></span>**TypeId**  
型の型 ID を指定します。

<span id="OutData"></span><span id="outdata"></span><span id="OUTDATA"></span>**OutData**  
型指定されたデータの説明を受け取ります。

<span id="Status"></span><span id="status"></span><span id="STATUS"></span>**オンライン**  
このサブ操作によって返されたステータスコードを受け取ります。 これは、[**要求**](request.md)によって返される値と同じです。

<a name="remarks"></a>解説
-------

EXT\_TDOP\_\_型\_ID\_から\_を設定します。\_U64 は[**ext\_TDOP**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdbgexts/ne-wdbgexts-_ext_tdop)列挙の値です。

このサブ操作のパラメーターは、 [**EXT\_型指定**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdbgexts/ns-wdbgexts-_ext_typed_data)された\_データ構造体のメンバーです。 前の Parameters セクションに記載されていない EXT\_\_型のメンバーは、このサブ操作では使用されず、0に設定する必要があります。 前の Parameters セクションのメンバーの説明では、メンバーがどのように使用されるかを指定します。 詳細については、「 **EXT\_型指定**された\_データ」を参照してください。

## <a name="span-idsee_alsospansee-also"></a><span id="see_also"></span>関連項目


[ **\_要求\_EXT\_型指定された\_データ\_ANSI**](debug-request-ext-typed-data-ansi.md)

[**EXT\_TDOP**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdbgexts/ne-wdbgexts-_ext_tdop)

[**EXT\_型指定された\_データ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdbgexts/ns-wdbgexts-_ext_typed_data)

[**Request**](request.md)

 

 







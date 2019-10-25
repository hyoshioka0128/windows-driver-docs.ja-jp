---
title: EXT\_TDOP\_出力\_単純な\_値
description: EXT\_TDOP\_出力\_、デバッグ\_要求の単純\_値のサブ操作\_データ\_の型指定された\_データ\_ANSI 要求操作は、指定された型指定されたデータの値を出力します。
ms.assetid: dce51823-34e9-43b9-9cbd-41b436b43ccb
keywords:
- EXT_TDOP_OUTPUT_SIMPLE_VALUE Windows のデバッグ
topic_type:
- apiref
api_name:
- EXT_TDOP_OUTPUT_SIMPLE_VALUE
api_type:
- NA
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 74ca3999b37f2d90acf8c1a852d90bad5713b0e7
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838768"
---
# <a name="ext_tdop_output_simple_value"></a>EXT\_TDOP\_出力\_単純な\_値


EXT\_TDOP\_出力\_単純な\_値による[**デバッグ\_要求のサブ操作\_データ\_ANSI**](debug-request-ext-typed-data-ansi.md)[**要求**](request.md)操作の型指定された型の値を出力します。データ.\_\_

**パラメーター**

<span id="Operation"></span><span id="operation"></span><span id="OPERATION"></span>**運用**  
EXT\_TDOP\_出力\_このサブ操作の単純\_値に設定されます。

<span id="InData"></span><span id="indata"></span><span id="INDATA"></span>**InData**  
値が出力される型指定されたデータを指定します。

<span id="Status"></span><span id="status"></span><span id="STATUS"></span>**オンライン**  
このサブ操作によって返されたステータスコードを受け取ります。 これは、[**要求**](request.md)によって返される値と同じです。

<a name="remarks"></a>解説
-------

値は書式設定され、デバッガーエンジンの[出力コールバック](https://docs.microsoft.com/windows-hardware/drivers/debugger/using-input-and-output#output-callbacks)に送信されます。

EXT\_TDOP\_出力\_単純\_値は、 [**ext\_TDOP**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdbgexts/ne-wdbgexts-_ext_tdop)列挙の値です。

このサブ操作のパラメーターは、 [**EXT\_型指定**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdbgexts/ns-wdbgexts-_ext_typed_data)された\_データ構造体のメンバーです。 前の Parameters セクションに記載されていない EXT\_\_型のメンバーは、このサブ操作では使用されず、0に設定する必要があります。 前の Parameters セクションのメンバーの説明では、メンバーがどのように使用されるかを指定します。 詳細については、「 **EXT\_型指定**された\_データ」を参照してください。

## <a name="span-idsee_alsospansee-also"></a><span id="see_also"></span>関連項目


[ **\_要求\_EXT\_型指定された\_データ\_ANSI**](debug-request-ext-typed-data-ansi.md)

[**EXT\_TDOP**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdbgexts/ne-wdbgexts-_ext_tdop)

[**EXT\_型指定された\_データ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdbgexts/ns-wdbgexts-_ext_typed_data)

[**Request**](request.md)

 

 







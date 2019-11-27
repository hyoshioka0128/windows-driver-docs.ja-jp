---
title: EXT\_TDOP\_出力\_型\_名
description: EXT\_TDOP\_出力\_型の\_名前を指定した\_データ\_\_データ\_の型指定されたデータの型名を出力します。\_
ms.assetid: eb0a9026-92fd-4b3e-b513-b691221b3196
keywords:
- Windows デバッグの EXT_TDOP_OUTPUT_TYPE_NAME
topic_type:
- apiref
api_name:
- EXT_TDOP_OUTPUT_TYPE_NAME
api_type:
- NA
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0fd7e3b15c2bfd404439abd149ec659f6f635cd0
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72826426"
---
# <a name="ext_tdop_output_type_name"></a>EXT\_TDOP\_出力\_型\_名


EXT\_TDOP\_出力\_型の\_名前を指定した[ **\_データ**](debug-request-ext-typed-data-ansi.md)[](request.md)\_\_データ\_の型指定されたデータの型名を出力します。\_

**パラメーター**

<span id="Operation"></span><span id="operation"></span><span id="OPERATION"></span>**運用**  
EXT\_TDOP\_出力\_このサブ操作の\_名に設定します。

<span id="InData"></span><span id="indata"></span><span id="INDATA"></span>**InData**  
型名を出力する型指定されたデータを指定します。

<span id="Status"></span><span id="status"></span><span id="STATUS"></span>**オンライン**  
このサブ操作によって返されたステータスコードを受け取ります。 これは、[**要求**](request.md)によって返される値と同じです。

<a name="remarks"></a>注釈
-------

型名は、デバッガーエンジンの[出力コールバック](https://docs.microsoft.com/windows-hardware/drivers/debugger/using-input-and-output#output-callbacks)に送信されます。

EXT\_TDOP\_出力\_型\_NAME は、 [**ext\_tdop**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdbgexts/ne-wdbgexts-_ext_tdop)列挙の値です。

このサブ操作のパラメーターは、 [**EXT\_型指定**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdbgexts/ns-wdbgexts-_ext_typed_data)された\_データ構造体のメンバーです。 前の Parameters セクションに記載されていない EXT\_\_型のメンバーは、このサブ操作では使用されず、0に設定する必要があります。 前の Parameters セクションのメンバーの説明では、メンバーがどのように使用されるかを指定します。 詳細については、「 **EXT\_型指定**された\_データ」を参照してください。

## <a name="span-idsee_alsospansee-also"></a><span id="see_also"></span>関連項目


[ **\_要求\_EXT\_型指定された\_データ\_ANSI**](debug-request-ext-typed-data-ansi.md)

[**EXT\_TDOP**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdbgexts/ne-wdbgexts-_ext_tdop)

[**EXT\_型指定された\_データ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdbgexts/ns-wdbgexts-_ext_typed_data)

[**申請**](request.md)

 

 







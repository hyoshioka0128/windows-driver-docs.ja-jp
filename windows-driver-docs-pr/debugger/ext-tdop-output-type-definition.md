---
title: EXT\_TDOP\_出力\_型\_の定義
description: EXT\_TDOP\_出力\_型\_定義の\_\_データ\_の型指定されたデータ型指定されたデータの定義を出力します.
ms.assetid: 88e97066-f471-4e6c-9b9b-369f31da5bde
keywords:
- EXT_TDOP_OUTPUT_TYPE_DEFINITION Windows のデバッグ
topic_type:
- apiref
api_name:
- EXT_TDOP_OUTPUT_TYPE_DEFINITION
api_type:
- NA
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 255d778515c1001b4e0d12abbae9e941de0ce73f
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72826428"
---
# <a name="ext_tdop_output_type_definition"></a>EXT\_TDOP\_出力\_型\_の定義


EXT\_TDOP\_出力\_型の\_定義のサブ操作[ **\_データ**](debug-request-ext-typed-data-ansi.md)を入力\_データ\_ANSI[**要求**](request.md)操作の型の定義を出力します。指定した型指定されたデータ。

**Parameters**

<span id="Operation"></span><span id="operation"></span><span id="OPERATION"></span>**運用**  
このサブ操作の\_の種類\_定義を\_には、EXT\_TDOP を設定します。

<span id="InData"></span><span id="indata"></span><span id="INDATA"></span>**InData**  
型の定義が出力される型指定されたデータを指定します。

<span id="Status"></span><span id="status"></span><span id="STATUS"></span>**オンライン**  
このサブ操作によって返されたステータスコードを受け取ります。 これは、[**要求**](request.md)によって返される値と同じです。

<a name="remarks"></a>注釈
-------

型の定義は書式設定され、デバッガーエンジンの[出力コールバック](https://docs.microsoft.com/windows-hardware/drivers/debugger/using-input-and-output#output-callbacks)に送信されます。

EXT\_TDOP\_出力\_型\_定義は、 [**ext\_tdop**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdbgexts/ne-wdbgexts-_ext_tdop)列挙の値です。

このサブ操作のパラメーターは、 [**EXT\_型指定**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdbgexts/ns-wdbgexts-_ext_typed_data)された\_データ構造体のメンバーです。 前の Parameters セクションに記載されていない EXT\_\_型のメンバーは、このサブ操作では使用されず、0に設定する必要があります。 前の Parameters セクションのメンバーの説明では、メンバーがどのように使用されるかを指定します。 詳細については、「 **EXT\_型指定**された\_データ」を参照してください。

## <a name="span-idsee_alsospansee-also"></a><span id="see_also"></span>関連項目


[ **\_要求\_EXT\_型指定された\_データ\_ANSI**](debug-request-ext-typed-data-ansi.md)

[**EXT\_TDOP**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdbgexts/ne-wdbgexts-_ext_tdop)

[**EXT\_型指定された\_データ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdbgexts/ns-wdbgexts-_ext_typed_data)

[**申請**](request.md)

 

 







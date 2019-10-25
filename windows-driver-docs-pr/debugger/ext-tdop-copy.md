---
title: EXT\_TDOP\_コピー
description: EXT\_TDOP\_デバッグ\_\_要求のサブ操作をコピーし、型指定された\_データ\_ANSI 要求操作によって、型指定されたデータの説明のコピーが作成されます。\_
ms.assetid: 2de920de-db93-408d-8e80-a29c4e2930a0
keywords:
- EXT_TDOP_COPY Windows のデバッグ
topic_type:
- apiref
api_name:
- EXT_TDOP_COPY
api_type:
- NA
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: f258b19527495e4e9e669aedb3cbeb371519abcc
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838771"
---
# <a name="ext_tdop_copy"></a>EXT\_TDOP\_コピー


EXT\_TDOP\_[**デバッグ\_\_要求**](debug-request-ext-typed-data-ansi.md)のサブ操作をコピーし、型指定された\_データ\_ANSI[**要求**](request.md)操作によって、型指定されたデータの説明のコピーが作成されます。\_

**パラメーター**

<span id="Operation"></span><span id="operation"></span><span id="OPERATION"></span>**運用**  
このサブ操作には、EXT\_TDOP\_コピーを設定します。

<span id="InData"></span><span id="indata"></span><span id="INDATA"></span>**InData**  
[**デバッグ\_型**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdbgexts/ns-wdbgexts-_debug_typed_data)指定された\_データ構造体の元のインスタンスを指定します。

<span id="OutData"></span><span id="outdata"></span><span id="OUTDATA"></span>**OutData**  
**Indata**によって指定された型指定された[ **\_データ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdbgexts/ns-wdbgexts-_debug_typed_data)構造体\_、デバッグのインスタンスのコピーを受け取ります。

<span id="Status"></span><span id="status"></span><span id="STATUS"></span>**オンライン**  
このサブ操作によって返されたステータスコードを受け取ります。 これは、[**要求**](request.md)によって返される値と同じです。

<a name="remarks"></a>解説
-------

EXT\_TDOP\_コピーは、 [**ext\_tdop**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdbgexts/ne-wdbgexts-_ext_tdop)列挙の値です。

このサブ操作のパラメーターは、 [**EXT\_型指定**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdbgexts/ns-wdbgexts-_ext_typed_data)された\_データ構造体のメンバーです。 前の Parameters セクションに記載されていない EXT\_\_型のメンバーは、このサブ操作では使用されず、0に設定する必要があります。 前の Parameters セクションのメンバーの説明では、メンバーがどのように使用されるかを指定します。 メンバーの詳細については、「 **EXT\_型指定**された\_データ」を参照してください。

## <a name="span-idsee_alsospansee-also"></a><span id="see_also"></span>関連項目


[ **\_要求\_EXT\_型指定された\_データ\_ANSI**](debug-request-ext-typed-data-ansi.md)

[**EXT\_TDOP**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdbgexts/ne-wdbgexts-_ext_tdop)

[**EXT\_型指定された\_データ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdbgexts/ns-wdbgexts-_ext_typed_data)

[**Request**](request.md)

 

 







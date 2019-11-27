---
title: EXT\_TDOP\_\_型\_のサイズを取得します
description: EXT\_TDOP\_、DEBUG\_要求の\_TYPE\_SIZE サブ操作を\_の型指定されたデータ\_データ\_の型指定されたデータのサイズを返します。\_
ms.assetid: 3e668522-60bb-4abc-87b8-6b1beea573a3
keywords:
- Windows デバッグの EXT_TDOP_GET_TYPE_SIZE
topic_type:
- apiref
api_name:
- EXT_TDOP_GET_TYPE_SIZE
api_type:
- NA
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8e5c5a751672ed8f391fd16436d135b02a5f16cc
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72826431"
---
# <a name="ext_tdop_get_type_size"></a>EXT\_TDOP\_\_型\_のサイズを取得します


EXT\_TDOP\_、 [**DEBUG\_要求**](debug-request-ext-typed-data-ansi.md)[](request.md)の\_TYPE\_SIZE サブ操作を\_の型指定されたデータ\_データ\_の型指定されたデータのサイズを返します。\_

**パラメーター**

<span id="Operation"></span><span id="operation"></span><span id="OPERATION"></span>**運用**  
このサブ操作の\_型\_サイズを取得\_には、EXT\_TDOP に設定します。

<span id="InData"></span><span id="indata"></span><span id="INDATA"></span>**InData**  
サイズが要求される型指定されたデータを指定します。

<span id="Out32"></span><span id="out32"></span><span id="OUT32"></span>**Out32**  
型指定されたデータのサイズ (バイト単位) を受信します。

<span id="Status"></span><span id="status"></span><span id="STATUS"></span>**オンライン**  
このサブ操作によって返されたステータスコードを受け取ります。 これは、[**要求**](request.md)によって返される値と同じです。

<a name="remarks"></a>注釈
-------

EXT\_TDOP\_\_\_型を取得するには、 [**ext\_tdop**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdbgexts/ne-wdbgexts-_ext_tdop)列挙体の値を指定します。

このサブ操作のパラメーターは、 [**EXT\_型指定**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdbgexts/ns-wdbgexts-_ext_typed_data)された\_データ構造体のメンバーです。 前の Parameters セクションに記載されていない EXT\_\_型のメンバーは、このサブ操作では使用されず、0に設定する必要があります。 前の Parameters セクションのメンバーの説明では、メンバーがどのように使用されるかを指定します。 詳細については、「 **EXT\_型指定**された\_データ」を参照してください。

## <a name="span-idsee_alsospansee-also"></a><span id="see_also"></span>関連項目


[ **\_要求\_EXT\_型指定された\_データ\_ANSI**](debug-request-ext-typed-data-ansi.md)

[**EXT\_TDOP**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdbgexts/ne-wdbgexts-_ext_tdop)

[**EXT\_型指定された\_データ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdbgexts/ns-wdbgexts-_ext_typed_data)

[**申請**](request.md)

 

 







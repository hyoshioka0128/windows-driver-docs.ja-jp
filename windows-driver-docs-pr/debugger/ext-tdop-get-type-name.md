---
title: EXT\_TDOP\_\_型\_名を取得します
description: EXT\_TDOP\_、DEBUG\_要求の\_型\_NAME サブ操作を取得\_データ\_ANSI 要求操作は、指定された型指定されたデータの型名を返します。
ms.assetid: ce896ded-a49e-4f89-969e-6d464e583ca8
keywords:
- EXT_TDOP_GET_TYPE_NAME Windows のデバッグ
topic_type:
- apiref
api_name:
- EXT_TDOP_GET_TYPE_NAME
api_type:
- NA
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: e0db3ddb92be6a3c42334b7748a63c6d45fb9391
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72826437"
---
# <a name="ext_tdop_get_type_name"></a>EXT\_TDOP\_\_型\_名を取得します


EXT\_TDOP\_、 [**DEBUG\_要求**](debug-request-ext-typed-data-ansi.md)の\_型\_NAME サブ操作を取得し\_データ\_ANSI[**要求**](request.md)操作の型指定された型名を返します。データ.

**Parameters**

<span id="Operation"></span><span id="operation"></span><span id="OPERATION"></span>**運用**  
このサブ操作の\_名\_型を取得\_には、EXT\_TDOP を設定します。

<span id="InData"></span><span id="indata"></span><span id="INDATA"></span>**InData**  
型名が要求される型指定されたデータを指定します。

<span id="StrBufferIndex"></span><span id="strbufferindex"></span><span id="STRBUFFERINDEX"></span>**StrBufferIndex**  
型名を受け取ります。

<span id="StrBufferChars"></span><span id="strbufferchars"></span><span id="STRBUFFERCHARS"></span>**StrBufferChars**  
ANSI 文字列バッファーの**Strbufferindex**のサイズを文字数で指定します。

<span id="StrCharsNeeded"></span><span id="strcharsneeded"></span><span id="STRCHARSNEEDED"></span>**StrCharsNeeded**  
型名のサイズを文字数で受け取ります。

<span id="Status"></span><span id="status"></span><span id="STATUS"></span>**オンライン**  
このサブ操作によって返されたステータスコードを受け取ります。 これは、[**要求**](request.md)によって返される値と同じです。

<a name="remarks"></a>注釈
-------

EXT\_TDOP\_\_型の取得\_NAME は、 [**ext\_tdop**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdbgexts/ne-wdbgexts-_ext_tdop)列挙の値です。

このサブ操作のパラメーターは、 [**EXT\_型指定**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdbgexts/ns-wdbgexts-_ext_typed_data)された\_データ構造体のメンバーです。 前の Parameters セクションに記載されていない EXT\_\_型のメンバーは、このサブ操作では使用されず、0に設定する必要があります。 前の Parameters セクションのメンバーの説明では、メンバーがどのように使用されるかを指定します。 詳細については、「 **EXT\_型指定**された\_データ」を参照してください。

## <a name="span-idsee_alsospansee-also"></a><span id="see_also"></span>関連項目


[ **\_要求\_EXT\_型指定された\_データ\_ANSI**](debug-request-ext-typed-data-ansi.md)

[**EXT\_TDOP**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdbgexts/ne-wdbgexts-_ext_tdop)

[**EXT\_型指定された\_データ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdbgexts/ns-wdbgexts-_ext_typed_data)

[**申請**](request.md)

 

 







---
title: EXT\_TDOP\_HAS\_フィールド
description: EXT\_TDOP\_HAS\_、デバッグのフィールドのサブ操作\_要求\_EXT\_型指定された\_データ\_ANSI 要求操作は、構造体の場合を決定します。指定したメンバーが含まれています。
ms.assetid: c1486aff-63d3-4ceb-8dce-45a9c5835c99
keywords:
- デバッグ EXT_TDOP_HAS_FIELD Windows
topic_type:
- apiref
api_name:
- EXT_TDOP_HAS_FIELD
api_type:
- NA
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0a7e3106675bea09c22b34ad0d4e764469fc794f
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67366862"
---
# <a name="exttdophasfield"></a>EXT\_TDOP\_HAS\_フィールド


EXT\_TDOP\_HAS\_のサブ操作のフィールド、 [**デバッグ\_要求\_EXT\_型指定された\_データ\_ANSI**](debug-request-ext-typed-data-ansi.md) [**要求**](request.md)操作では、指定したメンバーが、構造に含まれるかどうかを判断します。

**Parameters**

<span id="Operation"></span><span id="operation"></span><span id="OPERATION"></span>**操作**  
EXT に設定\_TDOP\_HAS\_このサブ操作のフィールド。

<span id="InData"></span><span id="indata"></span><span id="INDATA"></span>**InData**  
メンバーの存在をチェックする型指定されたデータを指定します。 型指定されたデータが最初に、構造体のインスタンスを表すかどうかは、構造をチェックして、指定されたメンバーが含まれていないを確認するチェックします。

<span id="InStrIndex"></span><span id="instrindex"></span><span id="INSTRINDEX"></span>**InStrIndex**  
メンバーの名前を指定します。 名前はなどの下位メンバーを含めることができます、ドットで区切られたパス**mymember.mysubmember**します。 このドットで区切られたパス上のポインターを自動的に逆参照します。 ただし、ドット演算子 ( **.** ) 引き続き使用する必要がありますここで、通常の C ポインターではなく逆参照演算子 ( **-&gt;** )。

<span id="Status"></span><span id="status"></span><span id="STATUS"></span>**状態**  
このサブ操作によって返されるステータス コードを受け取ります。 これは、によって返される値と同じ[**要求**](request.md)します。

型指定されたデータには、メンバーが含まれている場合**状態**受信 S\_ok をクリックします。 型指定されたデータには、メンバーが含まれていない場合**状態**受信電子メール\_NOINTERFACE します。 その他のエラー値も返されます場合があります。

<a name="remarks"></a>注釈
-------

EXT\_TDOP\_HAS\_フィールドの値では、 [ **EXT\_TDOP** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdbgexts/ne-wdbgexts-_ext_tdop)列挙体。

このサブ操作のパラメーターのメンバーである、 [ **EXT\_型指定された\_データ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdbgexts/ns-wdbgexts-_ext_typed_data)構造体。 EXT のメンバー\_型指定された\_データは、前のパラメーター セクションには示されていないこのサブ操作では使用されませんし、0 に設定する必要があります。 前のパラメーター セクション内のメンバーの説明では、使用は、メンバーを指定します。 参照してください**EXT\_型指定された\_データ**の詳細。

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>参照してください。


[**デバッグ\_要求\_EXT\_型指定された\_データ\_ANSI**](debug-request-ext-typed-data-ansi.md)

[**EXT\_TDOP**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdbgexts/ne-wdbgexts-_ext_tdop)

[**EXT\_型指定された\_データ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdbgexts/ns-wdbgexts-_ext_typed_data)

[**要求**](request.md)

 

 







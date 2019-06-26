---
title: EXT\_TDOP\_取得\_配列\_要素
description: EXT\_TDOP\_取得\_配列\_、デバッグの要素のサブ操作\_要求\_EXT\_型指定された\_データ\_ANSI 要求操作配列から要素を返します。
ms.assetid: 67c87b14-3580-4507-884e-b02576ce7be2
keywords:
- デバッグ EXT_TDOP_GET_ARRAY_ELEMENT Windows
topic_type:
- apiref
api_name:
- EXT_TDOP_GET_ARRAY_ELEMENT
api_type:
- NA
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 17680fa1c11e7366b0b650ae7300f34a93fd3509
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67361362"
---
# <a name="exttdopgetarrayelement"></a>EXT\_TDOP\_取得\_配列\_要素


EXT\_TDOP\_取得\_配列\_の要素のサブ操作、 [**デバッグ\_要求\_EXT\_型指定された\_データ\_ANSI**](debug-request-ext-typed-data-ansi.md)[**要求**](request.md)操作では、配列の要素を返します。

**Parameters**

<span id="Operation"></span><span id="operation"></span><span id="OPERATION"></span>**操作**  
EXT に設定\_TDOP\_取得\_配列\_この操作のサブ要素です。

<span id="InData"></span><span id="indata"></span><span id="INDATA"></span>**InData**  
要素が要求されている配列を指定します。 **InData**ポインターを指定することもその場合、配列として扱われます。

<span id="OutData"></span><span id="outdata"></span><span id="OUTDATA"></span>**OutData**  
要求された要素を配列から受信します。

<span id="In64"></span><span id="in64"></span><span id="IN64"></span>**In64**  
配列内の要素のインデックスを指定します。

<span id="Status"></span><span id="status"></span><span id="STATUS"></span>**状態**  
このサブ操作によって返されるステータス コードを受け取ります。 これは、によって返される値と同じ[**要求**](request.md)します。

<a name="remarks"></a>注釈
-------

EXT\_TDOP\_取得\_配列\_要素では、 [ **EXT\_TDOP** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdbgexts/ne-wdbgexts-_ext_tdop)列挙体。

このサブ操作のパラメーターのメンバーである、 [ **EXT\_型指定された\_データ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdbgexts/ns-wdbgexts-_ext_typed_data)構造体。 EXT のメンバー\_型指定された\_データは、前のパラメーター セクションには示されていないこのサブ操作では使用されませんし、0 に設定する必要があります。 前のパラメーター セクション内のメンバーの説明では、使用は、メンバーを指定します。 参照してください**EXT\_型指定された\_データ**の詳細。

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>参照してください。


[**デバッグ\_要求\_EXT\_型指定された\_データ\_ANSI**](debug-request-ext-typed-data-ansi.md)

[**EXT\_TDOP**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdbgexts/ne-wdbgexts-_ext_tdop)

[**EXT\_型指定された\_データ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdbgexts/ns-wdbgexts-_ext_typed_data)

[**要求**](request.md)

 

 







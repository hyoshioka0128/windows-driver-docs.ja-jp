---
title: EXT\_TDOP\_取得\_型\_サイズ
description: EXT\_TDOP\_取得\_型\_、デバッグのサイズのサブ操作\_要求\_EXT\_型指定された\_データ\_ANSI 要求操作指定した型指定されたデータのサイズを返します。
ms.assetid: 3e668522-60bb-4abc-87b8-6b1beea573a3
keywords:
- デバッグ EXT_TDOP_GET_TYPE_SIZE Windows
topic_type:
- apiref
api_name:
- EXT_TDOP_GET_TYPE_SIZE
api_type:
- NA
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: e597ae980133db1e7b7904e252ac6706f289d6f9
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67361356"
---
# <a name="exttdopgettypesize"></a>EXT\_TDOP\_取得\_型\_サイズ


EXT\_TDOP\_取得\_型\_のサブ操作のサイズ、 [**デバッグ\_要求\_EXT\_型指定された\_データ\_ANSI**](debug-request-ext-typed-data-ansi.md)[**要求**](request.md)操作は、指定された型指定されたデータのサイズを返します。

**Parameters**

<span id="Operation"></span><span id="operation"></span><span id="OPERATION"></span>**操作**  
EXT に設定\_TDOP\_取得\_型\_このサブ操作のサイズ。

<span id="InData"></span><span id="indata"></span><span id="INDATA"></span>**InData**  
サイズが要求されている型指定されたデータを指定します。

<span id="Out32"></span><span id="out32"></span><span id="OUT32"></span>**Out32**  
型指定されたデータのバイト単位のサイズを受け取ります。

<span id="Status"></span><span id="status"></span><span id="STATUS"></span>**状態**  
このサブ操作によって返されるステータス コードを受け取ります。 これは、によって返される値と同じ[**要求**](request.md)します。

<a name="remarks"></a>注釈
-------

EXT\_TDOP\_取得\_型\_サイズは、値、 [ **EXT\_TDOP** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdbgexts/ne-wdbgexts-_ext_tdop)列挙体。

このサブ操作のパラメーターのメンバーである、 [ **EXT\_型指定された\_データ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdbgexts/ns-wdbgexts-_ext_typed_data)構造体。 EXT のメンバー\_型指定された\_データは、前のパラメーター セクションには示されていないこのサブ操作では使用されませんし、0 に設定する必要があります。 前のパラメーター セクション内のメンバーの説明では、使用は、メンバーを指定します。 参照してください**EXT\_型指定された\_データ**の詳細。

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>参照してください。


[**デバッグ\_要求\_EXT\_型指定された\_データ\_ANSI**](debug-request-ext-typed-data-ansi.md)

[**EXT\_TDOP**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdbgexts/ne-wdbgexts-_ext_tdop)

[**EXT\_型指定された\_データ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdbgexts/ns-wdbgexts-_ext_typed_data)

[**要求**](request.md)

 

 







---
title: EXT\_TDOP\_出力\_型\_名
description: EXT\_TDOP\_出力\_型\_、デバッグの名前のサブ操作\_要求\_EXT\_型指定された\_データ\_ANSI 要求操作指定した型指定されたデータの型名を出力します。
ms.assetid: eb0a9026-92fd-4b3e-b513-b691221b3196
keywords:
- デバッグ EXT_TDOP_OUTPUT_TYPE_NAME Windows
topic_type:
- apiref
api_name:
- EXT_TDOP_OUTPUT_TYPE_NAME
api_type:
- NA
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 11474fed4e918f34d393dee8f2362da59e2cd44a
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67366857"
---
# <a name="exttdopoutputtypename"></a>EXT\_TDOP\_出力\_型\_名


EXT\_TDOP\_出力\_型\_のサブ操作の名前、 [**デバッグ\_要求\_EXT\_型指定された\_データ\_ANSI**](debug-request-ext-typed-data-ansi.md)[**要求**](request.md)操作が指定した型指定されたデータの型名を出力します。

**Parameters**

<span id="Operation"></span><span id="operation"></span><span id="OPERATION"></span>**操作**  
EXT に設定\_TDOP\_出力\_型\_このサブ操作の名前。

<span id="InData"></span><span id="indata"></span><span id="INDATA"></span>**InData**  
型名を持つが印刷される型指定されたデータを指定します。

<span id="Status"></span><span id="status"></span><span id="STATUS"></span>**状態**  
このサブ操作によって返されるステータス コードを受け取ります。 これは、によって返される値と同じ[**要求**](request.md)します。

<a name="remarks"></a>注釈
-------

型名は、デバッガー エンジンの送信[コールバックを出力](https://docs.microsoft.com/windows-hardware/drivers/debugger/using-input-and-output#output-callbacks)します。

EXT\_TDOP\_出力\_型\_名は、値、 [ **EXT\_TDOP** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdbgexts/ne-wdbgexts-_ext_tdop)列挙体。

このサブ操作のパラメーターのメンバーである、 [ **EXT\_型指定された\_データ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdbgexts/ns-wdbgexts-_ext_typed_data)構造体。 EXT のメンバー\_型指定された\_データは、前のパラメーター セクションには示されていないこのサブ操作では使用されませんし、0 に設定する必要があります。 前のパラメーター セクション内のメンバーの説明では、使用は、メンバーを指定します。 参照してください**EXT\_型指定された\_データ**の詳細。

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>参照してください。


[**デバッグ\_要求\_EXT\_型指定された\_データ\_ANSI**](debug-request-ext-typed-data-ansi.md)

[**EXT\_TDOP**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdbgexts/ne-wdbgexts-_ext_tdop)

[**EXT\_型指定された\_データ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdbgexts/ns-wdbgexts-_ext_typed_data)

[**要求**](request.md)

 

 







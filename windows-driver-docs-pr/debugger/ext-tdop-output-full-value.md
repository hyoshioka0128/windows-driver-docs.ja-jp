---
title: EXT\_TDOP\_出力\_完全\_値
description: EXT\_TDOP\_出力\_完全\_、デバッグの値のサブ操作\_要求\_EXT\_型指定された\_データ\_ANSI 要求操作型と指定した型指定されたデータの値を出力します。
ms.assetid: d64f7a38-c9ae-412f-985b-22115d772116
keywords:
- デバッグ EXT_TDOP_OUTPUT_FULL_VALUE Windows
topic_type:
- apiref
api_name:
- EXT_TDOP_OUTPUT_FULL_VALUE
api_type:
- NA
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0efb4746472cb14035e6ad06ca607d46776aca71
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67361340"
---
# <a name="exttdopoutputfullvalue"></a>EXT\_TDOP\_出力\_完全\_値


EXT\_TDOP\_出力\_完全\_のサブ操作の値、 [**デバッグ\_要求\_EXT\_型指定された\_データ\_ANSI**](debug-request-ext-typed-data-ansi.md)[**要求**](request.md)操作の種類と指定した型指定されたデータの値を出力します。

**Parameters**

<span id="Operation"></span><span id="operation"></span><span id="OPERATION"></span>**操作**  
EXT に設定\_TDOP\_出力\_完全\_このサブ操作の値。

<span id="InData"></span><span id="indata"></span><span id="INDATA"></span>**InData**  
印刷される型の名前と値の型指定されたデータを指定します。

<span id="Status"></span><span id="status"></span><span id="STATUS"></span>**状態**  
このサブ操作によって返されるステータス コードを受け取ります。 これは、によって返される値と同じ[**要求**](request.md)します。

<a name="remarks"></a>注釈
-------

型名と書式設定された値は、デバッガー エンジンの送信[コールバックを出力](https://docs.microsoft.com/windows-hardware/drivers/debugger/using-input-and-output#output-callbacks)します。 EXT\_TDOP\_出力\_完全\_値より値の詳細情報を出力する[ **EXT\_TDOP\_出力\_単純な\_値**](ext-tdop-output-simple-value.md)します。 たとえば、ポインターが逆参照しをポイントしている値を出力もします。

EXT\_TDOP\_出力\_完全\_値値では、 [ **EXT\_TDOP** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdbgexts/ne-wdbgexts-_ext_tdop)列挙体。

このサブ操作のパラメーターのメンバーである、 [ **EXT\_型指定された\_データ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdbgexts/ns-wdbgexts-_ext_typed_data)構造体。 EXT のメンバー\_型指定された\_データは、前のパラメーター セクションには示されていないこのサブ操作では使用されませんし、0 に設定する必要があります。 前のパラメーター セクション内のメンバーの説明では、使用は、メンバーを指定します。 参照してください**EXT\_型指定された\_データ**の詳細。

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>参照してください。


[**デバッグ\_要求\_EXT\_型指定された\_データ\_ANSI**](debug-request-ext-typed-data-ansi.md)

[**EXT\_TDOP**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdbgexts/ne-wdbgexts-_ext_tdop)

[**EXT\_型指定された\_データ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdbgexts/ns-wdbgexts-_ext_typed_data)

[**要求**](request.md)

 

 







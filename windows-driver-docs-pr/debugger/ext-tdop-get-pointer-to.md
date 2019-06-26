---
title: EXT\_TDOP\_取得\_ポインター\_TO
description: EXT\_TDOP\_取得\_ポインター\_、デバッグのサブ操作に\_要求\_EXT\_型指定された\_データ\_ANSI 要求操作指定された型指定されたデータへのポインターを表す新しい型指定されたデータの説明を返します。
ms.assetid: 05db8e07-b94f-4cf3-b01b-a918b737ecf4
keywords:
- デバッグ EXT_TDOP_GET_POINTER_TO Windows
topic_type:
- apiref
api_name:
- EXT_TDOP_GET_POINTER_TO
api_type:
- NA
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 54e0f9f4353649dc76a6ec9412fa658ce3b04fa4
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67361345"
---
# <a name="exttdopgetpointerto"></a>EXT\_TDOP\_取得\_ポインター\_TO


EXT\_TDOP\_取得\_ポインター\_のサブ操作に、 [**デバッグ\_要求\_EXT\_型指定された\_データ\_ANSI**](debug-request-ext-typed-data-ansi.md)[**要求**](request.md)操作は、指定された型指定されたデータへのポインターを表す新しい型指定されたデータの説明を返します。

**Parameters**

<span id="Operation"></span><span id="operation"></span><span id="OPERATION"></span>**操作**  
EXT に設定\_TDOP\_取得\_ポインター\_このサブ操作にします。

<span id="InData"></span><span id="indata"></span><span id="INDATA"></span>**InData**  
ポインターが返される元の型指定されたデータの説明を指定します。

<span id="OutData"></span><span id="outdata"></span><span id="OUTDATA"></span>**OutData**  
指定された型指定されたデータへのポインターを表す名前の型指定されたデータを受け取る**InData**します。

<span id="Status"></span><span id="status"></span><span id="STATUS"></span>**状態**  
このサブ操作によって返されるステータス コードを受け取ります。 これは、によって返される値と同じ[**要求**](request.md)します。

<a name="remarks"></a>注釈
-------

EXT\_TDOP\_取得\_ポインター\_には、値、 [ **EXT\_TDOP** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdbgexts/ne-wdbgexts-_ext_tdop)列挙体。

このサブ操作のパラメーターのメンバーである、 [ **EXT\_型指定された\_データ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdbgexts/ns-wdbgexts-_ext_typed_data)構造体。 EXT のメンバー\_型指定された\_データは、前のパラメーター セクションには示されていないこのサブ操作では使用されませんし、0 に設定する必要があります。 前のパラメーター セクション内のメンバーの説明では、使用は、メンバーを指定します。 参照してください**EXT\_型指定された\_データ**の詳細。

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>参照してください。


[**デバッグ\_要求\_EXT\_型指定された\_データ\_ANSI**](debug-request-ext-typed-data-ansi.md)

[**EXT\_TDOP**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdbgexts/ne-wdbgexts-_ext_tdop)

[**EXT\_型指定された\_データ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdbgexts/ns-wdbgexts-_ext_typed_data)

[**要求**](request.md)

 

 







---
title: EXT\_TDOP\_設定\_FROM\_U64\_EXPR
description: EXT\_TDOP\_設定\_FROM\_U64\_デバッグ EXPR サブ操作\_要求\_EXT\_型指定された\_データ\_ANSIRequest 操作では、式の値を表す型指定されたデータの説明を返します。
ms.assetid: 3d0007f8-09c7-4333-a1f0-090918c9f8fa
keywords:
- デバッグ EXT_TDOP_SET_FROM_U64_EXPR Windows
topic_type:
- apiref
api_name:
- EXT_TDOP_SET_FROM_U64_EXPR
api_type:
- NA
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 16179a5686ed6e0cdc1d086784ad3b0dfb0cfb9e
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67366838"
---
# <a name="exttdopsetfromu64expr"></a>EXT\_TDOP\_設定\_FROM\_U64\_EXPR


EXT\_TDOP\_設定\_FROM\_U64\_の EXPR サブ操作、 [**デバッグ\_要求\_EXT\_型指定されました。\_データ\_ANSI**](debug-request-ext-typed-data-ansi.md)[**要求**](request.md)操作は、式の値を表す型指定されたデータの説明を返します。

<span id="Operation"></span><span id="operation"></span><span id="OPERATION"></span>**操作**  
EXT に設定\_TDOP\_設定\_FROM\_U64\_EXPR このサブ操作。

<span id="Flags"></span><span id="flags"></span><span id="FLAGS"></span>**フラグ**  
式の値が存在するターゲットのメモリを記述するビット フラグを指定します。 参照してください[ **EXT\_型指定された\_データ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdbgexts/ns-wdbgexts-_ext_typed_data)これらのフラグの詳細についてはします。

<span id="InData"></span><span id="indata"></span><span id="INDATA"></span>**InData**  
によって指定された式で、ターゲットのメモリ内アドレスを持つことができます、省略可能な型指定されたデータを指定します。 **InStrIndex**します。 このアドレスは、擬似レジスタとして式で使用 **$extin**します。

<span id="OutData"></span><span id="outdata"></span><span id="OUTDATA"></span>**OutData**  
受信、 [**デバッグ\_型指定された\_データ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdbgexts/ns-wdbgexts-_debug_typed_data)式の値を表す構造体です。

<span id="InStrIndex"></span><span id="instrindex"></span><span id="INSTRINDEX"></span>**InStrIndex**  
評価する式を指定します。 この式は、既定の式エバリュエーターによって評価されます。

<span id="Status"></span><span id="status"></span><span id="STATUS"></span>**状態**  
このサブ操作によって返されるステータス コードを受け取ります。 これは、によって返される値と同じ[**要求**](request.md)します。

<a name="remarks"></a>注釈
-------

EXT\_TDOP\_設定\_FROM\_U64\_EXPR の値、 [ **EXT\_TDOP** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdbgexts/ne-wdbgexts-_ext_tdop)列挙体。

このサブ操作のパラメーターのメンバーである、 [ **EXT\_型指定された\_データ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdbgexts/ns-wdbgexts-_ext_typed_data)構造体。 EXT のメンバー\_型指定された\_データは、前のパラメーター セクションには示されていないこのサブ操作では使用されませんし、0 に設定する必要があります。 前のパラメーター セクション内のメンバーの説明では、使用は、メンバーを指定します。 参照してください**EXT\_型指定された\_データ**の詳細。

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>参照してください。


[**デバッグ\_要求\_EXT\_型指定された\_データ\_ANSI**](debug-request-ext-typed-data-ansi.md)

[**EXT\_TDOP**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdbgexts/ne-wdbgexts-_ext_tdop)

[**EXT\_型指定された\_データ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdbgexts/ns-wdbgexts-_ext_typed_data)

[**要求**](request.md)

 

 







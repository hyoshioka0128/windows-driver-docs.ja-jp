---
title: EXT\_TDOP\_\_EXPR から\_を設定します
description: EXT\_TDOP\_、デバッグ\_要求の\_EXPR サブ操作から\_設定されます。 ANSI 要求操作では、型指定されたデータの説明が返されます。条件.
ms.assetid: 51d5884e-da7f-4bce-ba49-12500208d117
keywords:
- EXT_TDOP_SET_FROM_EXPR Windows のデバッグ
topic_type:
- apiref
api_name:
- EXT_TDOP_SET_FROM_EXPR
api_type:
- NA
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: b5437c56be9474cb1f78ddc6cf9936dc98da39db
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838759"
---
# <a name="ext_tdop_set_from_expr"></a>EXT\_TDOP\_\_EXPR から\_を設定します


EXT\_TDOP\_、デバッグ\_要求の\_EXPR サブ操作から\_設定されています\_[**データ\_ANSI**](debug-request-ext-typed-data-ansi.md)[**要求**](request.md)操作では、型指定されたデータの説明が返されます。式の値を表します。

**Parameters**

<span id="Operation"></span><span id="operation"></span><span id="OPERATION"></span>**運用**  
このサブ操作の\_EXPR から\_を設定\_には、EXT\_TDOP を設定します。

<span id="Flags"></span><span id="flags"></span><span id="FLAGS"></span>**示す**  
式の値が存在するターゲットのメモリを示すビットフラグを指定します。 これらのフラグの詳細については、「 [**EXT\_型指定**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdbgexts/ns-wdbgexts-_ext_typed_data)された\_データ」を参照してください。

<span id="OutData"></span><span id="outdata"></span><span id="OUTDATA"></span>**OutData**  
式の値を表す、型指定された[ **\_\_データ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdbgexts/ns-wdbgexts-_debug_typed_data)構造体を受け取ります。

<span id="InStrIndex"></span><span id="instrindex"></span><span id="INSTRINDEX"></span>**InStrIndex**  
評価する式を指定します。 この式は、既定の式エバリュエーターによって評価されます。

<span id="Status"></span><span id="status"></span><span id="STATUS"></span>**オンライン**  
このサブ操作によって返されたステータスコードを受け取ります。 これは、[**要求**](request.md)によって返される値と同じです。

<a name="remarks"></a>注釈
-------

EXT\_TDOP\_SET\_は\_EXPR から[**ext\_tdop**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdbgexts/ne-wdbgexts-_ext_tdop)列挙の値です。

このサブ操作のパラメーターは、 [**EXT\_型指定**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdbgexts/ns-wdbgexts-_ext_typed_data)された\_データ構造体のメンバーです。 前の Parameters セクションに記載されていない EXT\_\_型のメンバーは、このサブ操作では使用されず、0に設定する必要があります。 前の Parameters セクションのメンバーの説明では、メンバーがどのように使用されるかを指定します。 詳細については、「 **EXT\_型指定**された\_データ」を参照してください。

## <a name="span-idsee_alsospansee-also"></a><span id="see_also"></span>関連項目


[ **\_要求\_EXT\_型指定された\_データ\_ANSI**](debug-request-ext-typed-data-ansi.md)

[**EXT\_TDOP**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdbgexts/ne-wdbgexts-_ext_tdop)

[**EXT\_型指定された\_データ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdbgexts/ns-wdbgexts-_ext_typed_data)

[**申請**](request.md)

 

 







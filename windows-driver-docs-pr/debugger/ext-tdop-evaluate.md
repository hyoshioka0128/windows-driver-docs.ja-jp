---
title: EXT\_TDOP\_評価
description: EXT\_TDOP\_、型指定された\_データ\_\_EXT\_の\_要求のサブ操作を評価します。 ANSI 要求操作は、式の値を表す型指定されたデータの説明を返します。
ms.assetid: 2df6cf92-6889-4407-93c0-4c777a68cbc8
keywords:
- EXT_TDOP_EVALUATE Windows のデバッグ
topic_type:
- apiref
api_name:
- EXT_TDOP_EVALUATE
api_type:
- NA
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: a51949a330074584b59d5254e5d27b0a4f9187fa
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72826530"
---
# <a name="ext_tdop_evaluate"></a>EXT\_TDOP\_評価


EXT\_TDOP\_DEBUG\_要求のサブ操作を評価[ **\_ext\_型指定された\_データ\_ANSI**](debug-request-ext-typed-data-ansi.md)[**要求**](request.md)操作は、の値を表す型指定されたデータの説明を返します。条件.

**Parameters**

<span id="Operation"></span><span id="operation"></span><span id="OPERATION"></span>**運用**  
このサブ操作に対して\_を評価するには、EXT\_TDOP に設定します。

<span id="Flags"></span><span id="flags"></span><span id="FLAGS"></span>**示す**  
式の値が存在するターゲットのメモリを示すビットフラグを指定します。 これらのフラグの詳細については、「 [**EXT\_型指定**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdbgexts/ns-wdbgexts-_ext_typed_data)された\_データ」を参照してください。

<span id="InData"></span><span id="indata"></span><span id="INDATA"></span>**InData**  
**InStrIndex**で指定された式で使用できる値を持つ、省略可能な型指定されたデータを指定します。 この値は、擬似レジスタ **$extin**として式によって使用されます。

<span id="OutData"></span><span id="outdata"></span><span id="OUTDATA"></span>**OutData**  
式の値を表す、型指定された[ **\_\_データ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdbgexts/ns-wdbgexts-_debug_typed_data)構造体を受け取ります。

<span id="InStrIndex"></span><span id="instrindex"></span><span id="INSTRINDEX"></span>**InStrIndex**  
評価する式を指定します。 この式は、既定の式エバリュエーターによって評価されます。

<span id="Status"></span><span id="status"></span><span id="STATUS"></span>**オンライン**  
このサブ操作によって返されたステータスコードを受け取ります。 これは、[**要求**](request.md)によって返される値と同じです。

<a name="remarks"></a>注釈
-------

EXT\_TDOP\_EVALUATE は、 [**ext\_tdop**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdbgexts/ne-wdbgexts-_ext_tdop)列挙体の値です。

このサブ操作のパラメーターは、 [**EXT\_型指定**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdbgexts/ns-wdbgexts-_ext_typed_data)された\_データ構造体のメンバーです。 前の Parameters セクションに記載されていない EXT\_\_型のメンバーは、このサブ操作では使用されず、0に設定する必要があります。 前の Parameters セクションのメンバーの説明では、メンバーがどのように使用されるかを指定します。 詳細については、「 **EXT\_型指定**された\_データ」を参照してください。

## <a name="span-idsee_alsospansee-also"></a><span id="see_also"></span>関連項目


[ **\_要求\_EXT\_型指定された\_データ\_ANSI**](debug-request-ext-typed-data-ansi.md)

[**EXT\_TDOP**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdbgexts/ne-wdbgexts-_ext_tdop)

[**EXT\_型指定された\_データ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdbgexts/ns-wdbgexts-_ext_typed_data)

[**申請**](request.md)

 

 







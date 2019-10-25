---
title: EXT\_TDOP\_リリース
description: EXT\_TDOP\_、型指定された\_データ\_データ\_ANSI 要求操作のデバッグ\_\_要求のサブ操作を解放すると、型指定されたデータの記述が解放されます。
ms.assetid: 4c2bbc65-a98d-4ee7-bbd0-e30b33c330e0
keywords:
- EXT_TDOP_RELEASE Windows のデバッグ
topic_type:
- apiref
api_name:
- EXT_TDOP_RELEASE
api_type:
- NA
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: ba47443e5432dac224dc7bb9458d2b6f3bf059e5
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838764"
---
# <a name="ext_tdop_release"></a>EXT\_TDOP\_リリース


EXT\_TDOP\_、型指定された\_データ\_データ\_ANSI[**要求**](request.md)操作の[**デバッグ\_\_要求**](debug-request-ext-typed-data-ansi.md)のサブ操作を解放すると、型指定されたデータの記述が解放されます。

**パラメーター**

<span id="Operation"></span><span id="operation"></span><span id="OPERATION"></span>**運用**  
このサブ操作では、EXT\_TDOP\_RELEASE に設定されています。

<span id="InData"></span><span id="indata"></span><span id="INDATA"></span>**InData**  
解放する[**データ構造\_型**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdbgexts/ns-wdbgexts-_debug_typed_data)指定されたデバッグ\_のインスタンスを指定します。

<span id="Status"></span><span id="status"></span><span id="STATUS"></span>**オンライン**  
このサブ操作によって返されたステータスコードを受け取ります。 これは、[**要求**](request.md)によって返される値と同じです。

<a name="remarks"></a>解説
-------

EXT\_TDOP\_RELEASE は、 [**ext\_tdop**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdbgexts/ne-wdbgexts-_ext_tdop)列挙体の値です。

このサブ操作のパラメーターは、 [**EXT\_型指定**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdbgexts/ns-wdbgexts-_ext_typed_data)された\_データ構造体のメンバーです。 前の Parameters セクションに記載されていない EXT\_\_型のメンバーは、このサブ操作では使用されず、0に設定する必要があります。 前のパラメーターセクションのメンバーの説明では、この特定の設定のメンバーの目的だけを指定しています。 詳細については、「 **EXT\_型指定**された\_データ」を参照してください。

## <a name="span-idsee_alsospansee-also"></a><span id="see_also"></span>関連項目


[ **\_要求\_EXT\_型指定された\_データ\_ANSI**](debug-request-ext-typed-data-ansi.md)

[**EXT\_TDOP**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdbgexts/ne-wdbgexts-_ext_tdop)

[**EXT\_型指定された\_データ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdbgexts/ns-wdbgexts-_ext_typed_data)

[**Request**](request.md)

 

 







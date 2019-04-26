---
title: EXT\_TDOP\_取得\_逆参照
description: EXT\_TDOP\_取得\_、デバッグのサブ操作の逆参照\_要求\_EXT\_型指定された\_データ\_ANSI 要求操作を逆参照、ポインターが指す値を返します。
ms.assetid: 0b5eed03-4241-4038-8950-12c82c2d086f
keywords:
- デバッグ EXT_TDOP_GET_DEREFERENCE Windows
topic_type:
- apiref
api_name:
- EXT_TDOP_GET_DEREFERENCE
api_type:
- NA
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 66e9248162924096c157cb55e3a2cf359210a05d
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63341695"
---
# <a name="exttdopgetdereference"></a>EXT\_TDOP\_取得\_逆参照


EXT\_TDOP\_取得\_のサブ操作の逆参照、 [**デバッグ\_要求\_EXT\_型指定された\_データ\_ANSI** ](debug-request-ext-typed-data-ansi.md) [**要求**](request.md)操作、ポインターを逆参照し、指す値を返します。

**Parameters**

<span id="Operation"></span><span id="operation"></span><span id="OPERATION"></span>**操作**  
EXT に設定\_TDOP\_取得\_このサブ操作の逆参照します。

<span id="InData"></span><span id="indata"></span><span id="INDATA"></span>**InData**  
逆参照へのポインターを指定します。 **InData**場合、配列の最初の要素が返される配列の指定もできます。

<span id="OutData"></span><span id="outdata"></span><span id="OUTDATA"></span>**OutData**  
指す値を受け取ります。

<span id="Status"></span><span id="status"></span><span id="STATUS"></span>**状態**  
このサブ操作によって返されるステータス コードを受け取ります。 これは、によって返される値と同じ[**要求**](request.md)します。

<a name="remarks"></a>注釈
-------

EXT\_TDOP\_取得\_逆参照は、値、 [ **EXT\_TDOP** ](https://msdn.microsoft.com/library/windows/hardware/ff544529)列挙体。

このサブ操作のパラメーターのメンバーである、 [ **EXT\_型指定された\_データ**](https://msdn.microsoft.com/library/windows/hardware/ff545306)構造体。 EXT のメンバー\_型指定された\_データは、前のパラメーター セクションには示されていないこのサブ操作では使用されませんし、0 に設定する必要があります。 前のパラメーター セクション内のメンバーの説明では、使用は、メンバーを指定します。 参照してください**EXT\_型指定された\_データ**の詳細。

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>参照してください。


[**デバッグ\_要求\_EXT\_型指定された\_データ\_ANSI**](debug-request-ext-typed-data-ansi.md)

[**EXT\_TDOP**](https://msdn.microsoft.com/library/windows/hardware/ff544529)

[**EXT\_型指定された\_データ**](https://msdn.microsoft.com/library/windows/hardware/ff545306)

[**要求**](request.md)

 

 







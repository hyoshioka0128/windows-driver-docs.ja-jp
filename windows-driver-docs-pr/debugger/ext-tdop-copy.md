---
title: EXT\_TDOP\_コピー
description: EXT\_TDOP\_、デバッグのコピーのサブ操作\_要求\_EXT\_型指定された\_データ\_ANSI 要求操作は、型指定されたデータの説明のコピーを作成します。
ms.assetid: 2de920de-db93-408d-8e80-a29c4e2930a0
keywords:
- デバッグ EXT_TDOP_COPY Windows
topic_type:
- apiref
api_name:
- EXT_TDOP_COPY
api_type:
- NA
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6d55cee518a69ad1ea1ef6e2cf9f2b405ceddf8b
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63379739"
---
# <a name="exttdopcopy"></a>EXT\_TDOP\_コピー


EXT\_TDOP\_のサブ操作のコピー、 [**デバッグ\_要求\_EXT\_型指定された\_データ\_ANSI** ](debug-request-ext-typed-data-ansi.md)[**要求**](request.md)操作は、型指定されたデータの説明のコピーを作成します。

**Parameters**

<span id="Operation"></span><span id="operation"></span><span id="OPERATION"></span>**操作**  
EXT に設定\_TDOP\_このサブ操作のコピーします。

<span id="InData"></span><span id="indata"></span><span id="INDATA"></span>**InData**  
元のインスタンスを指定します、 [**デバッグ\_型指定された\_データ**](https://msdn.microsoft.com/library/windows/hardware/ff541706)構造体。

<span id="OutData"></span><span id="outdata"></span><span id="OUTDATA"></span>**OutData**  
インスタンスのコピーを受け取る、 [**デバッグ\_型指定された\_データ**](https://msdn.microsoft.com/library/windows/hardware/ff541706)構造体で指定された**InData**します。

<span id="Status"></span><span id="status"></span><span id="STATUS"></span>**状態**  
このサブ操作によって返されるステータス コードを受け取ります。 これは、によって返される値と同じ[**要求**](request.md)します。

<a name="remarks"></a>注釈
-------

EXT\_TDOP\_コピーがの値、 [ **EXT\_TDOP** ](https://msdn.microsoft.com/library/windows/hardware/ff544529)列挙体。

このサブ操作のパラメーターのメンバーである、 [ **EXT\_型指定された\_データ**](https://msdn.microsoft.com/library/windows/hardware/ff545306)構造体。 EXT のメンバー\_型指定された\_データは、前のパラメーター セクションには示されていないこのサブ操作では使用されませんし、0 に設定する必要があります。 前のパラメーター セクション内のメンバーの説明では、使用は、メンバーを指定します。 メンバーの詳細については、次を参照してください。 **EXT\_型指定された\_データ**します。

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>参照してください。


[**デバッグ\_要求\_EXT\_型指定された\_データ\_ANSI**](debug-request-ext-typed-data-ansi.md)

[**EXT\_TDOP**](https://msdn.microsoft.com/library/windows/hardware/ff544529)

[**EXT\_型指定された\_データ**](https://msdn.microsoft.com/library/windows/hardware/ff545306)

[**要求**](request.md)

 

 







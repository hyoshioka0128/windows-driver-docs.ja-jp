---
title: EXT\_TDOP\_リリース
description: EXT\_TDOP\_、デバッグのリリースのサブ操作\_要求\_EXT\_型指定された\_データ\_ANSI 要求操作は、型指定されたデータの説明を解放します。
ms.assetid: 4c2bbc65-a98d-4ee7-bbd0-e30b33c330e0
keywords:
- デバッグ EXT_TDOP_RELEASE Windows
topic_type:
- apiref
api_name:
- EXT_TDOP_RELEASE
api_type:
- NA
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 70389f57b224b26e87464c79766a170f65bc1f37
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63367262"
---
# <a name="exttdoprelease"></a>EXT\_TDOP\_リリース


EXT\_TDOP\_のリリースのサブ操作、 [**デバッグ\_要求\_EXT\_型指定された\_データ\_ANSI** ](debug-request-ext-typed-data-ansi.md)[**要求**](request.md)操作は、型指定されたデータの説明を解放します。

**Parameters**

<span id="Operation"></span><span id="operation"></span><span id="OPERATION"></span>**操作**  
EXT に設定\_TDOP\_このサブ操作用のリリース。

<span id="InData"></span><span id="indata"></span><span id="INDATA"></span>**InData**  
インスタンスを指定します、 [**デバッグ\_型指定された\_データ**](https://msdn.microsoft.com/library/windows/hardware/ff541706)構造体を解放します。

<span id="Status"></span><span id="status"></span><span id="STATUS"></span>**状態**  
このサブ操作によって返されるステータス コードを受け取ります。 これは、によって返される値と同じ[**要求**](request.md)します。

<a name="remarks"></a>注釈
-------

EXT\_TDOP\_リリースは、値、 [ **EXT\_TDOP** ](https://msdn.microsoft.com/library/windows/hardware/ff544529)列挙体。

このサブ操作のパラメーターのメンバーである、 [ **EXT\_型指定された\_データ**](https://msdn.microsoft.com/library/windows/hardware/ff545306)構造体。 EXT のメンバー\_型指定された\_データは、前のパラメーター セクションには示されていないこのサブ操作では使用されませんし、0 に設定する必要があります。 前のパラメーター セクション内のメンバーの説明では、この特定の設定で、メンバーの目的のみを指定します。 参照してください**EXT\_型指定された\_データ**の詳細。

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>参照してください。


[**デバッグ\_要求\_EXT\_型指定された\_データ\_ANSI**](debug-request-ext-typed-data-ansi.md)

[**EXT\_TDOP**](https://msdn.microsoft.com/library/windows/hardware/ff544529)

[**EXT\_型指定された\_データ**](https://msdn.microsoft.com/library/windows/hardware/ff545306)

[**要求**](request.md)

 

 







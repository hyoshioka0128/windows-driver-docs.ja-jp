---
title: EXT\_TDOP\_取得\_型\_名
description: EXT\_TDOP\_取得\_型\_、デバッグの名前のサブ操作\_要求\_EXT\_型指定された\_データ\_ANSI 要求操作指定した型指定されたデータの型名を返します。
ms.assetid: ce896ded-a49e-4f89-969e-6d464e583ca8
keywords:
- デバッグ EXT_TDOP_GET_TYPE_NAME Windows
topic_type:
- apiref
api_name:
- EXT_TDOP_GET_TYPE_NAME
api_type:
- NA
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 132d5a92956d3fed4dd25e0b7a4c8e10688c3ab0
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63379893"
---
# <a name="exttdopgettypename"></a>EXT\_TDOP\_取得\_型\_名


EXT\_TDOP\_取得\_型\_のサブ操作の名前、 [**デバッグ\_要求\_EXT\_型指定された\_データ\_ANSI**](debug-request-ext-typed-data-ansi.md)[**要求**](request.md)操作は、指定した型指定されたデータの型名を返します。

**Parameters**

<span id="Operation"></span><span id="operation"></span><span id="OPERATION"></span>**操作**  
EXT に設定\_TDOP\_取得\_型\_このサブ操作の名前。

<span id="InData"></span><span id="indata"></span><span id="INDATA"></span>**InData**  
型名を持つが要求されている型指定されたデータを指定します。

<span id="StrBufferIndex"></span><span id="strbufferindex"></span><span id="STRBUFFERINDEX"></span>**StrBufferIndex**  
型名を受け取ります。

<span id="StrBufferChars"></span><span id="strbufferchars"></span><span id="STRBUFFERCHARS"></span>**StrBufferChars**  
文字の ANSI 文字列バッファーのサイズを指定**StrBufferIndex**します。

<span id="StrCharsNeeded"></span><span id="strcharsneeded"></span><span id="STRCHARSNEEDED"></span>**StrCharsNeeded**  
型名の文字のサイズを受け取ります。

<span id="Status"></span><span id="status"></span><span id="STATUS"></span>**状態**  
このサブ操作によって返されるステータス コードを受け取ります。 これは、によって返される値と同じ[**要求**](request.md)します。

<a name="remarks"></a>注釈
-------

EXT\_TDOP\_取得\_型\_名は、値、 [ **EXT\_TDOP** ](https://msdn.microsoft.com/library/windows/hardware/ff544529)列挙体。

このサブ操作のパラメーターのメンバーである、 [ **EXT\_型指定された\_データ**](https://msdn.microsoft.com/library/windows/hardware/ff545306)構造体。 EXT のメンバー\_型指定された\_データは、前のパラメーター セクションには示されていないこのサブ操作では使用されませんし、0 に設定する必要があります。 前のパラメーター セクション内のメンバーの説明では、使用は、メンバーを指定します。 参照してください**EXT\_型指定された\_データ**の詳細。

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>参照してください。


[**デバッグ\_要求\_EXT\_型指定された\_データ\_ANSI**](debug-request-ext-typed-data-ansi.md)

[**EXT\_TDOP**](https://msdn.microsoft.com/library/windows/hardware/ff544529)

[**EXT\_型指定された\_データ**](https://msdn.microsoft.com/library/windows/hardware/ff545306)

[**要求**](request.md)

 

 







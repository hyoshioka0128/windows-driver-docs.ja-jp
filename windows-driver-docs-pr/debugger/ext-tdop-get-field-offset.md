---
title: EXT\_TDOP\_取得\_フィールド\_オフセット
description: EXT\_TDOP\_取得\_フィールド\_、デバッグのサブ操作のオフセット\_要求\_EXT\_型指定された\_データ\_ANSI 要求操作構造体のメンバーのオフセットを返します。
ms.assetid: 2703d518-1bc3-42a2-9a22-f9ea88a12c05
keywords:
- デバッグ EXT_TDOP_GET_FIELD_OFFSET Windows
topic_type:
- apiref
api_name:
- EXT_TDOP_GET_FIELD_OFFSET
api_type:
- NA
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0ebab86ea70bb2113b54aef97325acebe554eeec
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56529570"
---
# <a name="exttdopgetfieldoffset"></a>EXT\_TDOP\_取得\_フィールド\_オフセット


EXT\_TDOP\_取得\_フィールド\_のサブ操作のオフセット、 [**デバッグ\_要求\_EXT\_型指定された\_データ\_ANSI**](debug-request-ext-typed-data-ansi.md)[**要求**](request.md)操作は、構造内のメンバーのオフセットを返します。

**パラメーター**

<span id="Operation"></span><span id="operation"></span><span id="OPERATION"></span>**操作**  
EXT に設定\_TDOP\_取得\_フィールド\_このサブ操作のオフセットします。

<span id="InData"></span><span id="indata"></span><span id="INDATA"></span>**InData**  
オフセットが要求されているメンバーを格納する構造体のインスタンスを表す、型指定されたデータを指定します。

<span id="InStrIndex"></span><span id="instrindex"></span><span id="INSTRINDEX"></span>**InStrIndex**  
オフセットが要求されているメンバーの名前を指定します。 名前は、ドットで区切られたパスし、サブ メンバーを含めることができます。 たとえば、 **mymember.mysubmember**します。 このドットで区切られたパス上のポインターを自動的に逆参照します。 ただし、ドット演算子 (**.**) 引き続き使用する必要がありますここで、通常の C ポインターではなく逆参照演算子 (**-&gt;**)。

<span id="Out32"></span><span id="out32"></span><span id="OUT32"></span>**Out32**  
構造体のインスタンス内のメンバーのオフセットを受け取ります。 これは、構造体のインスタンスの先頭とメンバー間のバイト数です。

<span id="Status"></span><span id="status"></span><span id="STATUS"></span>**状態**  
このサブ操作によって返されるステータス コードを受け取ります。 これは、によって返される値と同じ[**要求**](request.md)します。

<a name="remarks"></a>注釈
-------

EXT\_TDOP\_取得\_フィールド\_オフセットの値は、 [ **EXT\_TDOP** ](https://msdn.microsoft.com/library/windows/hardware/ff544529)列挙体。

このサブ操作のパラメーターのメンバーである、 [ **EXT\_型指定された\_データ**](https://msdn.microsoft.com/library/windows/hardware/ff545306)構造体。 EXT のメンバー\_型指定された\_データは、前のパラメーター セクションには示されていないこのサブ操作では使用されませんし、0 に設定する必要があります。 前のパラメーター セクション内のメンバーの説明では、使用は、メンバーを指定します。 参照してください**EXT\_型指定された\_データ**の詳細。

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>参照してください。


[**デバッグ\_要求\_EXT\_型指定された\_データ\_ANSI**](debug-request-ext-typed-data-ansi.md)

[**EXT\_TDOP**](https://msdn.microsoft.com/library/windows/hardware/ff544529)

[**EXT\_型指定された\_データ**](https://msdn.microsoft.com/library/windows/hardware/ff545306)

[**要求**](request.md)

 

 







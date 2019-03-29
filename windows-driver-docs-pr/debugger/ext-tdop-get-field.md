---
title: EXT\_TDOP\_取得\_フィールド
description: EXT\_TDOP\_取得\_、デバッグのフィールドのサブ操作\_要求\_EXT\_型指定された\_データ\_ANSI 要求の操作は、型指定されたデータを返します。指定された構造体のメンバーを表す説明します。
ms.assetid: c91c0ecf-c093-4585-a6b5-6bda91899ec3
keywords:
- デバッグ EXT_TDOP_GET_FIELD Windows
topic_type:
- apiref
api_name:
- EXT_TDOP_GET_FIELD
api_type:
- NA
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: d15a0fd165d1756353143385f5922148a7664b75
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56578531"
---
# <a name="exttdopgetfield"></a>EXT\_TDOP\_取得\_フィールド


EXT\_TDOP\_取得\_のサブ操作のフィールド、 [**デバッグ\_要求\_EXT\_型指定された\_データ\_ANSI**](debug-request-ext-typed-data-ansi.md) [**要求**](request.md)操作は、特定の構造体のメンバーを表す型指定されたデータの説明を返します。

**Parameters**

<span id="Operation"></span><span id="operation"></span><span id="OPERATION"></span>**操作**  
EXT に設定\_TDOP\_取得\_このサブ操作のフィールド。

<span id="InData"></span><span id="indata"></span><span id="INDATA"></span>**InData**  
インスタンスを指定します[**デバッグ\_型指定された\_データ**](https://msdn.microsoft.com/library/windows/hardware/ff541706)そのメンバーが必要な構造を記述します。

<span id="OutData"></span><span id="outdata"></span><span id="OUTDATA"></span>**OutData**  
インスタンスを受け取る[**デバッグ\_型指定された\_データ**](https://msdn.microsoft.com/library/windows/hardware/ff541706)要求されたメンバー。

<span id="InStrIndex"></span><span id="instrindex"></span><span id="INSTRINDEX"></span>**InStrIndex**  
要求されたメンバーの名前を指定します。 メンバーの名前はなどの下位メンバーを含めることができます、ドットで区切られたパス**mymember.mysubmember**します。 このドットで区切られたパス上のポインターを自動的に逆参照します。 ただし、ドット演算子 (**.**) 引き続き使用する必要がありますここで、通常の C ポインターではなく逆参照演算子 (**-&gt;**)。

<span id="Status"></span><span id="status"></span><span id="STATUS"></span>**状態**  
このサブ操作によって返されるステータス コードを受け取ります。 これは、によって返される値と同じ[**要求**](request.md)します。

<a name="remarks"></a>コメント
-------

EXT\_TDOP\_取得\_フィールドの値では、 [ **EXT\_TDOP** ](https://msdn.microsoft.com/library/windows/hardware/ff544529)列挙体。

このサブ操作のパラメーターのメンバーである、 [ **EXT\_型指定された\_データ**](https://msdn.microsoft.com/library/windows/hardware/ff545306)構造体。 EXT のメンバー\_型指定された\_データは、前のパラメーター セクションには示されていないこのサブ操作では使用されませんし、0 に設定する必要があります。 前のパラメーター セクション内のメンバーの説明では、使用は、メンバーを指定します。 参照してください**EXT\_型指定された\_データ**の詳細。

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>参照してください。


[**デバッグ\_要求\_EXT\_型指定された\_データ\_ANSI**](debug-request-ext-typed-data-ansi.md)

[**EXT\_TDOP**](https://msdn.microsoft.com/library/windows/hardware/ff544529)

[**EXT\_型指定された\_データ**](https://msdn.microsoft.com/library/windows/hardware/ff545306)

[**要求**](request.md)

 

 







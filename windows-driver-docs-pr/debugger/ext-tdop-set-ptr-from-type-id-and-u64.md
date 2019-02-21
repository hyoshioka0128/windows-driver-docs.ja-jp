---
title: EXT\_TDOP\_設定\_PTR\_FROM\_型\_ID\_AND\_U64
description: EXT\_TDOP\_設定\_PTR\_FROM\_型\_ID\_AND\_デバッグ U64 サブ操作\_要求\_EXT\_型指定された\_データ\_ANSI 要求操作は、種類を指定して、指定したメモリ位置へのポインターを表す型指定されたデータ記述を作成します。
ms.assetid: 1ca61962-718e-4cbd-8e16-f87e0c9ec9af
keywords:
- EXT_TDOP_SET_PTR_FROM_TYPE_ID_AND_U64 Windows Debugging
topic_type:
- apiref
api_name:
- EXT_TDOP_SET_PTR_FROM_TYPE_ID_AND_U64
api_type:
- NA
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 416ffe6f75517082538a03605fe9f5ce4b1620f2
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56539410"
---
# <a name="exttdopsetptrfromtypeidandu64"></a>EXT\_TDOP\_設定\_PTR\_FROM\_型\_ID\_AND\_U64


EXT\_TDOP\_設定\_PTR\_FROM\_型\_ID\_AND\_の U64 サブ操作、 [**デバッグ\_要求\_EXT\_型指定された\_データ\_ANSI**](debug-request-ext-typed-data-ansi.md)[**要求**](request.md)操作を作成します。種類を指定して、指定したメモリ位置へのポインターを表すデータの説明を入力します。

**パラメーター**

<span id="Operation"></span><span id="operation"></span><span id="OPERATION"></span>**操作**  
EXT に設定\_TDOP\_設定\_PTR\_FROM\_型\_ID\_AND\_U64 このサブ操作。

<span id="Flags"></span><span id="flags"></span><span id="FLAGS"></span>**フラグ**  
型指定されたデータの値が存在するターゲットのメモリを記述するビット フラグを指定します。 参照してください[ **EXT\_型指定された\_データ**](https://msdn.microsoft.com/library/windows/hardware/ff545306)これらのフラグの詳細についてはします。

<span id="InData"></span><span id="indata"></span><span id="INDATA"></span>**InData**  
型とメモリの場所を指定します。 このインスタンスの[**デバッグ\_型指定された\_データ**](https://msdn.microsoft.com/library/windows/hardware/ff541706)構造を手動で作成され、必要なメンバーに設定されます。 次のメンバーが使用されます。

<span id="ModBase"></span><span id="modbase"></span><span id="MODBASE"></span>**ModBase**  
データ型を含むモジュールのベース アドレスの仮想メモリのターゲットの場所を指定します。

<span id="Offset"></span><span id="offset"></span><span id="OFFSET"></span>**オフセット**  
データのメモリをターゲットの場所を指定します。 **オフセット**フラグに存在するがある場合を除き、仮想メモリ アドレスは、**フラグ**ことを指定する**オフセット**は物理メモリ アドレスです。

<span id="TypeId"></span><span id="typeid"></span><span id="TYPEID"></span>**TypeId**  
型の型 ID を指定します。

<span id="OutData"></span><span id="outdata"></span><span id="OUTDATA"></span>**OutData**  
型とメモリの場所へのポインターを表す型指定されたデータの説明を受け取ります。

<span id="Status"></span><span id="status"></span><span id="STATUS"></span>**状態**  
このサブ操作によって返されるステータス コードを受け取ります。 これは、によって返される値と同じ[**要求**](request.md)します。

<a name="remarks"></a>注釈
-------

EXT\_TDOP\_設定\_PTR\_FROM\_型\_ID\_AND\_U64 の値、 [ **EXT\_TDOP** ](https://msdn.microsoft.com/library/windows/hardware/ff544529)列挙体。

このサブ操作のパラメーターのメンバーである、 [ **EXT\_型指定された\_データ**](https://msdn.microsoft.com/library/windows/hardware/ff545306)構造体。 EXT のメンバー\_型指定された\_データは、前のパラメーター セクションには示されていないこのサブ操作では使用されませんし、0 に設定する必要があります。 前のパラメーター セクション内のメンバーの説明では、使用は、メンバーを指定します。 参照してください**EXT\_型指定された\_データ**の詳細。

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>参照してください。


[**デバッグ\_要求\_EXT\_型指定された\_データ\_ANSI**](debug-request-ext-typed-data-ansi.md)

[**EXT\_TDOP**](https://msdn.microsoft.com/library/windows/hardware/ff544529)

[**EXT\_型指定された\_データ**](https://msdn.microsoft.com/library/windows/hardware/ff545306)

[**要求**](request.md)

 

 







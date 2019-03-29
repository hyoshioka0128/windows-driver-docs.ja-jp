---
title: EXT\_TDOP\_評価
description: EXT\_TDOP\_、デバッグの評価のサブ操作\_要求\_EXT\_型指定された\_データ\_ANSI 要求操作の取得に型指定されたデータの説明式の値を表します。
ms.assetid: 2df6cf92-6889-4407-93c0-4c777a68cbc8
keywords:
- デバッグ EXT_TDOP_EVALUATE Windows
topic_type:
- apiref
api_name:
- EXT_TDOP_EVALUATE
api_type:
- NA
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0c80df88845aeddae6418f471d1adf1a90ab7e4e
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56581683"
---
# <a name="exttdopevaluate"></a>EXT\_TDOP\_評価


EXT\_TDOP\_のサブ操作の評価、 [**デバッグ\_要求\_EXT\_型指定された\_データ\_ANSI** ](debug-request-ext-typed-data-ansi.md)[**要求**](request.md)操作は、式の値を表す型指定されたデータの説明を返します。

**Parameters**

<span id="Operation"></span><span id="operation"></span><span id="OPERATION"></span>**操作**  
EXT に設定\_TDOP\_このサブ操作の評価。

<span id="Flags"></span><span id="flags"></span><span id="FLAGS"></span>**フラグ**  
式の値が存在するターゲットのメモリを記述するビット フラグを指定します。 参照してください[ **EXT\_型指定された\_データ**](https://msdn.microsoft.com/library/windows/hardware/ff545306)これらのフラグの詳細についてはします。

<span id="InData"></span><span id="indata"></span><span id="INDATA"></span>**InData**  
によって指定された式で値を持つことができます、省略可能な型指定されたデータを指定します。 **InStrIndex**します。 この値は、擬似レジスタとして式で使用 **$extin**します。

<span id="OutData"></span><span id="outdata"></span><span id="OUTDATA"></span>**OutData**  
受信、 [**デバッグ\_型指定された\_データ**](https://msdn.microsoft.com/library/windows/hardware/ff541706)式の値を表す構造体です。

<span id="InStrIndex"></span><span id="instrindex"></span><span id="INSTRINDEX"></span>**InStrIndex**  
評価する式を指定します。 この式は、既定の式エバリュエーターによって評価されます。

<span id="Status"></span><span id="status"></span><span id="STATUS"></span>**状態**  
このサブ操作によって返されるステータス コードを受け取ります。 これは、によって返される値と同じ[**要求**](request.md)します。

<a name="remarks"></a>コメント
-------

EXT\_TDOP\_評価は、値、 [ **EXT\_TDOP** ](https://msdn.microsoft.com/library/windows/hardware/ff544529)列挙体。

このサブ操作のパラメーターのメンバーである、 [ **EXT\_型指定された\_データ**](https://msdn.microsoft.com/library/windows/hardware/ff545306)構造体。 EXT のメンバー\_型指定された\_データは、前のパラメーター セクションには示されていないこのサブ操作では使用されませんし、0 に設定する必要があります。 前のパラメーター セクション内のメンバーの説明では、使用は、メンバーを指定します。 参照してください**EXT\_型指定された\_データ**の詳細。

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>参照してください。


[**デバッグ\_要求\_EXT\_型指定された\_データ\_ANSI**](debug-request-ext-typed-data-ansi.md)

[**EXT\_TDOP**](https://msdn.microsoft.com/library/windows/hardware/ff544529)

[**EXT\_型指定された\_データ**](https://msdn.microsoft.com/library/windows/hardware/ff545306)

[**要求**](request.md)

 

 







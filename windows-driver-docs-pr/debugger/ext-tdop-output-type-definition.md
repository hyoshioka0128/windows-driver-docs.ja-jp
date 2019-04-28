---
title: EXT\_TDOP\_出力\_型\_定義
description: EXT\_TDOP\_出力\_型\_DEBUG の定義のサブ操作\_要求\_EXT\_型指定された\_データ\_ANSI 要求操作は、指定された型指定されたデータの型の定義を出力します。
ms.assetid: 88e97066-f471-4e6c-9b9b-369f31da5bde
keywords:
- デバッグ EXT_TDOP_OUTPUT_TYPE_DEFINITION Windows
topic_type:
- apiref
api_name:
- EXT_TDOP_OUTPUT_TYPE_DEFINITION
api_type:
- NA
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: b60acaae7a16995166aa64a58b6b57f28c22b852
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63379888"
---
# <a name="exttdopoutputtypedefinition"></a>EXT\_TDOP\_出力\_型\_定義


EXT\_TDOP\_出力\_型\_のサブ操作の定義、 [**デバッグ\_要求\_EXT\_型指定された\_データ\_ANSI**](debug-request-ext-typed-data-ansi.md)[**要求**](request.md)操作が指定された型指定されたデータの型の定義を出力します。

**Parameters**

<span id="Operation"></span><span id="operation"></span><span id="OPERATION"></span>**操作**  
EXT に設定\_TDOP\_出力\_型\_このサブ操作の定義。

<span id="InData"></span><span id="indata"></span><span id="INDATA"></span>**InData**  
型の定義を印刷する型指定されたデータを指定します。

<span id="Status"></span><span id="status"></span><span id="STATUS"></span>**状態**  
このサブ操作によって返されるステータス コードを受け取ります。 これは、によって返される値と同じ[**要求**](request.md)します。

<a name="remarks"></a>注釈
-------

型の定義の書式設定し、デバッガー エンジンに送信される[コールバックを出力](https://msdn.microsoft.com/library/windows/hardware/ff560116#output-callbacks)します。

EXT\_TDOP\_出力\_型\_定義内の値とは、 [ **EXT\_TDOP** ](https://msdn.microsoft.com/library/windows/hardware/ff544529)列挙体。

このサブ操作のパラメーターのメンバーである、 [ **EXT\_型指定された\_データ**](https://msdn.microsoft.com/library/windows/hardware/ff545306)構造体。 EXT のメンバー\_型指定された\_データは、前のパラメーター セクションには示されていないこのサブ操作では使用されませんし、0 に設定する必要があります。 前のパラメーター セクション内のメンバーの説明では、使用は、メンバーを指定します。 参照してください**EXT\_型指定された\_データ**の詳細。

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>参照してください。


[**デバッグ\_要求\_EXT\_型指定された\_データ\_ANSI**](debug-request-ext-typed-data-ansi.md)

[**EXT\_TDOP**](https://msdn.microsoft.com/library/windows/hardware/ff544529)

[**EXT\_型指定された\_データ**](https://msdn.microsoft.com/library/windows/hardware/ff545306)

[**要求**](request.md)

 

 







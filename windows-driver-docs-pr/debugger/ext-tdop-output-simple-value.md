---
title: EXT\_TDOP\_出力\_単純\_値
description: EXT\_TDOP\_出力\_単純\_、デバッグの値のサブ操作\_要求\_EXT\_型指定された\_データ\_ANSI 要求操作は、指定した型指定されたデータの値を出力します。
ms.assetid: dce51823-34e9-43b9-9cbd-41b436b43ccb
keywords:
- デバッグ EXT_TDOP_OUTPUT_SIMPLE_VALUE Windows
topic_type:
- apiref
api_name:
- EXT_TDOP_OUTPUT_SIMPLE_VALUE
api_type:
- NA
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: acaf37b2c3c1c157a112b23a0cf0da3b7607eed2
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56535868"
---
# <a name="exttdopoutputsimplevalue"></a>EXT\_TDOP\_出力\_単純\_値


EXT\_TDOP\_出力\_単純\_のサブ操作の値、 [**デバッグ\_要求\_EXT\_型指定された\_データ\_ANSI**](debug-request-ext-typed-data-ansi.md)[**要求**](request.md)操作には、指定した型指定されたデータの値が出力されます。

**パラメーター**

<span id="Operation"></span><span id="operation"></span><span id="OPERATION"></span>**操作**  
EXT に設定\_TDOP\_出力\_単純\_このサブ操作の値。

<span id="InData"></span><span id="indata"></span><span id="INDATA"></span>**InData**  
印刷される値を持つ、型指定されたデータを指定します。

<span id="Status"></span><span id="status"></span><span id="STATUS"></span>**状態**  
このサブ操作によって返されるステータス コードを受け取ります。 これは、によって返される値と同じ[**要求**](request.md)します。

<a name="remarks"></a>注釈
-------

値が書式設定し、デバッガー エンジンに送信される[コールバックを出力](https://msdn.microsoft.com/library/windows/hardware/ff560116#output-callbacks)します。

EXT\_TDOP\_出力\_単純\_値値では、 [ **EXT\_TDOP** ](https://msdn.microsoft.com/library/windows/hardware/ff544529)列挙体。

このサブ操作のパラメーターのメンバーである、 [ **EXT\_型指定された\_データ**](https://msdn.microsoft.com/library/windows/hardware/ff545306)構造体。 EXT のメンバー\_型指定された\_データは、前のパラメーター セクションには示されていないこのサブ操作では使用されませんし、0 に設定する必要があります。 前のパラメーター セクション内のメンバーの説明では、使用は、メンバーを指定します。 参照してください**EXT\_型指定された\_データ**の詳細。

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>参照してください。


[**デバッグ\_要求\_EXT\_型指定された\_データ\_ANSI**](debug-request-ext-typed-data-ansi.md)

[**EXT\_TDOP**](https://msdn.microsoft.com/library/windows/hardware/ff544529)

[**EXT\_型指定された\_データ**](https://msdn.microsoft.com/library/windows/hardware/ff545306)

[**要求**](request.md)

 

 







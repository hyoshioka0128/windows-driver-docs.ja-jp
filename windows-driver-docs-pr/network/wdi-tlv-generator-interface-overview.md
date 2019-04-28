---
title: WDI TLV ジェネレーター インターフェイスの概要
description: このセクションでは、WDI TLV ジェネレーター インターフェイスの関数のモデルの概要を説明します
ms.assetid: 8A344BF7-932E-4404-9B3E-E7D3C33722C3
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: fe1a49a55ebbb1c918e011a724f64f90a9c48092
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63382866"
---
# <a name="wdi-tlv-generator-interface-overview"></a>WDI TLV ジェネレーター インターフェイスの概要


## <a name="c-overloaded-function-model"></a>C++ のオーバー ロードされた関数のモデル


このモデルでは、データ構造から TLV バイト配列を生成する 1 つだけの関数呼び出しです。

```c++
WDI_INDICATION_BSS_ENTRY_LIST_PARAMETERS BssEntryList = ...;
BYTE* pOutput = NULL;
ULONG length = 0;
NDIS_STATUS ndisStatus = NDIS_STATUS_SUCCESS;

ndisStatus = Generate(
    &BssEntryList,
    cbHeaderLength,
    &Context,
    &length,
    &pOutput);
```

2 番目のパラメーターは、非常に役立ちます。 場合によっては、TLV バッファーがより大きなデータ構造体にパックされているし、このパラメーターでは、事前にそのヘッダーのバッファーの先頭にスペースを予約することができます。 正しい値*cbHeaderLength*多くの場合は、`sizeof(WDI_MESSAGE_HEADER)`します。

メッセージの関連付けられているデータがない場合はまだ生成 Api では、オーバー ロードが、最初のパラメーターはオプションであり、単として渡すことで`(EmptyMessageStructureType*)NULL`します。

含まれる TLV データで完了したら*pOutput*バッファーを解放するためにライブラリにコールバックする必要があります。

```c++
    FreeGenerated(pOutput);
    pOutput = NULL;
```

## <a name="c-style-function-model"></a>C スタイルの関数のモデル


このモデルで最上位レベル メッセージごとの特定の生成ルーチンがあるまたは構造体 C がサポートされていないためにオーバー ロードされた関数。 それ以外の場合、C モデルの場合と同様に動作します。

```c
ndisStatus = GenerateWdiGetAdapterCapabilities(
    &adapterCapabilities,
    (ULONG)sizeof(WFC_COMMAND_HEADER),
    &Context,
    &length,
    &pOutput);
```

TLV バイト配列を使用したら、C モデルと同じ方法でメモリを解放するコールバックします。

```c
    FreeGenerated(pOutput);
    pOutput = NULL;
```

 

 






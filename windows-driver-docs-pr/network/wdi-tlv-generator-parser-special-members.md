---
title: WDI TLV ジェネレーター/パーサーの特殊メンバー
description: このセクションには、WDI TLV ジェネレーター/パーサーの特殊なメンバーがについて説明します
ms.assetid: 2FD485E5-E2F9-4B21-A777-ABA9693B1223
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 49fdbc21dac128aa40c307f0f3a2580f578e1d73
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63382862"
---
# <a name="wdi-tlv-generatorparser-special-members"></a>WDI TLV ジェネレーター/パーサーの特殊メンバー


## <a name="optional-members"></a>省略可能なメンバー


親がという名前の 1 つのフィールドを省略可能な子 TLV メンバーを持つ任意の TLV の **(省略可能)** します。 という名前の省略可能な子ごとに 1 つのブール型フィールドがある、そのフィールド内で * **&lt;子\_名前&gt;*\_IsPresent**、これが TRUE に設定パーサーによって場合、子存在する場合は、それ以外の場合。 同様に、Api に予想されるフィールドを生成場合は TRUE にする必要があります、TLV バイト ストリームに存在して FALSE それ以外の場合。

```C++
WDI_SET_FIRMWARE_CONFIGURATION_PARAMETERS fwConfig = { 0 };
NDIS_STATUS status;
status = ParseWdiSetAdapterConfiguration(
    pNdisRequest->DATA.METHOD_INFORMATION.InputBufferLength - 
        sizeof(WDI_MESSAGE_HEADER),
    (PUINT8)pNdisRequest->DATA.METHOD_INFORMATION.InformationBuffer + 
        sizeof(WDI_MESSAGE_HEADER),
    0,
    &fwConfig);

if (status == NDIS_STATUS_SUCCESS)
{
    if (fwConfig.Optional.MacAddress_IsPresent)
    {
        // Safe to use fwConfig.MacAddress
        fwConfig.MacAddress;
    }
}
```

## <a name="array-members"></a>配列メンバー


同じ親を持つ同じ種類の複数の子要素を表示したときに (たとえば、&lt;コンテナー/&gt;の*isCollection*属性)、パーサーとジェネレーターは、特別な構造を使用して、配列を表します。ArrayOfElements します。 C++ クライアントは、デストラクションのセマンティクスでクリーンアップする、厳密に型指定されたテンプレートの構造と適用されます。 C のクライアント (たとえば、ArrayOfElementsOfUINT8) 明示的に名前付き構造体が作成されます。 ただし、これらの構造が自動的にクリーンアップされません C がデストラクターをサポートしていないため、ユーザー C Api のメモリ リークが発生しないように注意する必要があります (または二重解放)。

ArrayOfElements 内の 2 つの重要なフィールドです。**ElementCount**と**pElements**します。 **ElementCount**は、配列内の要素の数です。 **pElements**は要素の C スタイル配列です。 このサンプルで示すように、この要素を反復できます。

```C++
for (UINT32 i = 0;
    i < pConnectTaskParameters->ConnectParameters.
            MulticastCipherAlgorithms.ElementCount;
    i++)
{
    // Safe to use pElements[i]
    pConnectTaskParameters->ConnectParameters.MulticastCipherAlgorithms.
        pElements[i];
}
```

3 番目のフィールド**MemoryInternallyAllocated**パーサー/ジェネレーターによって内部的に使用されます。 IHV によっては変更できません。

 

 






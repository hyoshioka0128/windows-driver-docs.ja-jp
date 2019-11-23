---
title: WDI TLV バージョン管理
description: 下位互換性を維持するために、WDI とミニポートの両方で、TLV ストリームがバージョン管理の境界として使用されます。
ms.assetid: 308B4C7A-4AC1-4FEB-9775-65ED088F7C48
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2099ffc02bc2159232145f8b4c33f8b511054cb8
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841717"
---
# <a name="wdi-tlv-versioning"></a>WDI TLV バージョン管理


下位互換性を維持するために、WDI とミニポートの両方で、TLV ストリームがバージョン管理の境界として使用されます。 TLV バイトストリームのプロデューサーは、常に下位互換性のある TLV を生成する必要があり、新たに追加されたフィールドは含まれません。 これを実現するには、 **Peerversion**を*Context*パラメーターに追加します。 このフィールドは、初期化中に受信した*WdiVersion*に対して、呼び出し元によって初期化される必要があります。

次に、*コンテキスト*パラメーターの型定義を示します。これは、すべての解析 API と生成 API に渡されます。

```C++
typedef struct _TLV_CONTEXT
{
    ULONG_PTR   AllocationContext;
    ULONG       PeerVersion;
} TLV_CONTEXT, *PTLV_CONTEXT;
typedef const TLV_CONTEXT * PCTLV_CONTEXT;
```

割り当て**コンテキスト**は解析および生成 api によって変更されず、引き続きミニポートで提供される演算子 `new` コールバックに渡されます。 詳細については、「 [WDI TLV generator/パーサーメモリインターフェイス](wdi-tlv-generator-parser-memory-interface.md)」を参照してください。

WDI ベースのシングルバイナリドライバーが古いバージョンの WDI に対して実行される場合、ミニポートのジェネレーターは、 **Peerversion**を使用して古いバイトストリームを生成します。 逆に、パーサーは、 **Peerversion**に基づく古いバイトストリームを使用して、新しいデータ構造に変換します。

ミニポートドライバーで TLV パーサージェネレーターライブラリを使用せず、代わりに独自の TLV パーサーとジェネレーターを記述する場合は、1つのバイナリで古いバージョンの OS (つまり、WDI の旧バージョン) のみを実行する必要があるため、この機能も含まれている必要があります。 パーサーは、古い WDI によって生成された TLV 文法を受け入れる必要があり、そのジェネレーターは、前の文法に従って TLVs のみを生成する必要があります。

XML は、containerRefs で許可されている2つの属性 ( *Versionadded*および*versionadded*) を使用して、このバージョン管理をサポートするように強化されています。 これは、パーサーとジェネレーターが、ピアバージョンに応じてバイトストリームを調整するためのものです。

**  パーサー**とジェネレーターは、常に最新の状態\_\_バージョンとリンクされていることを前提としています。 このミニポートは、WDI\_VERSION\_1\_0 のような特定のバージョンを使用するのではなく、 [**NdisMRegisterWdiMiniportDriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dot11wdi/nf-dot11wdi-ndismregisterwdiminiportdriver)を呼び出すと、WDI\_VERSION\_LATEST を常に最新[ **\_\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/dot11wdi/ns-dot11wdi-_ndis_miniport_driver_wdi_characteristics)の状態に渡す必要があります。これは、他のエンドが予期しないバイト**ストリームを送信**する可能性があるためです。\_\_

 

 

 






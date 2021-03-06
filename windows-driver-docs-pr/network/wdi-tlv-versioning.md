---
title: WDI TLV バージョン管理
description: 下位互換性を維持するには、WDI およびミニポートの両方はバージョン管理の境界として TLV ストリームを使用します。
ms.assetid: 308B4C7A-4AC1-4FEB-9775-65ED088F7C48
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 07e04e1d5a55eeaeaae4786ef3aac101ea1133d3
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67357281"
---
# <a name="wdi-tlv-versioning"></a>WDI TLV バージョン管理


下位互換性を維持するには、WDI およびミニポートの両方はバージョン管理の境界として TLV ストリームを使用します。 TLV バイト ストリームのプロデューサーは、常に下位互換性のある TLV を生成し、新しく追加されたフィールドが含まれていない必要があります。 これは、追加することで実現を**PeerVersion**を*コンテキスト*パラメーター。 このフィールドは、呼び出し元によって初期化する必要があります、 *WdiVersion*初期化中に受信します。

型定義をここでは、*コンテキスト*パラメーターで、すべての解析と生成 API に渡されます。

```C++
typedef struct _TLV_CONTEXT
{
    ULONG_PTR   AllocationContext;
    ULONG       PeerVersion;
} TLV_CONTEXT, *PTLV_CONTEXT;
typedef const TLV_CONTEXT * PCTLV_CONTEXT;
```

**AllocationContext**解析および Api の生成によって変更されていない場合は、ミニポートで提供される演算子に渡すには引き続き`new`コールバック。 詳細については、次を参照してください。 [WDI TLV ジェネレーター/パーサー メモリ インターフェイス](wdi-tlv-generator-parser-memory-interface.md)します。

ミニポートのジェネレーターを使用して、WDI に基づく単一バイナリ ドライバーは、WDI の以前のバージョンに対して実行する場合、 **PeerVersion**古いバイト ストリームを生成します。 逆に、パーサーがに基づいて、古いバイト ストリームを消費、 **PeerVersion**と、新しいデータ構造体に変換します。

ミニポート ドライバー TLV パーサーのジェネレーターのライブラリを使用しない代わりに独自の TLV パーサーと、ジェネレーターを書き込み、古い OS バージョンとのみ WDI のために以前のバージョン) を実行している 1 つのバイナリには、この機能も、含める必要があります。 パーサーは、以前の WDI によって生成された TLV 文法を受け入れる必要があり、そのジェネレーター: 古い文法に従って TLVs のみを生成する必要があります。

XML を containerRefs で許可されている 2 つの属性でこのバージョン管理をサポートするために拡張されています: *versionAdded*と*versionRemoved*します。 これは、パーサーと対応するピアのバージョンのバイト ストリームを調整するジェネレーターを促すものです。

**注**  パーサーとジェネレーターは、それらが、WDI に常にリンクされていることを想定しています\_バージョン\_最新です。 WDI は常に成功ミニポート\_バージョン\_の最新[ **NDIS\_ミニポート\_ドライバー\_WDI\_特性**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dot11wdi/ns-dot11wdi-_ndis_miniport_driver_wdi_characteristics)::**WdiVersion**を呼び出すときに[ **NdisMRegisterWdiMiniportDriver** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dot11wdi/nf-dot11wdi-ndismregisterwdiminiportdriver) WDI などの特定のバージョンを使用するのではなく\_バージョン\_1\_0、期限切れになり、もう一方の end が予想されるバイト ストリームを送信可能性がありますので、TLV パーサーのジェネレーターに問題が発生します。

 

 

 






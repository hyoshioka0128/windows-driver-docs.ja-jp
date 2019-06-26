---
title: 帯域幅割り当て
description: 帯域幅割り当て
ms.assetid: 775B4085-6028-441F-9D52-341077FF1647
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7cba524d36fafd814797c7768573200555bf7fd7
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67354652"
---
# <a name="bandwidth-allocation"></a>帯域幅割り当て


帯域幅の割り当ては、Enhanced Transmission Selection (ETS) アルゴリズムのコンポーネントです。 ETS が IEEE 802.1 qaz で指定されたドラフト標準。 この標準は、IEEE 802.1 データ センター ブリッジング (DCB) インターフェイスのフレームワークの一部です。

ETS、トラフィック クラスごとに 2 つの直接接続されているピア間でパケットを転送するためには、帯域幅の割合が割り当てられます。 トラフィック クラスに割り当てられた帯域幅が完全に使用しない場合は、IEEE 802.1p の優先度レベルがそれぞれ異なるトラフィック クラスで共有される未使用の帯域幅が、ETS できます。

NDIS のサービス品質 (QoS) パラメーターを使用して指定、 [ **NDIS\_QOS\_パラメーター** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_qos_parameters)構造体。 **TcBandwidthAssignmentTable**メンバーには、ETS のアルゴリズムを使用するクラスをトラフィックの帯域幅の割り当てを指定する配列が含まれています。

優先度レベルの詳細については、次を参照してください。 [IEEE 802.1p の優先度レベル](ieee-802-1p-priority-levels.md)します。

 

 






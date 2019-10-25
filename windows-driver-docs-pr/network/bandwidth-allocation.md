---
title: 帯域幅割り当て
description: 帯域幅割り当て
ms.assetid: 775B4085-6028-441F-9D52-341077FF1647
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6e24d2f66f9ad5fe97e215d65009510f4e9a8175
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72835273"
---
# <a name="bandwidth-allocation"></a>帯域幅割り当て


帯域幅割り当ては、Enhanced 伝送選択 (送信) アルゴリズムのコンポーネントです。 802.1 は、IEEE Qaz draft standard に指定されています。 この標準は、IEEE 802.1 データセンターブリッジング (DCB) インターフェイスのフレームワークの一部です。

この場合、各 traffic クラスには、直接接続されている2つのピア間でパケットを送信するために使用できる帯域幅の割合が割り当てられます。 Traffic クラスに割り当てられた帯域幅が完全に使用されていない場合は、異なる IEEE 802.1 p 優先度レベルを持つトラフィッククラスで、未使用の帯域幅を共有することができます。

NDIS Quality of Service (QoS) パラメーターは、 [**ndis\_QoS\_parameters**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_qos_parameters)構造体によって指定されます。 **TcBandwidthAssignmentTable**メンバーには、発生アルゴリズムを使用するトラフィッククラスの帯域幅割り当てを指定する配列が含まれています。

優先度レベルの詳細については、「 [IEEE 802.1 p Priority levels](ieee-802-1p-priority-levels.md)」を参照してください。

 

 






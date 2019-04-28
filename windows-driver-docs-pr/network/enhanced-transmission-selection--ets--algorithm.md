---
title: 拡張送信選択 (ETS) アルゴリズム
description: 拡張送信選択 (ETS) アルゴリズム
ms.assetid: 952ECB1E-96AD-4717-8E49-68558E7E9AD4
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b7ebf9b784f149a063d3b82698f196264cf21944
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63372454"
---
# <a name="enhanced-transmission-selection-ets-algorithm"></a>拡張送信選択 (ETS) アルゴリズム


強化された Transmission Selection (ETS) は、IEEE 802.1 qaz で指定されている伝送選択アルゴリズム (TSA) ドラフト標準。 この標準は、IEEE 802.1 データ センター ブリッジング (DCB) インターフェイスのフレームワークの一部です。

IEEE 802.1p の優先度レベルのみに基づく送信選択は、優先順位の高いトラフィックが優先順位の低いトラフィックをブロックするような状況につながります。 ETS では、さまざまな 802.1p の優先度レベルに割り当てられているトラフィック クラスに割り当てられる帯域幅の最小量を許可して公平性を保証します。

トラフィック クラスごとには、直接接続されているピア間のデータ リンクで使用できる帯域幅の割合が割り当てられます。 トラフィック クラスでは、その割り当てられた帯域幅を使用しない場合、ETS、トラフィック クラスを使用していない利用可能な帯域幅を使用するには、その他のトラフィック クラスを使用します。

OID メソッド要求を通じた NDIS サービスの品質 (QoS) トラフィック クラスが定義されている[OID\_QOS\_パラメーター](https://msdn.microsoft.com/library/windows/hardware/hh451835)します。 この OID 要求に含まれる、 [ **NDIS\_QOS\_パラメーター** ](https://msdn.microsoft.com/library/windows/hardware/hh451640)トラフィックの次のクラス属性を指定する構造体。

-   指定されているトラフィック クラスの数、 **NumTrafficClasses**メンバー。

-   トラフィック クラスで使用される TSA します。 これがで指定されて、 **TsaAssignmentTable**メンバー。 かどうか、トラフィック クラスの table 要素は、NDIS に設定されます\_QOS\_TSA\_ETS、トラフィック クラスを使用して、ETS TSA します。

-   トラフィック クラスに割り当てられている 802.1p の優先度です。 トラフィック クラスは、1 つまたは複数の優先度レベルに割り当てることができます。 ただし、各優先度レベルは 1 つのトラフィック クラスにのみ割り当てることができます。

    詳細については、次を参照してください。[トラフィック クラス優先順位の割り当て](traffic-class-priority-assignment.md)します。

-   トラフィック クラスに割り当てられた帯域幅。 これがで指定されて、 **TcBandwidthAssignmentTable**メンバー。 このテーブルは ETS TSA を使用して、トラフィック クラスに対してのみです。

    ETS の帯域幅の割り当ての詳細については、次を参照してください。[帯域幅割り当て](bandwidth-allocation.md)します。

優先度レベルの詳細については、次を参照してください。 [IEEE 802.1p の優先度レベル](ieee-802-1p-priority-levels.md)します。

 

 






---
title: 拡張送信選択 (ETS) アルゴリズム
description: 拡張送信選択 (ETS) アルゴリズム
ms.assetid: 952ECB1E-96AD-4717-8E49-68558E7E9AD4
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 16fe042990e221972b542c577ff8af4302cfd652
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838121"
---
# <a name="enhanced-transmission-selection-ets-algorithm"></a>拡張送信選択 (ETS) アルゴリズム


Enhanced 伝送選択 (TSA) は、IEEE 802.1 Qaz draft standard によって指定された伝送選択アルゴリズム () です。 この標準は、IEEE 802.1 データセンターブリッジング (DCB) インターフェイスのフレームワークの一部です。

IEEE 802.1 p の優先度レベルのみに基づいて転送を選択すると、優先順位の高いトラフィックが優先順位の低いトラフィックをブロックする状況が発生する可能性があります。 では、さまざまな 802.1 p 優先度レベルに割り当てられているトラフィッククラスに最小量の帯域幅を割り当てることによって、公平性を保証します。

各 traffic クラスには、直接接続されているピア間のデータリンクで使用可能な帯域幅に対する割合が割り当てられます。 トラフィッククラスで割り当てられた帯域幅が使用されていない場合は、トラフィッククラスが使用していない帯域幅を他のトラフィッククラスが使用できるようにします。

NDIS Quality of Service (QoS) トラフィッククラスは、 [oid\_QoS\_パラメーター](https://docs.microsoft.com/windows-hardware/drivers/network/oid-qos-parameters)の oid メソッド要求によって定義されます。 この OID 要求には、次の traffic クラス属性を指定する[**NDIS\_QOS\_PARAMETERS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_qos_parameters)構造体が含まれています。

-   **NumTrafficClasses**メンバーによって指定されたトラフィッククラスの数。

-   Traffic クラスによって使用される TSA。 これは、 **Tsaのテーブル**メンバーによって指定されます。 Traffic クラスの table 要素が NDIS に設定されている場合\_QOS\_TSA\_します。 traffic クラスは、TSA を使用します。

-   Traffic クラスに割り当てられている 802.1 p の優先順位。 Traffic クラスは、1つまたは複数の優先度レベルに割り当てることができます。 ただし、各優先度レベルは、1つの traffic クラスにのみ割り当てることができます。

    詳細については、「 [Traffic クラスの優先順位割り当て](traffic-class-priority-assignment.md)」を参照してください。

-   Traffic クラスに割り当てられた帯域幅。 これは、 **TcBandwidthAssignmentTable**メンバーによって指定されます。 このテーブルは、TSA を使用するトラフィッククラスに対してのみ有効です。

    帯域幅の割り当ての詳細については、「[帯域幅の割り当て](bandwidth-allocation.md)」を参照してください。

優先度レベルの詳細については、「 [IEEE 802.1 p Priority levels](ieee-802-1p-priority-levels.md)」を参照してください。

 

 






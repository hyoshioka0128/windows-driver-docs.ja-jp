---
title: NDIS QoS トラフィック クラス
description: NDIS QoS トラフィック クラス
ms.assetid: 0DE61F97-7173-4D91-90F3-20EAFB810251
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e1d60685e6bb08405adf399517c441ccf9bdd0c2
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67369161"
---
# <a name="ndis-qos-traffic-classes"></a>NDIS QoS トラフィック クラス


NDIS サービスの品質 (QoS) トラフィック クラスは、一連のネットワーク アダプターの送信、処理方法を決定するポリシーを指定または*エグレス*パケットの優先順位の高い配信します。 トラフィック クラスごとには、送信パケットに適用される次のポリシーを指定します。

<a href="" id="priority-level-and-flow-control"></a>優先度レベルとフロー制御  
このポリシーは、エグレス トラフィックの IEEE 802.1p の優先度レベルと省略可能なフロー コントロール アルゴリズムを定義します。

詳細については、次を参照してください。[優先度レベルとフロー制御](priority-levels-and-flow-control.md)します。

<a href="" id="traffic-selection-algorithms--tsas-"></a>トラフィックの選択アルゴリズム (TSAs)  
このポリシーは、ネットワーク アダプターがその送信キューからの配信のエグレス トラフィックがどのように選択する方法を指定します。 たとえば、アダプターでは、IEEE 802.1p の優先度またはトラフィック クラスごとに割り当てられているエグレス帯域幅の割合に基づく送信パケットを選択できます。

詳細については、次を参照してください。[伝送選択アルゴリズム (TSAs)](transmission-selection-algorithms--tsas-.md)します。

**注**  帯域幅の割り当てはの Enhanced Transmission Selection (ETS) TSA のみをサポートします。 詳細については、次を参照してください。 [Enhanced Transmission Selection (ETS) アルゴリズム](enhanced-transmission-selection--ets--algorithm.md)します。

 

トラフィック クラスのオブジェクト識別子 (OID) メソッドの要求を使用して指定[OID\_QOS\_パラメーター](https://docs.microsoft.com/windows-hardware/drivers/network/oid-qos-parameters)します。 この OID 要求に含まれる、 [ **NDIS\_QOS\_パラメーター** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_qos_parameters)次の NDIS QoS パラメーターを指定する構造体。

-   ネットワーク アダプターで構成されるトラフィック クラスの数。 トラフィック クラスごとが 0 の範囲内で値によって識別されます (**NumTrafficClasses**– 1) ここで、 **NumTrafficClasses**のメンバーである、 [ **NDIS\_QOS\_パラメーター** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_qos_parameters)構造体。

    **注**  NDIS 6.30 以降、NDIS QoS、NDIS 最大サポート\_QOS\_最大\_トラフィック\_トラフィック クラスのクラス (8)。 ネットワーク アダプターには、次の 3 つのトラフィック クラスの最小値をサポートする必要があります。

     

-   トラフィック クラスに関連付けられた 802.1p の優先度レベル。

-   トラフィック クラスに関連付けられた TSA します。

-   ETS TSA を使用するトラフィック クラスごとに割り当てられている送信帯域幅。

OID メソッド要求[OID\_QOS\_パラメーター](https://docs.microsoft.com/windows-hardware/drivers/network/oid-qos-parameters)もトラフィックの分類を指定します。 これらの分類は、送信パケットと IEEE 802.1p の優先度のレベル間のリレーションシップを定義します。 詳細については、次を参照してください。 [NDIS QoS トラフィックの分類](ndis-qos-traffic-classifications.md)します。

 

 






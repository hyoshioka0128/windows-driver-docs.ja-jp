---
title: NDIS QoS トラフィック クラス
description: NDIS QoS トラフィック クラス
ms.assetid: 0DE61F97-7173-4D91-90F3-20EAFB810251
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d829028d1310601948a316ad37b1d8d5286b17e2
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72833761"
---
# <a name="ndis-qos-traffic-classes"></a>NDIS QoS トラフィック クラス


NDIS Quality of Service (QoS) トラフィッククラスは、優先される配信のためにネットワークアダプターが*送信または*送信パケットを処理する方法を決定する一連のポリシーを指定します。 各 traffic クラスは、送信パケットに適用される次のポリシーを指定します。

<a href="" id="priority-level-and-flow-control"></a>優先度レベルとフロー制御  
このポリシーでは、送信トラフィックの IEEE 802.1 p 優先度レベルとオプションのフロー制御アルゴリズムを定義します。

詳細については、「[優先度レベルとフロー制御](priority-levels-and-flow-control.md)」を参照してください。

<a href="" id="traffic-selection-algorithms--tsas-"></a>トラフィック選択アルゴリズム (TSAs)  
このポリシーでは、ネットワークアダプターが送信キューから配信用の送信トラフィックを選択する方法を指定します。 たとえば、アダプターは、IEEE 802.1 p の優先順位に基づいた送信パケット、または各 traffic クラスに割り当てられている送信帯域幅の割合を選択できます。

詳細については、「[伝送選択アルゴリズム (TSAs)](transmission-selection-algorithms--tsas-.md)」を参照してください。

**注**  帯域幅の割り当ては、Enhanced 伝送選択 (TSA) の場合にのみサポートされます。 詳細については、「 [Enhanced 伝送選択 (送信) アルゴリズム](enhanced-transmission-selection--ets--algorithm.md)」を参照してください。

 

Traffic クラスは、オブジェクト識別子 (OID) による Oid 要求の要求によって指定され、 [QOS\_パラメーター\_](https://docs.microsoft.com/windows-hardware/drivers/network/oid-qos-parameters)ます。 この OID 要求には、次の NDIS QoS パラメーターを指定する[**ndis\_QOS\_PARAMETERS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_qos_parameters)構造体が含まれています。

-   ネットワークアダプターで構成されるトラフィッククラスの数。 各 traffic クラスは、0 ~ (**NumTrafficClasses**– 1) の範囲の値によって識別されます。 **NumTrafficClasses**は、 [**NDIS\_QOS\_PARAMETERS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_qos_parameters)構造体のメンバーです。

    **注**  Ndis 6.30 以降では、ndis qos では、最大\_トラフィック\_クラス (8) のトラフィッククラスの最大の NDIS\_qos\_サポートされています。 ネットワークアダプターは、3つ以上のトラフィッククラスをサポートしている必要があります。

     

-   Traffic クラスに関連付けられている 802.1 p の優先度レベル。

-   Traffic クラスに関連付けられている TSA。

-   TSA を使用する各トラフィッククラスに割り当てられた送信帯域幅。

Oid [\_\_](https://docs.microsoft.com/windows-hardware/drivers/network/oid-qos-parameters)の oid のメソッド要求では、トラフィックの分類も指定します。 これらの分類によって、送信パケットと IEEE 802.1 p の優先度レベルの関係が定義されます。 詳細については、「 [NDIS QoS Traffic 分類](ndis-qos-traffic-classifications.md)」を参照してください。

 

 






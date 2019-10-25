---
title: トラフィック クラス優先順位割り当て
description: トラフィック クラス優先順位割り当て
ms.assetid: 846AC7E6-28D9-4610-9493-BE547869AB15
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c28e0f5540c936fe544e8632be27e6ba0b97aeb5
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841779"
---
# <a name="traffic-class-priority-assignment"></a>トラフィック クラス優先順位割り当て


Enhanced 伝送選択 (送信) アルゴリズムでは、traffic クラスに 802.1 p 優先度レベルを割り当てる方法を指定します。 802.1 は、IEEE Qaz draft standard に指定されています。 この標準は、IEEE 802.1 データセンターブリッジング (DCB) インターフェイスのフレームワークの一部です。

NDIS Quality of Service (QoS) トラフィッククラスは、ネットワークアダプターが*送信または*送信パケットを処理する方法を決定する一連のポリシーを指定します。 この場合、各 traffic クラスには、パケットを送信するための IEEE 802.1 p 優先度レベルが割り当てられます。 Traffic クラスは、1つまたは複数の IEEE 802.1 p 優先度レベルに割り当てることができます。 ただし、各 IEEE 802.1 p 優先度レベルは、1つの traffic クラスにのみ割り当てることができます。

Ndis QoS パラメーターは、 [**ndis\_qos\_parameters**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_qos_parameters)構造体によって指定されます。 優先順位割り当て**テーブル**メンバーには、各 traffic クラスの優先度割り当てを指定する配列が含まれています。

優先度レベルの詳細については、「 [IEEE 802.1 p Priority levels](ieee-802-1p-priority-levels.md)」を参照してください。

 

 






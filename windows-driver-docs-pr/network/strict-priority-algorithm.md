---
title: 厳密な優先順位アルゴリズム
description: 厳密な優先順位アルゴリズム
ms.assetid: 7C7A34CA-673C-4EFC-970D-08458AA83EAD
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c7f777a209c2e5ccb123c72d5a9a0f71e07a59ef
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841815"
---
# <a name="strict-priority-algorithm"></a>厳密な優先順位アルゴリズム


Strict priority は、IEEE 802.1 Q-2005 標準で指定されている伝送選択アルゴリズム (TSA) です。 この標準は、IEEE 802.1 データセンターブリッジング (DCB) インターフェイスのフレームワークの一部です。

ネットワークアダプターは、厳密な優先順位の TSA を使用する場合、パケットの指定された IEEE 802.1 p 優先度レベルのみに基づいて、送信するパケットを選択します。 その結果、優先度の高いパケットは常に、優先度レベルの低いパケットより前に送信されます。

ミニポートドライバーでは、ndis\_QOS\_\_\_機能を設定することによって、厳密な優先順位の TSA のサポートを指定します。これは、 [**ndis\_qos\_CAPABILITIES**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_qos_capabilities)構造体の**FLAGS**メンバーでサポートされています。\_ ドライバーは、この構造を使用して、 [**NdisMSetMiniportAttributes**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismsetminiportattributes)への呼び出しに NDIS QOS と DCB 機能を登録します。

優先度レベルの詳細については、「 [IEEE 802.1 p Priority levels](ieee-802-1p-priority-levels.md)」を参照してください。

**注**  Ndis 6.30 以降では、DCB インターフェイスの ndis Quality of Service (QoS) をサポートするミニポートドライバーは、厳密な優先順位 TSA のサポートをアドバタイズする必要があります。

 

 

 






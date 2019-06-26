---
title: 厳密な優先順位アルゴリズム
description: 厳密な優先順位アルゴリズム
ms.assetid: 7C7A34CA-673C-4EFC-970D-08458AA83EAD
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: aa57416a294e273220c8206b901b855146646609
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67370574"
---
# <a name="strict-priority-algorithm"></a>厳密な優先順位アルゴリズム


厳密な優先順位は、IEEE 802.1 q で指定されている伝送選択アルゴリズム (TSA)-2005 standard。 この標準は、IEEE 802.1 データ センター ブリッジング (DCB) インターフェイスのフレームワークの一部です。

ネットワーク アダプターには、優先 TSA が施されている場合は、パケットの情報だけに基づいて転送に IEEE 802.1p の優先度レベルが指定された、パケットを選択します。 その結果より高い優先度レベルを持つパケットは常に低い優先度レベルを持つパケットを前に送信します。

ミニポート ドライバー NDIS を設定して、優先 TSA のサポートを指定する\_QOS\_機能\_STRICT\_TSA\_でサポートされている、**フラグ**メンバー[ **NDIS\_QOS\_機能**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_qos_capabilities)構造体。 ドライバーでは、この構造体を使用して、呼び出しの NDIS QoS と DCB の機能を登録します[ **NdisMSetMiniportAttributes**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismsetminiportattributes)します。

優先度レベルの詳細については、次を参照してください。 [IEEE 802.1p の優先度レベル](ieee-802-1p-priority-levels.md)します。

**注**  NDIS 6.30、以降、DCB の NDIS サービスの品質 (QoS) をサポートしているミニポート ドライバー インターフェイスは優先順位の厳密な TSA のサポートを提供する必要があります。

 

 

 






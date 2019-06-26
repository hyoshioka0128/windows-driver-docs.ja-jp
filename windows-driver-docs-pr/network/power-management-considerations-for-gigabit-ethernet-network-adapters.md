---
title: ギガビット イーサネット ネットワーク アダプターの電源管理の考慮事項
description: ギガビット イーサネット ネットワーク アダプターの電源管理に関する考慮事項
ms.assetid: f195d295-0a2a-4c44-a3b4-217dfad76826
keywords:
- 電源管理の WDK ネットワー キング、ギガビット イーサネット Nic
- ネットワーク インターフェイス カード WDK ネットワーク、電源の状態遷移
- Nic の WDK ネットワーク、電源の状態遷移
- Nic WDK ネットワー キング、ギガビット イーサネット Nic
- ネットワーク インターフェイス カード WDK ネットワー キング、ギガビット イーサネット Nic
- ギガビットのイーサネット Nic WDK ネットワーク
- 電源管理 WDK NDIS ミニポート、電源の状態遷移
- デバイスの電源状態が WDK ネットワーク
- WDK ネットワークの状態を電源します。
- WDK のネットワークの状態遷移の電源
- ウェイク アップ機能 WDK ネットワーク、電源の状態遷移
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4fffc18ddc49631b2fd491bf8adbbfa138e68803
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67383172"
---
# <a name="power-management-considerations-for-gigabit-ethernet-network-adapters"></a>ギガビット イーサネット ネットワーク アダプターの電源管理に関する考慮事項


ギガビット イーサネット ネットワーク アダプターが動作している 1000 メガ ビット/秒 (Mbps) で、多くの電力が供給を描画します。 このようなネットワーク アダプターは、低電力状態に遷移して、前に、ネットワーク アダプターが電力を描画するためのリンク速度が通常減少します。 短縮リンクの速度は、低電力状態に遷移するネットワーク アダプターを使用できます。 低電力状態に移行中に変化するリンクの速度が、中にネットワーク アダプターには通常しばらくの間のネットワーク接続が失われます。

逆に、ギガビット イーサネット ネットワーク アダプターは、低電力状態から完全にオン状態に遷移、ときに、ネットワーク アダプターのリンク速度が完全に operational 速度に向上します。 この移行中にネットワーク アダプターもしばらくの間の接続を失う可能性があります。

あるいは低電力状態からミニポート ドライバーの基になるネットワーク アダプターが移行されて、中にする必要がありますリンク速度を変更または接続の状態の変更もミニポートは示しません。 リンクの速度での変更を示す詳細については、次を参照してください。 [ **NDIS\_状態\_リンク\_状態**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-link-state)します。 接続の状態の変更を示す詳細については、次を参照してください。[接続の状態を示す](indicating-connection-status.md)します。

 

 






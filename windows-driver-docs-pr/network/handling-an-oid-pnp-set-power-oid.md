---
title: OID_PNP_SET_POWER OID の処理
description: OID_PNP_SET_POWER OID の処理
ms.assetid: 6140c772-57ba-47d3-b294-a2e2b2e3ccc7
keywords:
- OID_PNP_SET_POWER_OID
- ネットワーク インターフェイス カード WDK ネットワーク、電源の状態遷移
- ネットワーク アダプターの WDK ネットワーク、電源の状態遷移
- 電源管理 WDK NDIS ミニポート、電源の状態遷移
- デバイスの電源状態が WDK ネットワーク
- WDK ネットワークの状態を電源します。
- WDK のネットワークの状態遷移の電源
- ウェイク アップ機能 WDK ネットワーク、電源の状態遷移
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0d6cdbecc030ea7e6d3c079429b58efe49cd76ff
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67384395"
---
# <a name="handling-an-oidpnpsetpower-oid"></a>OID の処理\_PNP\_設定\_POWER OID





NDIS の OID 要求を送信する[OID\_PNP\_設定\_POWER](https://docs.microsoft.com/windows-hardware/drivers/network/oid-pnp-set-power)こと、ネットワーク アダプターが予想される遷移をスリープ状態を稼働状態またはスリープ状態からミニポート ドライバーに通知するには動作状態を状態です。 OID\_PNP\_設定\_POWER 要求の前に、 [OID\_PNP\_クエリ\_POWER](https://docs.microsoft.com/windows-hardware/drivers/network/oid-pnp-query-power)要求。

このセクションの内容:

[スリープ状態に遷移します。](transitioning-to-a-sleeping-state.md)

[稼働状態に遷移します。](transitioning-to-the-working-state.md)

 

 






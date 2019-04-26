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
ms.openlocfilehash: 3b2f607ba5ed502cc18ba821076dd7ca6624089a
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63349720"
---
# <a name="handling-an-oidpnpsetpower-oid"></a>OID の処理\_PNP\_設定\_POWER OID





NDIS の OID 要求を送信する[OID\_PNP\_設定\_POWER](https://msdn.microsoft.com/library/windows/hardware/ff569780)こと、ネットワーク アダプターが予想される遷移をスリープ状態を稼働状態またはスリープ状態からミニポート ドライバーに通知するには動作状態を状態です。 OID\_PNP\_設定\_POWER 要求の前に、 [OID\_PNP\_クエリ\_POWER](https://msdn.microsoft.com/library/windows/hardware/ff569778)要求。

このセクションの内容:

[スリープ状態に遷移します。](transitioning-to-a-sleeping-state.md)

[稼働状態に遷移します。](transitioning-to-the-working-state.md)

 

 






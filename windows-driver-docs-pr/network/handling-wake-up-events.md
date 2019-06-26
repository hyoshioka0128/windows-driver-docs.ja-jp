---
title: ウェイクアップ イベントの処理
description: ウェイクアップ イベントの処理
ms.assetid: 4989d5a4-158c-41db-ab2d-fc995b67a822
keywords:
- ウェイク アップ機能 WDK ネットワー キング、ウェイク アップのイベントの処理
- バスに固有のウェイク アップ行 WDK ネットワーク
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8823ff3c51a22d544424036b0165ca39701e91e9
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67381322"
---
# <a name="handling-wake-up-events"></a>ウェイクアップ イベントの処理





ミニポート ドライバーが NIC で検出されたウェイク アップ イベントを処理しません。 NIC は、有効なウェイク アップ イベントを検出すると、バスに固有のウェイク アップ行をアサートします。 電源マネージャーは、NDIS、応答、ミニポート ドライバーを送信しますこれを power IRP を送信し、 [OID\_PNP\_設定\_POWER](https://docs.microsoft.com/windows-hardware/drivers/network/oid-pnp-set-power)に NIC を配置するミニポート ドライバーを要求する OID、。highest-powered (D0) の状態。

 

 






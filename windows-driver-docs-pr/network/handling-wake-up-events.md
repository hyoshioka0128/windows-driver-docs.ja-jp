---
title: ウェイク アップのイベントの処理
description: ウェイク アップのイベントの処理
ms.assetid: 4989d5a4-158c-41db-ab2d-fc995b67a822
keywords:
- ウェイク アップ機能 WDK ネットワー キング、ウェイク アップのイベントの処理
- バスに固有のウェイク アップ行 WDK ネットワーク
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4ba0a88f668f1de6d2a43f1cf94d0f135bbf9927
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56561115"
---
# <a name="handling-wake-up-events"></a>ウェイク アップのイベントの処理





ミニポート ドライバーが NIC で検出されたウェイク アップ イベントを処理しません。 NIC は、有効なウェイク アップ イベントを検出すると、バスに固有のウェイク アップ行をアサートします。 電源マネージャーは、NDIS、応答、ミニポート ドライバーを送信しますこれを power IRP を送信し、 [OID\_PNP\_設定\_POWER](https://msdn.microsoft.com/library/windows/hardware/ff569780)に NIC を配置するミニポート ドライバーを要求する OID、。highest-powered (D0) の状態。

 

 






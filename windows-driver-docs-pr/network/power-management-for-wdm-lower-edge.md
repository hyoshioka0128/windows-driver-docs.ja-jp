---
title: WDM の下端の電源管理
description: WDM の下端の電源管理
ms.assetid: e4504206-b303-4623-bb10-a19acbcede03
keywords:
- NDIS WDM ミニポート ドライバー WDK ネットワーク、電源管理
- 下端の NDIS ミニポート ドライバー WDK ネットワーク、電源管理
- WDM 低い edge WDK ネットワーク、電源管理
- 電源管理の WDK ネットワー キング、NDIS WDM ミニポート ドライバー
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a938c6dc419ca9d6591015b73fe86c0b3d0a601b
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67386853"
---
# <a name="power-management-for-wdm-lower-edge"></a>WDM の下端の電源管理





NDIS は、すべてのプラグ アンド プレイ (PnP) および NDIS WDM ミニポート ドライバーの電源管理 Irp を処理します。 そのため、NDIS WDM ミニポート ドライバーは PnP および電源管理に Oid、」の説明に従って、デバイスの機能に基づく応答する必要があります[NDIS ミニポート ドライバーの電源管理](https://docs.microsoft.com/windows-hardware/drivers/network/power-management--ndis-6-0-and-ndis-6-1-)します。 これらの Oid の詳細については、次を参照してください。 [(NDIS 6.0 以降) の電源管理](https://docs.microsoft.com/windows-hardware/drivers/network/power-management--ndis-6-0-and-ndis-6-1-)します。

 

 






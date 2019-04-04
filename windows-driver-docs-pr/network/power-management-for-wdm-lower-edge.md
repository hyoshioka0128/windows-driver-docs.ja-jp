---
title: WDM 下端の電源管理
description: WDM 下端の電源管理
ms.assetid: e4504206-b303-4623-bb10-a19acbcede03
keywords:
- NDIS WDM ミニポート ドライバー WDK ネットワーク、電源管理
- 下端の NDIS ミニポート ドライバー WDK ネットワーク、電源管理
- WDM 低い edge WDK ネットワーク、電源管理
- 電源管理の WDK ネットワー キング、NDIS WDM ミニポート ドライバー
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 44259d0f3fa403ebf13adf5efac801013bf46734
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56530159"
---
# <a name="power-management-for-wdm-lower-edge"></a>WDM 下端の電源管理





NDIS は、すべてのプラグ アンド プレイ (PnP) および NDIS WDM ミニポート ドライバーの電源管理 Irp を処理します。 そのため、NDIS WDM ミニポート ドライバーは PnP および電源管理に Oid、」の説明に従って、デバイスの機能に基づく応答する必要があります[NDIS ミニポート ドライバーの電源管理](https://msdn.microsoft.com/library/windows/hardware/hh205399)します。 これらの Oid の詳細については、[(NDIS 6.0 以降) の電源管理](https://msdn.microsoft.com/library/windows/hardware/hh205399)を参照してください。

 

 






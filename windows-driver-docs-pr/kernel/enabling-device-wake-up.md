---
title: デバイス ウェイクアップの有効化
description: デバイス ウェイクアップの有効化
ms.assetid: 1c3b9ebc-cc77-4562-9c57-56f2c9a69772
keywords:
- Irp WDK の電源管理
- アクティブになるデバイス
- 電源管理のウェイク アップ機能 WDK
- デバイスのスリープ解除 ups WDK 電源管理
- IRP_MN_WAIT_WAKE
- IRP_MJ_POWER
- DEVICE_CAPABILITIES 構造体
- WDK カーネルの電源を復元します。
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: b48d4dfe950e7909bff5ec52ed259f3027241325
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67384947"
---
# <a name="enabling-device-wake-up"></a>デバイス ウェイクアップの有効化





デバイスは、ウェイク アップをサポートする場合、電源ポリシー所有者を有効にして、デバイスのウェイク アップを無効にすることである必要があります。 ドライバーにより、ウェイク アップを送信する[ **IRP\_MJ\_POWER** ](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-power)マイナー関数コードで要求を[ **IRP\_MN\_待機\_WAKE** ](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-wait-wake)以前送信を取り消すと、ウェイク アップを有効または無効に**IRP\_MN\_待機\_WAKE**します。 デバイスがある 1 つだけ**IRP\_MN\_待機\_WAKE**一度に保留中の要求。

そこからは、ウェイク アップ、およびシステム電源の状態、デバイスが、システムを起動できます通知デバイスの電源の状態、デバイスは、ウェイク アップをサポートするかどうかを確認するのにはドライバーによってチェックされます、 **SystemWake**、 **DeviceWake**、および **WakeFromD * * * x*内のメンバー、 [**デバイス\_機能**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ns-wdm-_device_capabilities)構造体。

有効にする方法の詳細については、無効化、およびドライバー、ウェイク アップ シグナルへの応答を参照してください[サポート デバイスがあるウェイク アップ機能](supporting-devices-that-have-wake-up-capabilities.md)します。

 

 





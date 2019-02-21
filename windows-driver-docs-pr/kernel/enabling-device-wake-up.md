---
title: デバイスのウェイク アップを有効にします。
description: デバイスのウェイク アップを有効にします。
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
ms.openlocfilehash: 4b2c1b7299c581b390a58e32e2825f8bc052aaa1
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56536432"
---
# <a name="enabling-device-wake-up"></a>デバイスのウェイク アップを有効にします。





デバイスは、ウェイク アップをサポートする場合、電源ポリシー所有者を有効にして、デバイスのウェイク アップを無効にすることである必要があります。 ドライバーにより、ウェイク アップを送信する[ **IRP\_MJ\_POWER** ](https://msdn.microsoft.com/library/windows/hardware/ff550784)マイナー関数コードで要求を[ **IRP\_MN\_待機\_WAKE** ](https://msdn.microsoft.com/library/windows/hardware/ff551766)以前送信を取り消すと、ウェイク アップを有効または無効に**IRP\_MN\_待機\_WAKE**します。 デバイスがある 1 つだけ**IRP\_MN\_待機\_WAKE**一度に保留中の要求。

そこからは、ウェイク アップ、およびシステム電源の状態、デバイスが、システムを起動できます通知デバイスの電源の状態、デバイスは、ウェイク アップをサポートするかどうかを確認するのにはドライバーによってチェックされます、 **SystemWake**、 **DeviceWake**、および **WakeFromD * * * x*内のメンバー、 [**デバイス\_機能**](https://msdn.microsoft.com/library/windows/hardware/ff543095)構造体。

有効にする方法の詳細については、無効化、およびドライバー、ウェイク アップ シグナルへの応答を参照してください[サポート デバイスがあるウェイク アップ機能](supporting-devices-that-have-wake-up-capabilities.md)します。

 

 





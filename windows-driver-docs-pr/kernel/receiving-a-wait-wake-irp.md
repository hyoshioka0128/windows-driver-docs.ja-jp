---
title: 待機/ウェイク IRP の受信
description: 待機/ウェイク IRP の受信
ms.assetid: 88fa7189-4897-484a-9cf4-b35e56e99d61
keywords:
- 電源管理の WDK カーネル、ウェイク アップ機能
- 外部ウェイク信号 WDK
- アクティブになるデバイス
- 電源管理のウェイク アップ機能 WDK
- デバイスのスリープ解除 ups WDK 電源管理
- IRP_MN_WAIT_WAKE
- 受信側の待機またはスリープ解除 Irp
- 待機/ウェイク Irp WDK の電源管理の受信
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: dee40b223b5127136f23b8d83e9b25185f12ce80
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67378739"
---
# <a name="receiving-a-waitwake-irp"></a>待機/ウェイク IRP の受信





すべての PnP ドライバーは IRP コードを少しで power Irp を受信する準備する必要があります[ **IRP\_MN\_待機\_WAKE**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-wait-wake)します。 ドライバーが待機/ウェイク IRP を処理する方法は、デバイス スタック、デバイスを制御し、元は、そのデバイスは、ウェイク アップをサポートしています。 特定の状態の種類内の位置によって異なります。

このセクションのトピックでは、この IRP がドライバーの種類とその待機/ウェイク サポートのレベルに基づいてを処理するためのガイドラインを提供します。

 

 





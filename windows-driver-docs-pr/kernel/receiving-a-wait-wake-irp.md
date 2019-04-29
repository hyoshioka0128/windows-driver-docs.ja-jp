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
ms.openlocfilehash: 335a7faa52469db06fee717ad1e67ea02c31b6f4
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63338505"
---
# <a name="receiving-a-waitwake-irp"></a>待機/ウェイク IRP の受信





すべての PnP ドライバーは IRP コードを少しで power Irp を受信する準備する必要があります[ **IRP\_MN\_待機\_WAKE**](https://msdn.microsoft.com/library/windows/hardware/ff551766)します。 ドライバーが待機/ウェイク IRP を処理する方法は、デバイス スタック、デバイスを制御し、元は、そのデバイスは、ウェイク アップをサポートしています。 特定の状態の種類内の位置によって異なります。

このセクションのトピックでは、この IRP がドライバーの種類とその待機/ウェイク サポートのレベルに基づいてを処理するためのガイドラインを提供します。

 

 





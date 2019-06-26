---
title: ウェイクアップ機能を備えたデバイスのサポート
description: ウェイクアップ機能を備えたデバイスのサポート
ms.assetid: 70b9d0af-c3d7-44dc-b11a-3274391508c5
keywords:
- 電源管理の WDK カーネル、ウェイク アップ機能
- 外部ウェイク信号 WDK
- アクティブになるデバイス
- 電源管理のウェイク アップ機能 WDK
- デバイスのスリープ解除 ups WDK 電源管理
- IRP_MN_WAIT_WAKE
- WDK カーネルの電源を復元します。
- Irp WDK の電源管理
- 待機/ウェイク Irp WDK 電源管理
- I/O 要求パケット WDK 電源管理
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1d2e12e28e1fbdda3170d91fac2d3b1c17acd20f
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67385115"
---
# <a name="supporting-devices-that-have-wake-up-capabilities"></a>ウェイクアップ機能を備えたデバイスのサポート





外部ウェイク信号に応答できるデバイスのドライバーが処理できる必要があります[ **IRP\_MN\_待機\_WAKE** ](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-wait-wake)要求 (*待機またはスリープ状態の解除Irp*)。 このようなデバイスの電源ポリシー所有者は、送信できる必要があります、 **IRP\_MN\_待機\_WAKE**要求。

通常、どのによりウェイク信号をアサートするデバイスは、デバイスの通常のサービス イベントではも。 たとえば、システムをスリープ解除するキーボードが発生する可能性があります、ユーザー入力は、キーボードとそのドライバーの通常イベントです。

このセクションの最初のトピック[待機またはスリープ解除操作の概要](overview-of-wait-wake-operation.md)、任意のドライバーの記述に役立つ情報が含まれています。 次の補足トピック処理に関する詳細情報を提供して待機/ウェイク Irp を送信します。

[待機/ウェイク IRP を受信](receiving-a-wait-wake-irp.md)

[待機/ウェイク IRP を送信します。](sending-a-wait-wake-irp.md)

[待機/ウェイク IRP のキャンセル](canceling-a-wait-wake-irp.md)

 

 





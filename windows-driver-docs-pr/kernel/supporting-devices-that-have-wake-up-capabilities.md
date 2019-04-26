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
ms.openlocfilehash: 96ca29d334f077081fd4143bd449aceade882e81
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63345436"
---
# <a name="supporting-devices-that-have-wake-up-capabilities"></a>ウェイクアップ機能を備えたデバイスのサポート





外部ウェイク信号に応答できるデバイスのドライバーが処理できる必要があります[ **IRP\_MN\_待機\_WAKE** ](https://msdn.microsoft.com/library/windows/hardware/ff551766)要求 (*待機またはスリープ状態の解除Irp*)。 このようなデバイスの電源ポリシー所有者は、送信できる必要があります、 **IRP\_MN\_待機\_WAKE**要求。

通常、どのによりウェイク信号をアサートするデバイスは、デバイスの通常のサービス イベントではも。 たとえば、システムをスリープ解除するキーボードが発生する可能性があります、ユーザー入力は、キーボードとそのドライバーの通常イベントです。

このセクションの最初のトピック[待機またはスリープ解除操作の概要](overview-of-wait-wake-operation.md)、任意のドライバーの記述に役立つ情報が含まれています。 次の補足トピック処理に関する詳細情報を提供して待機/ウェイク Irp を送信します。

[待機/ウェイク IRP を受信](receiving-a-wait-wake-irp.md)

[待機/ウェイク IRP を送信します。](sending-a-wait-wake-irp.md)

[待機/ウェイク IRP のキャンセル](canceling-a-wait-wake-irp.md)

 

 





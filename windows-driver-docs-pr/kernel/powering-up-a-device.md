---
title: デバイスの電源投入
description: デバイスの電源投入
ms.assetid: 115cc904-922d-447e-b221-cb3e489dd08d
keywords:
- I/O WDK 電源管理
- デバイスの電源 ups WDK カーネル
- WDK カーネルのデバイスの電源を入れる
- IRP_MN_SET_POWER
- 動作状態は、WDK の電源管理を返します
- デバイスの WDK の電源管理の有効化
- 自動電源 ups WDK カーネル
- WDK のカーネルの電源
- Irp WDK の電源管理
- スタートアップの電源管理の WDK カーネル
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8ed9ae34ef761b29f8a2794031be125f28765b1e
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63369134"
---
# <a name="powering-up-a-device"></a>デバイスの電源投入





バス ドライバーが、PnP は処理[ **IRP\_MN\_開始\_デバイス**](https://msdn.microsoft.com/library/windows/hardware/ff551749)で呼び出し、デバイスの電源をする必要があります、その子デバイスの 1 つの要求[**PoSetPowerState** ](https://msdn.microsoft.com/library/windows/hardware/ff559765)電源マネージャーにデバイスの電源状態を報告します。 デバイスの電源を入れては、デバイスのスタートアップの暗黙的な部分です。 デバイスの電源ポリシー所有者は送信しません、 [ **IRP\_MN\_設定\_POWER** ](https://msdn.microsoft.com/library/windows/hardware/ff551744)要求**PowerDeviceD0**、そのドライバー起動時にこれらの Irp を受信するのには期待できません。

電源の節約にデバイスを電源すると、そのドライバーする必要があります電源を入れます、I/O 要求が到着したとき。 この場合、デバイスの電源ポリシー所有者を送信する必要があります、 **IRP\_MN\_設定\_POWER**にデバイスを動作状態に戻ります。 IRP が完了したら、デバイスのドライバーは I/O キューを停止し、キューからの要求の処理を開始します。

 

 





---
title: NIC の起動
description: NIC の起動
ms.assetid: 8463edba-1502-44b7-a9bd-30763b9e7679
keywords:
- Nic の WDK ネットワーク、開始
- 以降、ネットワーク インターフェイス カード WDK ネットワーク
- プラグ アンド プレイ WDK NDIS ミニポート、NIC の開始
- starting NICs WDK networking
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 34b8b932b021ab2d59fde24fe91a5746c031e6b3
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67377557"
---
# <a name="starting-a-nic"></a>NIC の起動





次の手順では、NDIS が NIC の開始時に参加する方法について説明します。

1.  PnP マネージャーの問題、 [ **IRP\_MN\_開始\_デバイス**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-start-device)要求。 この IRP には PnP マネージャーによって NIC に割り当てられたリソースについての情報が含まれています

2.  NDIS セット、 [ **IoCompletion** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-io_completion_routine)ルーチンを渡します IRP\_MN\_開始\_通常は、次の最も低いドライバーにデバイス スタックとデバイスの要求バス ドライバー。 バス ドライバーが IRP を受信すると\_MN\_開始\_デバイス要求、バス ドライバーのデバイスに対しては、その開始操作を実行および完了した IRP を渡す\_MN\_開始\_デバイス要求は、デバイス スタックをバックアップします。

3.  NDIS が完了した IRP を受信すると\_MN\_開始\_デバイス要求 (つまり、NDIS の[ **DispatchPnP** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_dispatch)ルーチンは下位のすべてのドライバーの制御を取得しました。完了したら、IRP)、NDIS ミニポート ドライバーの呼び出す[ *MiniportInitializeEx* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_initialize)関数。

4.  場合、 *MiniportInitializeEx*返します NDIS\_状態\_成功すると、NDIS スケジュール イベントを呼び出す、 [ *ProtocolBindAdapterEx* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-protocol_bind_adapter_ex)レジストリ内のバインド情報で示されている、アダプターにバインドすることになっているすべてのプロトコル ドライバーの関数。 ミニポート ドライバーにバインディングに関する情報がないことに注意してください。

5.  NDIS IRP の完了\_MN\_開始\_デバイス要求。

 

 






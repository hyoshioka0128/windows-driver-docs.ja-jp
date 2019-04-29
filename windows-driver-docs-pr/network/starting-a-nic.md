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
ms.openlocfilehash: 7174bfbc053cd299ac1cd3dcc358170db86c1033
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63390633"
---
# <a name="starting-a-nic"></a>NIC の起動





次の手順では、NDIS が NIC の開始時に参加する方法について説明します。

1.  PnP マネージャーの問題、 [ **IRP\_MN\_開始\_デバイス**](https://msdn.microsoft.com/library/windows/hardware/ff551749)要求。 この IRP には PnP マネージャーによって NIC に割り当てられたリソースについての情報が含まれています

2.  NDIS セット、 [ **IoCompletion** ](https://msdn.microsoft.com/library/windows/hardware/ff548354)ルーチンを渡します IRP\_MN\_開始\_通常は、次の最も低いドライバーにデバイス スタックとデバイスの要求バス ドライバー。 バス ドライバーが IRP を受信すると\_MN\_開始\_デバイス要求、バス ドライバーのデバイスに対しては、その開始操作を実行および完了した IRP を渡す\_MN\_開始\_デバイス要求は、デバイス スタックをバックアップします。

3.  NDIS が完了した IRP を受信すると\_MN\_開始\_デバイス要求 (つまり、NDIS の[ **DispatchPnP** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_dispatch)ルーチンは下位のすべてのドライバーの制御を取得しました。完了したら、IRP)、NDIS ミニポート ドライバーの呼び出す[ *MiniportInitializeEx* ](https://msdn.microsoft.com/library/windows/hardware/ff559389)関数。

4.  場合、 *MiniportInitializeEx*返します NDIS\_状態\_成功すると、NDIS スケジュール イベントを呼び出す、 [ *ProtocolBindAdapterEx* ](https://msdn.microsoft.com/library/windows/hardware/ff570220)レジストリ内のバインド情報で示されている、アダプターにバインドすることになっているすべてのプロトコル ドライバーの関数。 ミニポート ドライバーにバインディングに関する情報がないことに注意してください。

5.  NDIS IRP の完了\_MN\_開始\_デバイス要求。

 

 






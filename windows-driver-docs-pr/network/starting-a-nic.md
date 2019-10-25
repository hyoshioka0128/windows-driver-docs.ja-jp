---
title: NIC の起動
description: NIC の起動
ms.assetid: 8463edba-1502-44b7-a9bd-30763b9e7679
keywords:
- Nic WDK ネットワーク、開始
- ネットワークインターフェイスカード WDK ネットワーク、開始
- WDK NDIS ミニポートのプラグアンドプレイ、開始 NIC
- Nic を開始する WDK ネットワーク
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2b23ebc59f1dd28c1f3e32535a2115cf9f9d403b
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841832"
---
# <a name="starting-a-nic"></a>NIC の起動





次の手順では、NDIS が NIC の開始時にどのように参加するかを説明します。

1.  PnP マネージャーは、 [ **\_デバイス要求を開始\_、IRP\_を実行**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-start-device)します。 この IRP には、PnP マネージャーによって NIC に割り当てられたリソースに関する情報が NDIS に通知されます。

2.  NDIS は[**Iocompletion**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-io_completion_routine)ルーチンを設定し、\_デバイスの要求を開始する\_、デバイススタックから次の最低のドライバー (通常はバスドライバー) に IRP\_渡します。 バスドライバーが、\_デバイスの要求を開始し\_IRP\_を受信すると、バスドライバーはデバイスで開始操作を実行し、完了した IRP\_完了\_デバイスの要求を開始\_デバイスのスタックをバックアップします。

3.  NDIS は、完了した IRP を受信したときに、\_デバイスの要求を開始\_\_(つまり、下位のすべてのドライバーが IRP で終了した後に NDIS の[**DispatchPnP**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch)ルーチンで制御が得られたとき)、ndis はミニポートドライバー[*を呼び出します。MiniportInitializeEx*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_initialize)関数。

4.  *MiniportInitializeEx*関数が NDIS\_STATUS\_SUCCESS を返した場合、ndis は、アダプターにバインドすることが想定されているすべてのプロトコルドライバーの[*Protocolbindadapterex*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-protocol_bind_adapter_ex)関数を呼び出すイベントをスケジュールします。レジストリ内のバインド情報。 ミニポートドライバーには、バインドに関する情報がありません。

5.  NDIS は\_デバイス要求の開始\_IRP\_完了します。

 

 






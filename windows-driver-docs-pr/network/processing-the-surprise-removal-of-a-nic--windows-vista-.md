---
title: NIC の突然の取り外しの処理 (Windows Vista)
description: NIC の突然の取り外しの処理 (Windows Vista)
ms.assetid: 940E6109-0A4C-4F4C-8201-F28BB789D7AE
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: fb1ce7b11d08007dac4678fd252a143c7e6b94f2
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843479"
---
# <a name="processing-the-surprise-removal-of-a-nic-windows-vista"></a>NIC の突然の取り外しの処理 (Windows Vista)





次の手順では、Windows Vista および Windows Server 2008 で NDIS が NIC の削除に関与するしくみについて説明します。

1.  PnP マネージャーは、 [**IRP の\_削除**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-surprise-removal)要求を\_して、NIC のデバイススタックに対して、予期しない IRP\_を発行します。

2.  NDIS がこの IRP を受け取ると、ドライバースタック内の NIC に接続されている最も低いフィルタードライバーの[*FilterNetPnPEvent*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-filter_net_pnp_event)関数を呼び出します。 この呼び出しで、NDIS は**NetEventQueryRemoveDevice**のイベントコードを指定します。

    **注**  NDIS は、 [*FilterNetPnPEvent*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-filter_net_pnp_event)関数のエントリポイントを提供するフィルタードライバーに対してのみこの手順を実行します。 フィルタードライバーは、 [**NdisFRegisterFilterDriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfregisterfilterdriver)関数を呼び出すときにこのエントリポイントを提供します。

     

3.  フィルタードライバーは、 [*FilterNetPnPEvent*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-filter_net_pnp_event)関数の呼び出しのコンテキスト内で、 [**NdisFNetPnPEvent**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfnetpnpevent)を呼び出して、ドライバースタック内の次のフィルタードライバーに**NetEventQueryRemoveDevice**イベントを転送する必要があります。 これにより、NDIS は、イベントコード**NetEventQueryRemoveDevice.** を使用して、そのフィルタードライバーの*FilterNetPnPEvent*関数を呼び出します。

    **注**  NDIS は、 [*FilterNetPnPEvent*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-filter_net_pnp_event)関数のエントリポイントをアドバタイズする、ドライバースタック内の次のフィルタードライバーに対してのみこの手順を実行します。

     

4.  ドライバースタック内の各フィルタードライバーは、スタック内の最上位のフィルタードライバーが NetEventQueryRemoveDevice を転送するまで、前の手順を繰り返し**ます。** 場合.

    この場合、NDIS は NIC にバインドされているすべてのプロトコルドライバーの[*ProtocolNetPnPEvent*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-protocol_net_pnp_event)関数を呼び出します。 この呼び出しで、NDIS は**NetEventQueryRemoveDevice**のイベントコードを指定します。

5.  ミニポートドライバーが正常に初期化された場合、NDIS は**NdisDevicePnPEventSurpriseRemoved**のイベントコードを使用して[*MiniportDevicePnPEventNotify*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_device_pnp_event_notify)関数を呼び出します。 ミニポートドライバーは、デバイスが物理的に取り外されていることを確認する必要があります。 ミニポートドライバーが NDIS WDM ドライバーの場合は、基になるバスドライバーに送信された保留中の Irp をキャンセルする必要があります。 ミニポートドライバーが正常に初期化されなかった場合は、処理が続行されます。

6.  NDIS は、IRP\_\_、突然\_削除要求をスタック内の次に小さいデバイスオブジェクトに送信します。 スタック内の次の下位のデバイスオブジェクトから、返された IRP\_\_が完了したことを予期しない\_削除要求を受け取った後、NDIS は予期しない\_の削除要求を実行して IRP\_を完了します。\_

7.  PnP マネージャーは、IRP\_を発行し、 [ **\_デバイス**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-remove-device)の要求を削除して、NIC のソフトウェア表現 (デバイスオブジェクトなど) を削除する\_します。

8.  NDIS は、次の手順を実行します。

    1.  NIC にバインドされているすべてのプロトコルドライバーを一時停止します。

    2.  NIC に接続されているすべてのフィルタードライバーを一時停止します。

    3.  NIC のミニポートドライバーを一時停止します。

    4.  NIC にバインドされているすべてのプロトコルドライバーの[*Protocolunbindadapterex*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-protocol_unbind_adapter_ex)関数を呼び出します。

    5.  NIC に接続されているすべてのフィルターモジュールの[*Filterdetach*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-filter_detach)関数を呼び出します。

9.  すべてのプロトコルドライバーとフィルタードライバーがバインド解除され、NIC から切断されると、NDIS はミニポートドライバーのミニ[*Porthaltex*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_halt)関数を呼び出します。 NDIS は、 *Miniporthaltex*の*HaltAction*パラメーターを**NdisHaltDeviceSurpriseRemoved**に設定します。

10. NDIS は、IRP\_、\_デバイス要求をスタック内の次に小さいデバイスオブジェクトに削除\_を送信します。

11. NDIS は、完了した IRP を受信し、スタック内の次に小さいデバイスオブジェクトから\_デバイス要求を削除\_\_、NIC に対して作成された機能デバイスオブジェクト (FDO) を破棄します。

 

 






---
title: NIC の突然の削除の処理 (Windows 7 以降)
description: NIC の突然の取り外しの処理 (Windows 7 以降のバージョン)
ms.assetid: D1C1C862-8AFF-490F-8A1D-362280196548
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6cff6dbf4cc777cb633af02882d9f515a818ea05
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843481"
---
# <a name="processing-the-surprise-removal-of-a-nic-windows-7-and-later-versions"></a>NIC の突然の取り外しの処理 (Windows 7 以降のバージョン)





Windows 7 と Windows Server 2008 R2 以降では、NDIS は、以前のバージョンの Windows とは異なる方法で、ネットワークインターフェイスカード (NIC) の突然の削除に関与する場合があります。 次の*いずれか*の条件に該当する場合、NDIS は変更された突然の削除手順を実行します。

-   オペレーティングシステムは、Windows 8/Windows Server 2012 以降です。
-   オペレーティングシステムは Windows 7 で、KB2471472 の修正プログラムがインストールされています。
-   オペレーティングシステムは Windows 7、ネットワークアダプターはモバイルブロードバンド (MBB) デバイスです。

これらの条件のいずれも満たされない場合、NDIS は以前のバージョンの Windows と同様に、突然の削除プロセスに参加します。 この手順の詳細については、「 [NIC の突然の削除の処理 (Windows Vista)](processing-the-surprise-removal-of-a-nic--windows-vista-.md)」を参照してください。

次の手順では、NDIS が NIC の突然の削除に関与する、改訂された方法について説明します。

1.  PnP マネージャーは、 [**IRP の\_削除**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-surprise-removal)要求を\_して、NIC のデバイススタックに対して、予期しない IRP\_を発行します。

2.  NDIS がこの IRP を受け取ると、ドライバースタック内の NIC に接続されている最も低いフィルタードライバーの[*FilterNetPnPEvent*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-filter_net_pnp_event)関数を呼び出します。 この呼び出しで、NDIS は**NetEventQueryRemoveDevice**のイベントコードを指定します。

    **注**  NDIS は、 [*FilterNetPnPEvent*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-filter_net_pnp_event)関数のエントリポイントを提供するフィルタードライバーに対してのみこの手順を実行します。 フィルタードライバーは、 [**NdisFRegisterFilterDriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfregisterfilterdriver)関数を呼び出すときにこのエントリポイントを提供します。

     

3.  フィルタードライバーは、 [*FilterNetPnPEvent*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-filter_net_pnp_event)関数の呼び出しのコンテキスト内で、 [**NdisFNetPnPEvent**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfnetpnpevent)を呼び出して、ドライバースタック内の次のフィルタードライバーに**NetEventQueryRemoveDevice**イベントを転送する必要があります。 これにより、NDIS は、イベントコード**NetEventQueryRemoveDevice**を使用して、そのフィルタードライバーの*FilterNetPnPEvent*関数を呼び出します。

    **注**  NDIS は、 [*FilterNetPnPEvent*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-filter_net_pnp_event)関数のエントリポイントをアドバタイズする、ドライバースタック内の次のフィルタードライバーに対してのみこの手順を実行します。

     

4.  ドライバースタック内の各フィルタードライバーは、スタック内の最上位のフィルタードライバーが**NetEventQueryRemoveDevice**イベントを転送するまで、前の手順を繰り返します。

    この場合、NDIS は NIC にバインドされているすべてのプロトコルドライバーの[*ProtocolNetPnPEvent*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-protocol_net_pnp_event)関数を呼び出します。 この呼び出しで、NDIS は**NetEventQueryRemoveDevice**のイベントコードを指定します。

5.  NDIS は、 **NdisDevicePnPEventSurpriseRemoved**のイベントコードを使用して[*MiniportDevicePnPEventNotify*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_device_pnp_event_notify)関数を呼び出します。 ミニポートドライバーは、デバイスが物理的に取り外されていることを確認する必要があります。 ミニポートドライバーが NDIS WDM ドライバーの場合は、基になるバスドライバーに送信された保留中の Irp をキャンセルする必要があります。

6.  NDIS は、次の手順を実行します。

    1.  NIC にバインドされているすべてのプロトコルドライバーを一時停止します。

    2.  NIC に接続されているすべてのフィルタードライバーを一時停止します。

    3.  NIC のミニポートドライバーを一時停止します。

    4.  NIC にバインドされているすべてのプロトコルドライバーの[*Protocolunbindadapterex*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-protocol_unbind_adapter_ex)関数を呼び出します。

    5.  NIC に接続されているすべてのフィルターモジュールの[*Filterdetach*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-filter_detach)関数を呼び出します。

7.  すべてのプロトコルドライバーとフィルタードライバーがバインド解除され、NIC から切断されると、NDIS はミニポートドライバーのミニ[*Porthaltex*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_halt)関数を呼び出します。 NDIS は、 *Miniporthaltex*の*HaltAction*パラメーターを**NdisHaltDeviceSurpriseRemoved**に設定します。

8.  NDIS は、IRP\_\_、突然\_削除要求をスタック内の次に小さいデバイスオブジェクトに送信します。 スタック内の次の下位のデバイスオブジェクトから、返された IRP\_\_が完了したことを予期しない\_削除要求を受け取った後、NDIS は予期しない\_の削除要求を実行して IRP\_を完了します。

9.  PnP マネージャーは、IRP\_を発行し、 [ **\_デバイス**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-remove-device)の要求を削除して、NIC のソフトウェア表現 (デバイスオブジェクトなど) を削除する\_します。

10. NDIS は、IRP\_、\_デバイス要求をスタック内の次に小さいデバイスオブジェクトに削除\_を送信します。

11. NDIS は、完了した IRP を受信し、スタック内の次に小さいデバイスオブジェクトから\_デバイス要求を削除\_\_、NIC に対して作成された機能デバイスオブジェクト (FDO) を破棄します。

 

 






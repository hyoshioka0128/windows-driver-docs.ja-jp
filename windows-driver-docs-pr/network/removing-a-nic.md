---
title: NIC の取り外し
description: NIC の取り外し
ms.assetid: eaa4b784-4375-465d-9ef5-99b38b7fd15a
keywords:
- Nic WDK ネットワーク、削除
- ネットワークインターフェイスカード WDK ネットワーク、削除
- WDK NDIS ミニポートのプラグアンドプレイ、NIC の削除
- Nic の削除 WDK ネットワーク
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 157c2499cbec6f322ffe09aed2faecd6480801b6
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842068"
---
# <a name="removing-a-nic"></a>NIC の取り外し





次の手順では、NDIS が NIC の削除に参加するしくみについて説明します。

1.  PnP マネージャーは、 [**IRP\_\_クエリ**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-query-remove-device)を実行し、コンピューターを中断せずに NIC を削除できるかどうかを照会\_\_デバイスの要求を削除します。

2.  NDIS がこの IRP を受け取ると、ドライバースタック内の NIC に接続されている最も低いフィルタードライバーの[*FilterNetPnPEvent*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-filter_net_pnp_event)関数を呼び出します。 この呼び出しで、NDIS は**NetEventQueryRemoveDevice**のイベントコードを指定します。

    **注**  NDIS は、 [*FilterNetPnPEvent*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-filter_net_pnp_event)関数のエントリポイントを提供するフィルタードライバーに対してのみこの手順を実行します。 フィルタードライバーは、 [**NdisFRegisterFilterDriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfregisterfilterdriver)関数を呼び出すときにこのエントリポイントをアドバタイズします。

     

3.  フィルタードライバーは、 [*FilterNetPnPEvent*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-filter_net_pnp_event)関数の呼び出しのコンテキスト内で、 [**NdisFNetPnPEvent**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfnetpnpevent)を呼び出して、ドライバースタック内の次のフィルタードライバーに**NetEventQueryRemoveDevice**イベントを転送する必要があります。 これにより、NDIS は、イベントコード**NetEventQueryRemoveDevice**を使用して、そのフィルタードライバーの*FilterNetPnPEvent*関数を呼び出します。

    **注**  NDIS は、 [*FilterNetPnPEvent*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-filter_net_pnp_event)関数のエントリポイントをアドバタイズする、ドライバースタック内の次のフィルタードライバーに対してのみこの手順を実行します。

     

4.  ドライバースタック内の各フィルタードライバーは、スタック内の最上位のフィルタードライバーが**NetEventQueryRemoveDevice**イベントを転送するまで、前の手順を繰り返します。

    この場合、NDIS は NIC にバインドされているすべてのプロトコルドライバーの[*ProtocolNetPnPEvent*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-protocol_net_pnp_event)関数を呼び出します。 この呼び出しで、NDIS は**NetEventQueryRemoveDevice**のイベントコードを指定します。

5.  プロトコルドライバーがエラー\_\_コード NetEventQueryRemoveDevice を返すことによってイベントが失敗した場合、 *ProtocolNetPnPEvent*からエラーが発生した場合は、ndis または PnP マネージャーがエラーを無視し、その後[**IRP\_完了\_クエリ\_\_デバイス**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-query-remove-device)要求を削除することができます。 したがって、プロトコルドライバーは**NetEventQueryRemoveDevice**イベントに失敗した場合でも、NIC の削除を処理できるように準備する必要があります。

6.  PnP マネージャーは、 [**irp\_を完了\_、\_デバイス**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-remove-device)の要求を削除して、NIC または[ **\_IRP**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-cancel-remove-device)に対するソフトウェアの表現 (デバイスオブジェクトなど) を削除するための\_をキャンセル\_削除する\_デバイスの要求を削除します。 \_デバイスの要求\_削除される IRP\_は、常に IRP\_が発生していないことに注意してください\_デバイスの要求を削除\_ます。\_

7.  PnP マネージャーが IRP\_を\_して、\_デバイスの要求の削除\_取り消す場合、NDIS はドライバースタック内の NIC に接続されている最も低いフィルタードライバーの[*FilterNetPnPEvent*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-filter_net_pnp_event)関数を呼び出します。 この呼び出しで、NDIS は**NetEventCancelRemoveDevice**のイベントコードを指定します。

    **注**  NDIS は、 [*FilterNetPnPEvent*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-filter_net_pnp_event)関数のエントリポイントを提供するフィルタードライバーに対してのみこの手順を実行します。

     

8.  フィルタードライバーは、 [*FilterNetPnPEvent*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-filter_net_pnp_event)関数の呼び出しのコンテキスト内で、 [**NdisFNetPnPEvent**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfnetpnpevent)を呼び出して、ドライバースタック内の次のフィルタードライバーに**NetEventCancelRemoveDevice**イベントを転送する必要があります。 これにより、NDIS は、イベントコード**NetEventCancelRemoveDevice**を使用して、そのフィルタードライバーの*FilterNetPnPEvent*関数を呼び出します。

    **注**  NDIS は、 [*FilterNetPnPEvent*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-filter_net_pnp_event)関数のエントリポイントをアドバタイズする、ドライバースタック内の次のフィルタードライバーに対してのみこの手順を実行します。

     

9.  ドライバースタック内の各フィルタードライバーは、スタック内の最上位のフィルタードライバーが**NetEventCancelRemoveDevice**イベントを転送するまで、前の手順を繰り返します。

    この場合、NDIS は NIC にバインドされているすべてのプロトコルドライバーの[*ProtocolNetPnPEvent*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-protocol_net_pnp_event)関数を呼び出します。 この呼び出しで、NDIS は**NetEventCancelRemoveDevice**のイベントコードを指定します。 このイベントコードは、削除シーケンスを終了します。

10. PnP マネージャーが、\_デバイスの要求\_削除する IRP\_発行した場合、NDIS は次の手順を実行します。

    1.  NIC にバインドされているすべてのプロトコルドライバーを一時停止します。

    2.  NIC に接続されているすべてのフィルタードライバーを一時停止します。

    3.  NIC のミニポートドライバーを一時停止します。

    4.  NIC にバインドされているすべてのプロトコルドライバーの[*Protocolunbindadapterex*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-protocol_unbind_adapter_ex)関数を呼び出します。

    5.  NIC に接続されているすべてのフィルターモジュールの[*Filterdetach*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-filter_detach)関数を呼び出します。

11. ミニポートドライバーが正常に初期化された場合、NDIS はミニポートドライバーのミニ[*Porthaltex*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_halt)関数を呼び出します。 NDIS は、 *Miniporthaltex*の*HaltAction*パラメーターを**NdisHaltDeviceDisabled**に設定します。

12. NDIS は、IRP\_、\_デバイス要求をスタック内の次に小さいデバイスオブジェクトに削除\_を送信します。

13. NDIS は、完了した IRP を受信し、スタック内の次に小さいデバイスオブジェクトから\_デバイス要求を削除\_\_、NIC に対して作成された機能デバイスオブジェクト (FDO) を破棄します。

 

 






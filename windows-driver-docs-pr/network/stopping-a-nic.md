---
title: NIC の停止
description: NIC の停止
ms.assetid: 033b45bd-fbe9-4a40-84e6-b9447370b17f
keywords:
- Nic WDK ネットワーク、停止
- ネットワークインターフェイスカード WDK ネットワーク、停止
- WDK NDIS ミニポートのプラグアンドプレイ、NIC の停止
- Nic の停止 WDK ネットワーク
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a4639540bad0cb7ed91b4e564983839f3c60ca13
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841820"
---
# <a name="stopping-a-nic"></a>NIC の停止





PnP マネージャーは、nic に割り当てられているハードウェアリソースを再構成または再調整できるように、NIC を停止します。 次の手順では、NDIS が NIC の停止に参加するしくみについて説明します。

1.  PnP マネージャーは、\_デバイスの要求を[**停止\_、IRP\_の\_クエリ**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-query-stop-device)を発行します。

2.  NDIS がこの IRP を受け取ると、ドライバースタック内の NIC に接続されている最も低いフィルタードライバーの[*FilterNetPnPEvent*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-filter_net_pnp_event)関数を呼び出します。 この呼び出しで、NDIS は**NetEventQueryRemoveDevice**のイベントコードを指定します。

    **注**  NDIS は、 [*FilterNetPnPEvent*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-filter_net_pnp_event)関数のエントリポイントを提供するフィルタードライバーに対してのみこの手順を実行します。 フィルタードライバーは、 [**NdisFRegisterFilterDriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfregisterfilterdriver)関数を呼び出すときにこのエントリポイントをアドバタイズします。

     

3.  フィルタードライバーは、 [*FilterNetPnPEvent*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-filter_net_pnp_event)関数の呼び出しのコンテキスト内で、 [**NdisFNetPnPEvent**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfnetpnpevent)を呼び出して、ドライバースタック内の次のフィルタードライバーに**NetEventQueryRemoveDevice**イベントを転送する必要があります。 これにより、NDIS は、イベントコード**NetEventQueryRemoveDevice**を使用して、そのフィルタードライバーの*FilterNetPnPEvent*関数を呼び出します。

    **注**  NDIS は、 [*FilterNetPnPEvent*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-filter_net_pnp_event)関数のエントリポイントをアドバタイズする、ドライバースタック内の次のフィルタードライバーに対してのみこの手順を実行します。

     

4.  ドライバースタック内の各フィルタードライバーは、スタック内の最上位のフィルタードライバーが**NetEventQueryRemoveDevice**イベントを転送するまで、前の手順を繰り返します。

    この場合、NDIS は NIC にバインドされているすべてのプロトコルドライバーの[*ProtocolNetPnPEvent*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-protocol_net_pnp_event)関数を呼び出します。 この呼び出しで、NDIS は**NetEventQueryRemoveDevice**のイベントコードを指定します。

5.  プロトコルドライバーが*ProtocolNetPnPEvent*からエラーコードを返すことによって**NetEventQueryRemoveDevice**イベントに失敗した場合、NDIS または PnP マネージャーはエラーを無視し、その後 IRP\_\_完了したクエリを成功させる可能性があり\_デバイス要求の\_を停止します。 したがって、プロトコルドライバーは**NetEventQueryRemoveDevice**イベントに失敗した場合でも、NIC の削除を処理できるように準備する必要があります。

6.  PnP マネージャーは、 [**irp\_** ](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-stop-device)を完了\_、デバイスを停止する\_デバイスの要求を停止するか、または[**irp\_完了\_デバイス**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-cancel-stop-device)の要求を中止して、保留中の停止をキャンセル\_ます。\_

7.  PnP マネージャーが IRP\_を発行し、\_デバイスの要求を停止\_\_キャンセルすると、NDIS はドライバースタック内の NIC に接続されている最も低いフィルタードライバーの[*FilterNetPnPEvent*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-filter_net_pnp_event)関数を呼び出します。 この呼び出しで、NDIS は**NetEventCancelRemoveDevice**のイベントコードを指定します。

    **注**  NDIS は、 [*FilterNetPnPEvent*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-filter_net_pnp_event)関数のエントリポイントを提供するフィルタードライバーに対してのみこの手順を実行します。

     

8.  フィルタードライバーは、 [*FilterNetPnPEvent*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-filter_net_pnp_event)関数の呼び出しのコンテキスト内で、 [**NdisFNetPnPEvent**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfnetpnpevent)を呼び出して、ドライバースタック内の次のフィルタードライバーに**NetEventCancelRemoveDevice**イベントを転送する必要があります。 これにより、NDIS は、イベントコード**NetEventCancelRemoveDevice**を使用して、そのフィルタードライバーの*FilterNetPnPEvent*関数を呼び出します。

    **注**  NDIS は、 [*FilterNetPnPEvent*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-filter_net_pnp_event)関数のエントリポイントをアドバタイズする、ドライバースタック内の次のフィルタードライバーに対してのみこの手順を実行します。

     

9.  ドライバースタック内の各フィルタードライバーは、スタック内の最上位のフィルタードライバーが**NetEventCancelRemoveDevice**イベントを転送するまで、前の手順を繰り返します。

    この場合、NDIS は NIC にバインドされているすべてのプロトコルドライバーの[*ProtocolNetPnPEvent*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-protocol_net_pnp_event)関数を呼び出します。 この呼び出しで、NDIS は**NetEventCancelRemoveDevice**のイベントコードを指定します。

10. PnP マネージャーが、\_デバイスの要求を停止\_て IRP\_を発行すると、NDIS は次の手順を実行します。

    1.  NIC にバインドされているすべてのプロトコルドライバーを一時停止します。

    2.  NIC に接続されているすべてのフィルタードライバーを一時停止します。

    3.  NIC のミニポートドライバーを一時停止します。

    4.  NIC にバインドされているすべてのプロトコルドライバーの[*Protocolunbindadapterex*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-protocol_unbind_adapter_ex)関数を呼び出します。

    5.  NIC に接続されているすべてのフィルターモジュールの[*Filterdetach*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-filter_detach)関数を呼び出します。

11. すべてのプロトコルドライバーとフィルタードライバーがバインド解除され、NIC から切断されると、NDIS はミニポートドライバーのミニ[*Porthaltex*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_halt)関数を呼び出します。 NDIS は、 *Miniporthaltex*の*HaltAction*パラメーターを**NdisHaltDeviceStopped**に設定します。

12. \_デバイスの要求を停止\_\_IRP を処理する場合、NDIS は、 *AddDevice*ルーチンが呼び出されたときに NIC 用に作成された機能デバイスオブジェクト (FDO) を破棄しません。 NDIS は、IRP\_を受け取った後にのみデバイスオブジェクトを破棄し、NIC に対する[ **\_デバイスの要求\_削除**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-remove-device)します。

    PnP マネージャーが IRP\_を実行し、NIC を再起動する\_デバイスを起動\_場合、NDIS は以前に NIC 用に作成された FDO を再利用します。 その後、NDIS によって NIC が再起動されます。 この手順の詳細については、「 [NIC を開始する](starting-a-nic.md)」を参照してください。

 

 






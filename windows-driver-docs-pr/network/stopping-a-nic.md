---
title: NIC の停止
description: NIC の停止
ms.assetid: 033b45bd-fbe9-4a40-84e6-b9447370b17f
keywords:
- Nic WDK ネットワー キング、停止しています
- 停止、ネットワーク インターフェイス カード WDK ネットワーク
- プラグ アンド プレイ WDK NDIS ミニポート、NIC を停止しています
- stopping NICs WDK networking
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: eec84918a712f7fec38aee14d2af9723f282dc7b
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67383594"
---
# <a name="stopping-a-nic"></a>NIC の停止





再構成または NIC に割り当てることがハードウェア リソースを再調整できるように、PnP マネージャーは、NIC を停止します。 次の手順では、NDIS が NIC の停止に参加する方法について説明します。

1.  PnP マネージャーの問題、 [ **IRP\_MN\_クエリ\_停止\_デバイス**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-query-stop-device)要求。

2.  NDIS は、この IRP を受信、呼び出し、 [ *FilterNetPnPEvent* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-filter_net_pnp_event)ドライバー スタック内の NIC に関連付けられている最も低いフィルター ドライバーの機能です。 この呼び出しで NDIS 指定のイベント コード**NetEventQueryRemoveDevice**します。

    **注**  NDIS は、エントリをアドバタイズするフィルター ドライバーのためだけにこの手順を実行、 [ *FilterNetPnPEvent* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-filter_net_pnp_event)関数。 呼び出すときに、フィルター ドライバーはこのエントリ ポイントをアドバタイズし、 [ **NdisFRegisterFilterDriver** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisfregisterfilterdriver)関数。

     

3.  呼び出しのコンテキスト内でその[ *FilterNetPnPEvent* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-filter_net_pnp_event)関数、フィルター ドライバーを呼び出す必要があります[ **NdisFNetPnPEvent** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisfnetpnpevent)を転送するには**NetEventQueryRemoveDevice**ドライバー スタックでは、次のフィルター ドライバーまでイベント。 これにより、NDIS フィルター ドライバーの呼び出しに*FilterNetPnPEvent*のイベント コードを使用して関数**NetEventQueryRemoveDevice**します。

    **注**  NDIS ドライバー スタックのエントリ ポイントを通知するには、次のフィルター ドライバーに対してのみこの手順を実行する、 [ *FilterNetPnPEvent* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-filter_net_pnp_event)関数。

     

4.  スタックの最上位フィルター ドライバーが転送されるまでドライバー スタック内の各フィルター ドライバーが、前の手順を繰り返し、 **NetEventQueryRemoveDevice**イベント。

    この場合、NDIS 呼び出し、 [ *ProtocolNetPnPEvent* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-protocol_net_pnp_event) NIC にバインドされているすべてのプロトコル ドライバーの機能 この呼び出しで NDIS 指定のイベント コード**NetEventQueryRemoveDevice**します。

5.  プロトコル ドライバーに失敗した場合、 **NetEventQueryRemoveDevice**イベントからのエラー コードを返すことによって*ProtocolNetPnPEvent*、NDIS または PnP マネージャーがエラーを無視し、後から成功、IRP\_MN\_クエリ\_停止\_デバイス要求。 プロトコル ドライバーが失敗した場合でも、NIC の削除を処理するためにプロトコル ドライバーを準備する必要があります、そのため、 **NetEventQueryRemoveDevice**イベント。

6.  PnP マネージャーの問題、 [ **IRP\_MN\_停止\_デバイス**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-stop-device)デバイスの停止を要求または[ **IRP\_MN\_キャンセル\_停止\_デバイス**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-cancel-stop-device)保留中の停止のキャンセルを要求します。

7.  PnP マネージャー IRP が発行された場合\_MN\_キャンセル\_停止\_デバイス要求、NDIS 呼び出し、 [ *FilterNetPnPEvent* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-filter_net_pnp_event)最下位の関数ドライバー スタック内の NIC に関連付けられているフィルター ドライバー。 この呼び出しで NDIS 指定のイベント コード**NetEventCancelRemoveDevice**します。

    **注**  NDIS は、エントリをアドバタイズするフィルター ドライバーのためだけにこの手順を実行、 [ *FilterNetPnPEvent* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-filter_net_pnp_event)関数。

     

8.  呼び出しのコンテキスト内でその[ *FilterNetPnPEvent* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-filter_net_pnp_event)関数、フィルター ドライバーを呼び出す必要があります[ **NdisFNetPnPEvent** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisfnetpnpevent)を転送するには**NetEventCancelRemoveDevice**ドライバー スタックでは、次のフィルター ドライバーまでイベント。 これにより、NDIS フィルター ドライバーの呼び出しに*FilterNetPnPEvent*のイベント コードを使用して関数**NetEventCancelRemoveDevice**します。

    **注**  NDIS ドライバー スタックのエントリ ポイントを通知するには、次のフィルター ドライバーに対してのみこの手順を実行する、 [ *FilterNetPnPEvent* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-filter_net_pnp_event)関数。

     

9.  スタックの最上位フィルター ドライバーが転送されるまでドライバー スタック内の各フィルター ドライバーが、前の手順を繰り返し、 **NetEventCancelRemoveDevice**イベント。

    この場合、NDIS 呼び出し、 [ *ProtocolNetPnPEvent* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-protocol_net_pnp_event) NIC にバインドされているすべてのプロトコル ドライバーの機能 この呼び出しで NDIS 指定のイベント コード**NetEventCancelRemoveDevice**します。

10. PnP マネージャーが IRP を発行する場合\_MN\_停止\_デバイス要求と、NDIS は、次の手順を実行します。

    1.  NIC にバインドされているすべてのプロトコル ドライバーが一時停止します

    2.  NIC に関連付けられているすべてのフィルター ドライバーが一時停止します

    3.  NIC のミニポート ドライバーが一時停止します

    4.  呼び出す、 [ *ProtocolUnbindAdapterEx* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-protocol_unbind_adapter_ex) NIC にバインドされているすべてのプロトコル ドライバーの機能

    5.  呼び出す、 [ *FilterDetach* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-filter_detach) NIC に関連付けられているすべてのフィルター モジュールの関数

11. NDIS ミニポート ドライバーを呼び出すすべてのプロトコルとフィルター ドライバーはバインドされていないし、NIC からデタッチ、 [ *MiniportHaltEx* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_halt)関数。 NDIS セット、 *HaltAction*パラメーターの*MiniportHaltEx*に**NdisHaltDeviceStopped**します。

12. IRP の処理時に\_MN\_停止\_NDIS は NIC 用に作成する機能のデバイス オブジェクト (FDO) を破棄していないデバイスで要求時に、 *AddDevice*ルーチンが呼び出されました。 NDIS は、受信した後にのみデバイス オブジェクトを破棄する[ **IRP\_MN\_削除\_デバイス**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-remove-device) nic 要求

    PnP マネージャー IRP が発行された場合\_MN\_開始\_NDIS、NIC を再起動するデバイスが NIC に既に作成されている FDO を再利用 NDIS は NIC を再起動し、 この手順の詳細については、次を参照してください。[開始 NIC](starting-a-nic.md)します。

 

 






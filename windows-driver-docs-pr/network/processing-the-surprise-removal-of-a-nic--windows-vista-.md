---
title: NIC の突然の取り外しの処理 (Windows Vista)
description: NIC の突然の取り外しの処理 (Windows Vista)
ms.assetid: 940E6109-0A4C-4F4C-8201-F28BB789D7AE
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 998e3bf52aa6adc6119c5103c8d2d580f38b383e
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67385468"
---
# <a name="processing-the-surprise-removal-of-a-nic-windows-vista"></a>NIC の突然の取り外しの処理 (Windows Vista)





次の手順では、NDIS が Windows Vista および Windows Server 2008 では、NIC の突然の取り外しに参加する方法について説明します。

1.  PnP マネージャーの問題、 [ **IRP\_MN\_突然\_削除**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-surprise-removal) NIC デバイス スタックへの要求

2.  NDIS は、この IRP を受信、呼び出し、 [ *FilterNetPnPEvent* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-filter_net_pnp_event)ドライバー スタック内の NIC に関連付けられている最も低いフィルター ドライバーの機能です。 この呼び出しで NDIS 指定のイベント コード**NetEventQueryRemoveDevice**します。

    **注**  NDIS は、エントリをアドバタイズするフィルター ドライバーのためだけにこの手順を実行、 [ *FilterNetPnPEvent* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-filter_net_pnp_event)関数。 呼び出すときに、フィルター ドライバーはこのエントリ ポイントを提供、 [ **NdisFRegisterFilterDriver** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisfregisterfilterdriver)関数。

     

3.  呼び出しのコンテキスト内でその[ *FilterNetPnPEvent* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-filter_net_pnp_event)関数、フィルター ドライバーを呼び出す必要があります[ **NdisFNetPnPEvent** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisfnetpnpevent)を転送するには**NetEventQueryRemoveDevice**ドライバー スタックでは、次のフィルター ドライバーまでイベント。 これにより、NDIS フィルター ドライバーの呼び出しに*FilterNetPnPEvent*のイベント コードを使用して関数**NetEventQueryRemoveDevice。** します。

    **注**  NDIS ドライバー スタックのエントリ ポイントを通知するには、次のフィルター ドライバーに対してのみこの手順を実行する、 [ *FilterNetPnPEvent* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-filter_net_pnp_event)関数。

     

4.  スタックの最上位フィルター ドライバーが転送されるまでドライバー スタック内の各フィルター ドライバーが、前の手順を繰り返し、 **NetEventQueryRemoveDevice します。** イベントです。

    この場合、NDIS 呼び出し、 [ *ProtocolNetPnPEvent* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-protocol_net_pnp_event) NIC にバインドされているすべてのプロトコル ドライバーの機能 この呼び出しで NDIS 指定のイベント コード**NetEventQueryRemoveDevice。** します。

5.  NDIS を呼び出す場合は、ミニポート ドライバーが正常に初期化すると、 [ *MiniportDevicePnPEventNotify* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_device_pnp_event_notify)のイベント コードを使用して関数**NdisDevicePnPEventSurpriseRemoved**. ミニポート ドライバーは、デバイスが物理的に削除されたことに注意してください。 ミニポート ドライバーが、NDIS WDM ドライバーの場合基になるバス ドライバーに送信された保留中の Irp をキャンセルにする必要があります。 かどうか、ミニポート ドライバーが正常に初期化されていません、処理を続行します。

6.  NDIS 送信 IRP\_MN\_突然\_スタック内の次の下位のデバイス オブジェクトを削除要求。 返される IRP を受信した後\_MN\_突然\_NDIS IRP が完了すると、スタックで、次の下位のデバイスからの削除要求オブジェクト\_MN\_突然\_削除要求。

7.  PnP マネージャーの問題、 [ **IRP\_MN\_削除\_デバイス**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-remove-device) nic ソフトウェア表現 (デバイス オブジェクト、およびなど) の削除を要求する

8.  NDIS は、次の手順を実行します。

    1.  NIC にバインドされているすべてのプロトコル ドライバーが一時停止します

    2.  NIC に関連付けられているすべてのフィルター ドライバーが一時停止します

    3.  NIC のミニポート ドライバーが一時停止します

    4.  呼び出す、 [ *ProtocolUnbindAdapterEx* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-protocol_unbind_adapter_ex) NIC にバインドされているすべてのプロトコル ドライバーの機能

    5.  呼び出す、 [ *FilterDetach* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-filter_detach) NIC に関連付けられているすべてのフィルター モジュールの関数

9.  NDIS ミニポート ドライバーを呼び出すすべてのプロトコルとフィルター ドライバーはバインドされていないし、NIC からデタッチ、 [ *MiniportHaltEx* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_halt)関数。 NDIS セット、 *HaltAction*パラメーターの*MiniportHaltEx*に**NdisHaltDeviceSurpriseRemoved**します。

10. NDIS 送信 IRP\_MN\_削除\_スタックの次のような低いデバイス オブジェクトへのデバイス要求。

11. NDIS が完了した IRP を受信すると\_MN\_削除\_NDIS 破棄 NIC 用に作成する機能のデバイス オブジェクト (FDO) スタックでは、[次へ] の下のデバイスからのデバイス要求オブジェクト

 

 






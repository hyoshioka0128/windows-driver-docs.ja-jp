---
title: IRP_MN_CANCEL_REMOVE_DEVICE 要求の処理
description: IRP_MN_CANCEL_REMOVE_DEVICE 要求の処理
ms.assetid: 3382c47d-6ac8-409e-b558-ad2f2ae83715
keywords:
- IRP_MN_CANCEL_REMOVE_DEVICE
- 誤ったキャンセルと削除要求 PnP WDK
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3577ee383671247ae468f2c3a363a79a30252cf9
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63359801"
---
# <a name="handling-an-irpmncancelremovedevice-request"></a>IRP の処理\_MN\_キャンセル\_削除\_デバイス要求





応答、 [ **IRP\_MN\_キャンセル\_削除\_デバイス**](https://msdn.microsoft.com/library/windows/hardware/ff550823)要求の場合は、デバイスの状態にデバイスを返す必要がありますのドライバー受信する前に、 **IRP\_MN\_クエリ\_削除\_デバイス**要求。 通常、ドライバーは、開始状態へのデバイスを返します。

送信するだけでなく、 **IRP\_MN\_キャンセル\_削除\_デバイス**デバイス、PnP マネージャーに送信します IRP デバイスの取り外し関係では、存在する場合。 PnP マネージャーでは、デバイスの子にキャンセルと削除 IRP も送信します。

PnP マネージャーでは、いずれかを呼び出す**EventCategoryTargetDeviceChange**通知コールバックの後、 **IRP\_MN\_キャンセル\_削除\_デバイス**要求を完了します。 このようなコールバックは、呼び出すことによって、デバイスに登録された[ **IoRegisterPlugPlayNotification**](https://msdn.microsoft.com/library/windows/hardware/ff549526)します。 PnP マネージャーも呼び出して登録されているすべてのユーザー モード コンポーネントのような通知を呼び出して**RegisterDeviceNotification**します。

**IRP\_MN\_キャンセル\_削除\_デバイス**デバイスの親のバス ドライバー、続いてデバイス スタックの各以上のドライバーに要求を最初に処理する必要があります。 ドライバーのハンドルの Irp の削除、 [ *DispatchPnP* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_dispatch)ルーチン。

ドライバーの処理、 **IRP\_MN\_キャンセル\_削除\_デバイス**要求は、次のようなプロシージャを使ってその*DispatchPnP*ルーチン。

1.  関数またはフィルター ドライバーでは、下位のドライバーには、再起動操作が完了するまで、デバイスの再起動を延期します。

    関数またはフィルター ドライバーの設定、 [ *IoCompletion* ](https://msdn.microsoft.com/library/windows/hardware/ff548354) 、日常的なパス、 **IRP\_MN\_キャンセル\_削除\_デバイス**デバイス スタックを下のすべてのドライバーが IRP に完了するまで、その再起動操作を延期します。 (を参照してください[下位のドライバーが完了するまで、PnP IRP の処理を延期する](postponing-pnp-irp-processing-until-lower-drivers-finish.md))。

2.  下位のドライバーが完了すると、以前の PnP 状態、デバイスを返します。

    ドライバーがデバイスを受信する前の状態に戻す、 **IRP\_MN\_クエリ\_削除\_デバイス**要求。 通常、ドライバーは、開始状態へのデバイスを返します。 正確な操作は、デバイスとドライバーによって異なります。

    デバイスの電源ポリシー所有者 (関数ドライバーでは通常) 場合、ウェイク アップのデバイスは既に有効、送信、 [ **IRP\_MN\_待機\_WAKE** ](https://msdn.microsoft.com/library/windows/hardware/ff551766)ウェイク アップを再度有効にする要求です。 参照してください[電源管理](implementing-power-management.md)詳細についてはします。

3.  設定**Irp -&gt;IoStatus.Status**ステータス\_成功の IRP の完了と[ **IoCompleteRequest**](https://msdn.microsoft.com/library/windows/hardware/ff548343)。

    同様に、PnP IRP では、バス ドライバーは IRP を完了します。

    関数またはフィルター ドライバーも完了すると、IRP では、ここでため、ドライバーの*IoCompletion*ルーチン完了状態を返すことによって処理が中断\_詳細\_処理\_必須。

    ドライバーは、この IRP が成功する必要があります。 任意のドライバーには、この IRP が失敗した場合、デバイスは一貫性のない状態のままです。

ドライバーは、デバイスが開始され、アクティブなときに、誤ったキャンセルと削除の要求にすることがあります。 これが行われる、たとえば、ドライバー (またはデバイス履歴の上位にドライバー) が失敗した場合、 **IRP\_MN\_クエリ\_削除\_デバイス**要求。 デバイスが開始され、アクティブのときは、ドライバーでは単にデバイスの誤ったキャンセルと削除の要求が成功します。

 

 





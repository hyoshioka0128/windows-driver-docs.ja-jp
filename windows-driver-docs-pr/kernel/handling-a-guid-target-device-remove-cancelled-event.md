---
title: GUID_TARGET_DEVICE_REMOVE_CANCELLED イベントの処理
description: GUID_TARGET_DEVICE_REMOVE_CANCELLED イベントの処理
ms.assetid: 19fe012b-3ed0-4356-999b-79b1d08dfbd6
keywords:
- 通知 WDK PnP、ターゲット デバイスの変更
- ターゲット デバイスの変更通知 PnP WDK
- EventCategoryTargetDeviceChange 通知
- GUID_TARGET_DEVICE_REMOVE_CANCELLED
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: c3c8adea938b74a4c7f9eddfcfacf85c0f198dff
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67385251"
---
# <a name="handling-a-guidtargetdeviceremovecancelled-event"></a>GUID の処理\_ターゲット\_デバイス\_削除\_キャンセル イベント





場合、 [ **IRP\_MN\_クエリ\_削除\_デバイス**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-query-remove-device) PnP マネージャー送信要求に失敗した、 [ **IRP\_MN\_キャンセル\_削除\_デバイス**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-cancel-remove-device) IRP デバイスのドライバーをします。 キャンセルと削除 IRP が正常に完了した後、PnP マネージャーは、任意の通知に登録するコールバック ルーチン**EventCategoryTargetDeviceChange**デバイスにします。 PnP マネージャーを指定します、 *NotificationStructure*.**イベント**GUID の\_ターゲット\_デバイス\_削除\_キャンセルします。

GUID を処理するときに\_ターゲット\_デバイス\_削除\_CANCELLED のイベント通知のコールバック ルーチンをする必要があります。

-   ターゲット デバイスの通知を登録してください。

    ドライバーにクエリの削除通知に対する応答で以前登録ハンドルが閉じているため、ドライバーは新しいハンドルを開く必要があります。 ドライバーが必要です。

    1.  削除での登録が古い[ **IoUnregisterPlugPlayNotification**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iounregisterplugplaynotification)します。

    2.  デバイスへの新しいハンドルを開きます。

    3.  通知を使用して、新しいハンドルの再登録**IoRegisterPlugPlayNotification**します。

 

 





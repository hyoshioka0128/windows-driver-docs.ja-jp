---
title: GUID_TARGET_DEVICE_REMOVE_CANCELLED イベントの処理
description: GUID_TARGET_DEVICE_REMOVE_CANCELLED イベントの処理
ms.assetid: 19fe012b-3ed0-4356-999b-79b1d08dfbd6
keywords:
- 通知 WDK PnP、ターゲットデバイスの変更
- ターゲットデバイスの変更通知の WDK PnP
- Eventカテゴリ Targetdevicechange notification
- GUID_TARGET_DEVICE_REMOVE_CANCELLED
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: cd7c54ded519fcecbff386e5d22539d2ad267a69
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72836667"
---
# <a name="handling-a-guid_target_device_remove_cancelled-event"></a>\_ターゲット\_デバイスを処理して\_取り消されたイベントを削除\_





[**Irp\_\_クエリ\_削除\_デバイス**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-query-remove-device)の要求が失敗した場合、PnP マネージャーは、デバイスのドライバーに対して\_デバイスの IRP の削除を\_して、 [**irp\_** ](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-cancel-remove-device)を正常に送信します。 取り消しの削除の IRP が正常に完了すると、デバイス上の**Eventカテゴリ Targetdevicechange**に登録されている通知コールバックルーチンが PnP マネージャーによって呼び出されます。 PnP マネージャーは*Notificationstructure*を指定します。GUID\_ターゲット\_デバイス\_削除\_取り消された**イベント**。

GUID\_ターゲット\_デバイスを処理するときに、取り消されたイベント\_\_削除する場合、通知コールバックルーチンは次のことを行う必要があります。

-   ターゲットデバイスの通知を再登録します。

    ドライバーは、クエリ削除通知への応答として前の登録ハンドルを閉じたため、ドライバーは新しいハンドルを開く必要があります。 ドライバーは次のことを行う必要があります。

    1.  [**IoUnregisterPlugPlayNotification**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iounregisterplugplaynotification)を使用して古い登録を削除します。

    2.  デバイスへの新しいハンドルを開きます。

    3.  **IoRegisterPlugPlayNotification**を使用して新しいハンドルで通知を再登録します。

 

 





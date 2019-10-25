---
title: GUID_TARGET_DEVICE_REMOVE_COMPLETE イベントの処理
description: GUID_TARGET_DEVICE_REMOVE_COMPLETE イベントの処理
ms.assetid: 7f20faae-b5ef-4a64-9150-bff14b04aaa4
keywords:
- 通知 WDK PnP、ターゲットデバイスの変更
- ターゲットデバイスの変更通知の WDK PnP
- Eventカテゴリ Targetdevicechange notification
- GUID_TARGET_DEVICE_REMOVE_COMPLETE
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 26677ce4388df92ca279679c871eec0d51db16ab
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838675"
---
# <a name="handling-a-guid_target_device_remove_complete-event"></a>\_デバイスの GUID\_ターゲットの処理\_\_完了イベントの削除





PnP マネージャーが Irp\_を送信して、デバイスのドライバーに\_デバイスの irp を[**削除\_** ](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-remove-device)する前に、pnp マネージャーは**Eventカテゴリ targetdevicechange**に登録されているカーネルモード通知コールバックルーチンを呼び出します。デバイス。 PnP マネージャーは*Notificationstructure*を指定します。\_ターゲット\_デバイス\_削除\_完了した GUID の**イベント**。

GUID\_ターゲット\_デバイスを処理して\_完了イベントを削除\_場合、通知コールバックルーチンは次の操作を行う必要があります。

-   デバイスの通知登録を削除します。

    デバイスは削除されているため、ドライバーは[**IoUnregisterPlugPlayNotification**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iounregisterplugplaynotification)を呼び出して通知登録を削除します。

    デバイスはコンピューター上に物理的に存在する可能性がありますが、すべてのデバイスオブジェクトが削除されているため、デバイスを使用できません。

-   ドライバーが前回のクエリ削除通知を受信しなかった場合は、驚くべき削除処理を実行します。

    デバイスが突然削除された場合、PnP マネージャーは、前のクエリ削除通知を使用せずに、登録されているドライバーを削除完了通知に送信します。 この場合、ドライバーは、デバイスへのハンドルのクローズ、ファイルオブジェクトへの未処理の参照の削除など、必要なクリーンアップを実行する必要があります。

 

 





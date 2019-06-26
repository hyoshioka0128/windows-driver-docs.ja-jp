---
title: GUID_TARGET_DEVICE_REMOVE_COMPLETE イベントの処理
description: GUID_TARGET_DEVICE_REMOVE_COMPLETE イベントの処理
ms.assetid: 7f20faae-b5ef-4a64-9150-bff14b04aaa4
keywords:
- 通知 WDK PnP、ターゲット デバイスの変更
- ターゲット デバイスの変更通知 PnP WDK
- EventCategoryTargetDeviceChange 通知
- GUID_TARGET_DEVICE_REMOVE_COMPLETE
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: a66256d99e32d2de03c1cb49147aa77fd323257d
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67385246"
---
# <a name="handling-a-guidtargetdeviceremovecomplete-event"></a>GUID の処理\_ターゲット\_デバイス\_削除\_完了イベント





PnP マネージャーに送信する前に、 [ **IRP\_MN\_削除\_デバイス**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-remove-device) IRP のデバイス ドライバーを PnP マネージャーが、カーネル モードの通知コールバックを呼び出す登録ルーチン**EventCategoryTargetDeviceChange**デバイスにします。 PnP マネージャーを指定します、 *NotificationStructure*.**イベント**GUID の\_ターゲット\_デバイス\_削除\_完了します。

GUID を処理するときに\_ターゲット\_デバイス\_削除\_完了のイベント通知のコールバック ルーチンをする必要があります。

-   デバイスの通知の登録を削除します。

    デバイスが削除されているので、ドライバーは呼び出し[ **IoUnregisterPlugPlayNotification** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iounregisterplugplaynotification)通知登録を削除します。

    デバイスが、コンピューターに物理的に存在する可能性がありますが、すべてのデバイス オブジェクトが削除されているし、デバイスが使用するために使用できません。

-   ドライバーは、前のクエリの削除通知を受信しませんでした突然削除処理を実行します。

    デバイスが突然削除された場合は、PnP マネージャーは以前のクエリと削除の通知なしの削除完了の通知登録済みのドライバーを送信します。 この場合、ドライバーは、デバイスへのすべてのハンドルを閉じたり、ファイル オブジェクトに未解決の参照を削除するなど、必要なクリーンアップを実行するは。

 

 





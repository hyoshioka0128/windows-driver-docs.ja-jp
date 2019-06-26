---
title: デバイス インターフェイス変更の通知登録
description: デバイス インターフェイス変更の通知登録
ms.assetid: 680e4c5c-dac6-41b1-b754-aee782145ed0
keywords:
- WDK PnP、通知デバイス インターフェイスの変更
- EventCategoryDeviceInterfaceChange 通知
- デバイス インターフェイスの変更通知 PnP WDK
- デバイス インターフェイスの変更通知を登録します。
- IoRegisterPlugPlayNotification
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6f1633ee6fae1e21fe51460221ba1c2bc1ab1df5
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67373459"
---
# <a name="registering-for-device-interface-change-notification"></a>デバイス インターフェイス変更の通知登録





ドライバーでは、呼び出すことによってデバイス インターフェイスの削除と到着のイベントの通知を登録します。 [ **IoRegisterPlugPlayNotification**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ioregisterplugplaynotification)します。

次の情報は、デバイス インターフェイスの変更通知のこのルーチンの呼び出しに適用されます。

-   指定、*によって*の**EventCategoryDeviceInterfaceChange**します。

-   *EventCategoryData*デバイス インターフェイスのクラスの GUID をポイントする必要があります。

    インターフェイス クラスの GUID は通常、インターフェイス構造体、定数、およびなどを含むヘッダー ファイルで定義されます。

-   指定、 *EventCategoryFlags* PNPNOTIFY の\_デバイス\_インターフェイス\_INCLUDE\_既存\_インターフェイス。

    このフラグを登録する PnP マネージャーに指示、 *CallbackRoutine*の将来のデバイスのインターフェイスの出会いと別れを呼び出すと、指定したクラスの*CallbackRoutine*いずれかが即座に既にアクティブにされている関連するデバイスのインターフェイス。

    ドライバーが呼び出せる[ **IoGetDeviceInterfaces** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iogetdeviceinterfaces)ルーチンが、このフラグを設定、フラグを使用せず、特定のクラスの既存のインターフェイスの一覧を取得し、そのコールバックを登録する方が簡単で、回避できます、潜在的なタイミングの問題。

-   ドライバーの定義を指定*コンテキスト*、必要に応じて、PnP マネージャーは、コールバック ルーチンに渡されます。

デバイス インターフェイス着荷通知に対する応答でデバイスを識別するハンドルを開いたドライバーに登録する必要があります**EventCategoryTargetDeviceChange**デバイス上のイベント。 (を参照してください[PnP ターゲット デバイスの変更通知を使用して](using-pnp-target-device-change-notification.md))。

ドライバーは、呼び出すことによって通知登録をキャンセル[ **IoUnregisterPlugPlayNotification** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iounregisterplugplaynotification)で、 *NotificationEntry*によって返される**IoRegisterPlugPlayNotification**します。

 

 





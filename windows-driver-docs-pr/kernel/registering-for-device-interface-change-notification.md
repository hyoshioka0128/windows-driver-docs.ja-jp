---
title: デバイス インターフェイスの変更通知を登録します。
description: デバイス インターフェイスの変更通知を登録します。
ms.assetid: 680e4c5c-dac6-41b1-b754-aee782145ed0
keywords:
- WDK PnP、通知デバイス インターフェイスの変更
- EventCategoryDeviceInterfaceChange 通知
- デバイス インターフェイスの変更通知 PnP WDK
- デバイス インターフェイスの変更通知を登録します。
- IoRegisterPlugPlayNotification
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4ba4c9d31d21e381bc006f9d6c5f0bb8e7d35f0b
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56527907"
---
# <a name="registering-for-device-interface-change-notification"></a>デバイス インターフェイスの変更通知を登録します。





ドライバーでは、呼び出すことによってデバイス インターフェイスの削除と到着のイベントの通知を登録します。 [ **IoRegisterPlugPlayNotification**](https://msdn.microsoft.com/library/windows/hardware/ff549526)します。

次の情報は、デバイス インターフェイスの変更通知のこのルーチンの呼び出しに適用されます。

-   指定、*によって*の**EventCategoryDeviceInterfaceChange**します。

-   *EventCategoryData*デバイス インターフェイスのクラスの GUID をポイントする必要があります。

    インターフェイス クラスの GUID は通常、インターフェイス構造体、定数、およびなどを含むヘッダー ファイルで定義されます。

-   指定、 *EventCategoryFlags* PNPNOTIFY の\_デバイス\_インターフェイス\_INCLUDE\_既存\_インターフェイス。

    このフラグを登録する PnP マネージャーに指示、 *CallbackRoutine*の将来のデバイスのインターフェイスの出会いと別れを呼び出すと、指定したクラスの*CallbackRoutine*いずれかが即座に既にアクティブにされている関連するデバイスのインターフェイス。

    ドライバーが呼び出せる[ **IoGetDeviceInterfaces** ](https://msdn.microsoft.com/library/windows/hardware/ff549186)ルーチンが、このフラグを設定、フラグを使用せず、特定のクラスの既存のインターフェイスの一覧を取得し、そのコールバックを登録する方が簡単で、回避できます、潜在的なタイミングの問題。

-   ドライバーの定義を指定*コンテキスト*、必要に応じて、PnP マネージャーは、コールバック ルーチンに渡されます。

デバイス インターフェイス着荷通知に対する応答でデバイスを識別するハンドルを開いたドライバーに登録する必要があります**EventCategoryTargetDeviceChange**デバイス上のイベント。 (を参照してください[PnP ターゲット デバイスの変更通知を使用して](using-pnp-target-device-change-notification.md))。

ドライバーは、呼び出すことによって通知登録をキャンセル[ **IoUnregisterPlugPlayNotification** ](https://msdn.microsoft.com/library/windows/hardware/ff550398)で、 *NotificationEntry*によって返される**IoRegisterPlugPlayNotification**します。

 

 





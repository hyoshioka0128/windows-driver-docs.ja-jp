---
title: ターゲット デバイス変更の通知登録
description: ターゲット デバイス変更の通知登録
ms.assetid: 5f7a9c44-c9a4-4ff8-a97d-ad2462b86af0
keywords:
- 通知 WDK PnP、ターゲット デバイスの変更
- ターゲット デバイスの変更通知 PnP WDK
- EventCategoryTargetDeviceChange 通知
- ターゲット デバイスの変更通知を登録します。
- IoRegisterPlugPlayNotification
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 96b478944afdeac60fe7c5d75bc9f7320ab9c6b0
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63338446"
---
# <a name="registering-for-target-device-change-notification"></a>ターゲット デバイス変更の通知登録

ドライバーを呼び出すことによって PnP ターゲット デバイスの変更イベントの通知の登録[ **IoRegisterPlugPlayNotification**](https://msdn.microsoft.com/library/windows/hardware/ff549526)します。

次の情報は、ターゲット デバイスの変更通知のこのルーチンの呼び出しに適用されます。

-   指定、*によって*の**EventCategoryTargetDeviceChange**します。

-   *EventCategoryData*通知を要求したデバイスのファイル オブジェクトをポイントする必要があります。

    ドライバーを呼び出す前に、ファイル オブジェクトの参照を取得する必要があります、ドライバーのコールバック ルーチンは、ファイル オブジェクトへのアクセスを必要とする場合**IoRegisterPlugPlayNotification**します。

    ドライバーのコールバック ルーチンに、ファイル オブジェクトへのアクセスが必要としない場合、ドライバーが、オブジェクトを参照する必要はありません。

    ファイル オブジェクトが閉じられた後、ドライバーは、その通知の登録を削除するまで、デバイスの通知を受信するドライバーが続行されます。 この設計により、GUID の通知を受け取るドライバー\_ターゲット\_デバイス\_削除\_など、イベントをキャンセルします。

-   ドライバーの定義を指定*コンテキスト*PnP マネージャーは、コールバック ルーチンに渡す。

    ドライバーを使用して、可能性があります、*コンテキスト*ファイル オブジェクトの現在の状態に関する情報を保持するパラメーター (たとえば、きました閉じた削除) します。

    また、ドライバーを使用して、*コンテキスト*当初デバイスを開くために使用するパスを格納します。 ドライバーは、このパスを使用して、操作の削除を取り消された後、デバイスを再度開きます。 (を参照してください[処理 GUID\_ターゲット\_デバイス\_削除\_キャンセル イベント](handling-a-guid-target-device-remove-cancelled-event.md)詳細についてはします)。

ドライバーを呼び出して通知登録を削除する[ **IoUnregisterPlugPlayNotification** ](https://msdn.microsoft.com/library/windows/hardware/ff550398)で、 *NotificationEntry*によって返される**IoRegisterPlugPlayNotification**します。 ドライバーは、通知に登録し、参照が未解決のまま、ファイル オブジェクトの参照が失われた、登録を削除して、ドライバーは、参照を解放する必要があります。

 

 





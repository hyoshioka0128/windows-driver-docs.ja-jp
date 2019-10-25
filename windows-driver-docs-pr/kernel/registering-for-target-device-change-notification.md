---
title: ターゲット デバイス変更の通知登録
description: ターゲット デバイス変更の通知登録
ms.assetid: 5f7a9c44-c9a4-4ff8-a97d-ad2462b86af0
keywords:
- 通知 WDK PnP、ターゲットデバイスの変更
- ターゲットデバイスの変更通知の WDK PnP
- Eventカテゴリ Targetdevicechange notification
- ターゲットデバイスの変更通知を登録しています
- IoRegisterPlugPlayNotification
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3c7490335a9b315ad9d3c28b286c7a1c0d2c1b73
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72827464"
---
# <a name="registering-for-target-device-change-notification"></a>ターゲット デバイス変更の通知登録

ドライバーは、 [**IoRegisterPlugPlayNotification**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioregisterplugplaynotification)を呼び出して、PnP ターゲットデバイス変更イベントの通知を登録します。

次の情報は、ターゲットデバイス変更通知に対してこのルーチンを呼び出す場合に適用されます。

-   Eventcategory **Targetdevicechange**の*eventcategory*を指定します。

-   *Eventカテゴリデータ*は、通知が要求されたデバイスのファイルオブジェクトを指している必要があります。

    ドライバーのコールバックルーチンがファイルオブジェクトへのアクセスを必要とする場合、ドライバーは**IoRegisterPlugPlayNotification**を呼び出す前に、ファイルオブジェクトの参照を取得する必要があります。

    ドライバーのコールバックルーチンがファイルオブジェクトへのアクセスを必要としない場合、ドライバーはオブジェクトを参照する必要はありません。

    ファイルオブジェクトが閉じられると、ドライバーはその通知登録を削除するまで、デバイスの通知を受信し続けます。 このように設計することで、ドライバーは、GUID\_ターゲット\_デバイスの通知を受信し\_\_取り消されたイベントを削除することができます。

-   PnP マネージャーがコールバックルーチンに渡すドライバー定義の*コンテキスト*を指定します。

    ドライバーは、 *Context*パラメーターを使用して、ファイルオブジェクトの現在の状態に関する情報を保持する場合があります (たとえば、閉じられたか、削除されています)。

    また、ドライバーは、最初にデバイスを開いたときに使用したパスを格納するために*コンテキスト*を使用する場合もあります。 ドライバーは、このパスを使用して、削除操作の取り消し後にデバイスを再度開くことができます。 (詳細については[、「\_デバイス\_\_ターゲット\_ターゲットを処理する](handling-a-guid-target-device-remove-cancelled-event.md)」を参照してください。

ドライバーは、 **IoRegisterPlugPlayNotification**によって返された*notificationentry*を使用して[**IoUnregisterPlugPlayNotification**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iounregisterplugplaynotification)を呼び出すことによって、通知登録を削除します。 ドライバーが通知用に登録されているときにファイルオブジェクトの参照を受け取り、その参照が未解決のままである場合、ドライバーは登録を削除した後に参照を解放する必要があります。

 

 





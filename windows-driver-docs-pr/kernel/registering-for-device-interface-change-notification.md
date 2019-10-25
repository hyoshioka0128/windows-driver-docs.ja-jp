---
title: デバイス インターフェイス変更の通知登録
description: デバイス インターフェイス変更の通知登録
ms.assetid: 680e4c5c-dac6-41b1-b754-aee782145ed0
keywords:
- 通知 WDK PnP、デバイスインターフェイスの変更
- EventCategoryDeviceInterfaceChange 通知
- デバイスインターフェイスの変更通知の WDK PnP
- デバイスインターフェイスの変更通知を登録しています
- IoRegisterPlugPlayNotification
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 75f29e2a2487baf7649e5bd381aa6fefae2919d4
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72827488"
---
# <a name="registering-for-device-interface-change-notification"></a>デバイス インターフェイス変更の通知登録





ドライバーは、 [**IoRegisterPlugPlayNotification**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioregisterplugplaynotification)を呼び出して、デバイスインターフェイスの到着イベントと削除イベントの通知を登録します。

次の情報は、デバイスインターフェイスの変更通知にこのルーチンを呼び出す場合に適用されます。

-   **EventCategoryDeviceInterfaceChange**の*eventcategory*を指定します。

-   *Eventカテゴリデータ*は、デバイスインターフェイスクラスの GUID を指している必要があります。

    インターフェイスクラスの GUID は、通常、インターフェイスの構造体、定数などのヘッダーファイルで定義されます。

-   PNPNOTIFY\_DEVICE\_INTERFACE の*Event フラグ*を指定して\_既存の\_インターフェイスを含め\_ます。

    このフラグは、PnP マネージャーに対して、将来のデバイスインターフェイスの到着と指定したクラスの出発に使用するためのコールアウト*ルーチン*を登録し、既に存在する関連デバイスインターフェイスに対して、すぐにシリアル*ルーチン*を呼び出すように指示します。能動的.

    ドライバーは[**Iogetdeviceinterfaces**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iogetdeviceinterfaces)を呼び出して、特定のクラスの既存のインターフェイスの一覧を取得し、このフラグを指定せずにコールバックルーチンを登録できます。ただし、フラグを使用する方が簡単で、タイミングの問題を回避できます。

-   PnP マネージャーがコールバックルーチンに渡すドライバー定義の*コンテキスト*を指定します (該当する場合)。

デバイスインターフェイスの到着通知に応答してデバイスへのハンドルを開くドライバーは、デバイス上の**Eventカテゴリ Targetdevicechange**イベントに登録する必要があります。 (「 [PnP ターゲットデバイスの変更通知の使用」を](using-pnp-target-device-change-notification.md)参照してください)。

ドライバーは、 **IoRegisterPlugPlayNotification**によって返された*notificationentry*を使用して[**IoUnregisterPlugPlayNotification**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iounregisterplugplaynotification)を呼び出すことによって、通知の登録をキャンセルします。

 

 





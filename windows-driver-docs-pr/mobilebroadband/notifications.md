---
title: 通知
description: 通知
ms.assetid: 55292cae-9255-4dae-9f60-93ce22253e60
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3812a8004840cf5a18ab9d017ae79a4dca91a8e7
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56536889"
---
# <a name="notifications"></a>通知


プランのアクティブ化の状態、データの上限に近づいている現在のローミングなどのサービス通知でユーザーを保持することができます。 Windows では、通知をトリガーする、SMS、USSD、および Windows Notification Service などの既存のチャネルをサポートします。

ユーザーが別のアプリであるかどうか、モバイル ブロード バンド アプリでトースト通知を通じてユーザーに時間が重要なイベントを伝える必要があります、**開始** 画面で、またはデスクトップ。

![トースト通知](images/mb-fig3-toast.png)

アプリには、SMS のプロセスにバック グラウンド イベントまたは USSD 通知を受信できます。 モバイル ブロード バンドのアプリに関連付けられているバック グラウンド通知の詳細については、これらの API ページを参照してください、 [Windows.ApplicationModel.Background](https://docs.microsoft.com/uwp/api/windows.applicationmodel.background)名前空間。

- [MobileBroadbandDeviceServiceNotificationTrigger](https://docs.microsoft.com/uwp/api/windows.applicationmodel.background.mobilebroadbanddeviceservicenotificationtrigger)
- [MobileBroadbandPcoDataChangeTrigger](https://docs.microsoft.com/uwp/api/windows.applicationmodel.background.mobilebroadbandpcodatachangetrigger)
- [NetworkOperatorNotificationTrigger](https://docs.microsoft.com/uwp/api/windows.applicationmodel.background.networkoperatornotificationtrigger)
- [SmsMessageReceivedTrigger](https://docs.microsoft.com/uwp/api/windows.applicationmodel.background.smsmessagereceivedtrigger)

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>関連トピック


[モバイル ブロード バンドのアプリのシナリオ](mobile-broadband-app-scenarios.md)

 

 







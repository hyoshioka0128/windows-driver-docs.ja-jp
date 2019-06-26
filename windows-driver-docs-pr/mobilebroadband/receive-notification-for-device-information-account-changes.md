---
title: 変更に関するデバイス情報アカウントの通知を受信する
description: 変更に関するデバイス情報アカウントの通知を受信する
ms.assetid: 67d96f61-57dc-4e4b-a6c1-5c3da28e8aaf
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 94def6e8a508d9801bb71febf9017e5718e10134
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67369206"
---
# <a name="receive-notification-for-device-information-account-changes"></a>変更に関するデバイス情報アカウントの通知を受信する


デバイス情報のアカウントの変更の通知を受信するには、使用、 [ **AccountUpdated** ](https://docs.microsoft.com/uwp/api/Windows.Networking.NetworkOperators.MobileBroadbandAccountWatcher#Windows_Networking_NetworkOperators_MobileBroadbandAccountWatcher_AccountUpdated)のイベント[ **MobileBroadbandAccountWatcher** ](https://docs.microsoft.com/uwp/api/Windows.Networking.NetworkOperators.MobileBroadbandAccountWatcher)ここで説明します。

1.  インスタンスを作成、 [ **MobileBroadbandAccountWatcher** ](https://docs.microsoft.com/uwp/api/Windows.Networking.NetworkOperators.MobileBroadbandAccountWatcher)オブジェクト。

2.  追加、 [ **AccountUpdated** ](https://docs.microsoft.com/uwp/api/Windows.Networking.NetworkOperators.MobileBroadbandAccountWatcher#Windows_Networking_NetworkOperators_MobileBroadbandAccountWatcher_AccountUpdated)イベント ハンドラー。

3.  呼び出す[**開始**](https://docs.microsoft.com/uwp/api/Windows.Networking.NetworkOperators.MobileBroadbandAccountWatcher#Windows_Networking_NetworkOperators_MobileBroadbandAccountWatcher_Start)ウォッチャーにします。

4.  クエリ、 [ **HasDeviceInformationChanged** ](https://docs.microsoft.com/uwp/api/Windows.Networking.NetworkOperators.MobileBroadbandAccountUpdatedEventArgs#Windows_Networking_NetworkOperators_MobileBroadbandAccountUpdatedEventArgs_HasDeviceInformationChanged)のプロパティ、 [ **MobileBroadbandAccountUpdatedEventArgs** ](https://docs.microsoft.com/uwp/api/Windows.Networking.NetworkOperators.MobileBroadbandAccountUpdatedEventArgs) 内のオブジェクト[**AccountUpdated** ](https://docs.microsoft.com/uwp/api/Windows.Networking.NetworkOperators.MobileBroadbandAccountWatcher#Windows_Networking_NetworkOperators_MobileBroadbandAccountWatcher_AccountUpdated)イベント ハンドラー。

5.  デバイスの情報が変更された場合は、アカウントを照会[ **CurrentDeviceInformation.TelephoneNumbers** ](https://docs.microsoft.com/uwp/api/Windows.Networking.NetworkOperators.MobileBroadbandDeviceInformation#Windows_Networking_NetworkOperators_MobileBroadbandDeviceInformation_TelephoneNumbers)電話番号のプロパティ。

    次に、例を示します。

    ``` syntax
    if (account.currentDeviceInformation.TelephoneNumbers.length > 0)
    {
      // there is now at least one telephone number
    }
    ```

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>関連トピック


[モバイル ブロード バンドの Windows ランタイム Api の一般的なタスク](common-tasks-for-mobile-broadband-windows-runtime-apis.md)

 

 







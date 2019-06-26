---
title: デバイスが PIN ロックされているかどうかを決定する
description: デバイスが PIN ロックされているかどうかを決定する
ms.assetid: 7889c049-e8a2-4d69-9e5b-4b4756dcf1b4
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f0d156ab5e78fddff13b61dfb0dbce8b5d7126e3
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67381514"
---
# <a name="determine-if-a-device-is-pin-locked"></a>デバイスが PIN ロックされているかどうかを決定する


ロックされたデバイス (たとえば、ICCID または IMEI) 上のサブスクリプション情報を利用できない可能性があります、ため、すべてのロックされたデバイスは、使用可能なネットワーク アカウントを列挙します。 アカウントがロックされているデバイスを表すかどうかを知るには、クエリ、 [ **NetworkDeviceStatus** ](https://docs.microsoft.com/uwp/api/Windows.Networking.NetworkOperators.MobileBroadbandDeviceInformation#Windows_Networking_NetworkOperators_MobileBroadbandDeviceInformation_NetworkDeviceStatus)のプロパティ、 [ **CurrentDeviceInformation** ](https://docs.microsoft.com/uwp/api/Windows.Networking.NetworkOperators.MobileBroadbandAccount#Windows_Networking_NetworkOperators_MobileBroadbandAccount_CurrentDeviceInformation)アカウントのプロパティ。 [**NetworkDeviceStatus**](https://docs.microsoft.com/uwp/api/Windows.Networking.NetworkOperators.NetworkDeviceStatus).**DeviceLocked** PIN ロックでは、一方をことを示します**NetworkDeviceStatus**.**DeviceBlocked** PUK ブロックを示します。

例:

``` syntax
var account = Windows.Networking.NetworkOperators.MobileBroadbandAccount.createFromNetworkAccountId(accountId);
if (account.currentDeviceInformation.networkDeviceStatus == Windows.Networking.NetworkOperators.NetworkDeviceStatus.DeviceLocked)
{
  // the pin is locked
}
```

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>関連トピック


[モバイル ブロード バンドの Windows ランタイム Api の一般的なタスク](common-tasks-for-mobile-broadband-windows-runtime-apis.md)

 

 







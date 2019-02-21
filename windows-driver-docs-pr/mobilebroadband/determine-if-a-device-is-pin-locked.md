---
title: デバイスが PIN ロックされているかを判断します。
description: デバイスが PIN ロックされているかを判断します。
ms.assetid: 7889c049-e8a2-4d69-9e5b-4b4756dcf1b4
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b758ae2f468fd1f4d1447627dfb21c9f24e0c551
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56550199"
---
# <a name="determine-if-a-device-is-pin-locked"></a>デバイスが PIN ロックされているかを判断します。


ロックされたデバイス (たとえば、ICCID または IMEI) 上のサブスクリプション情報を利用できない可能性があります、ため、すべてのロックされたデバイスは、使用可能なネットワーク アカウントを列挙します。 アカウントがロックされているデバイスを表すかどうかを知るには、クエリ、 [ **NetworkDeviceStatus** ](https://msdn.microsoft.com/library/windows/apps/br207369)のプロパティ、 [ **CurrentDeviceInformation** ](https://msdn.microsoft.com/library/windows/apps/hh770609)アカウントのプロパティ。 [**NetworkDeviceStatus**](https://msdn.microsoft.com/library/windows/apps/br207375).**DeviceLocked** PIN ロックでは、一方をことを示します**NetworkDeviceStatus**.**DeviceBlocked** PUK ブロックを示します。

次に、例を示します。

``` syntax
var account = Windows.Networking.NetworkOperators.MobileBroadbandAccount.createFromNetworkAccountId(accountId);
if (account.currentDeviceInformation.networkDeviceStatus == Windows.Networking.NetworkOperators.NetworkDeviceStatus.DeviceLocked)
{
  // the pin is locked
}
```

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>関連トピック


[モバイル ブロード バンドの Windows ランタイム Api の一般的なタスク](common-tasks-for-mobile-broadband-windows-runtime-apis.md)

 

 







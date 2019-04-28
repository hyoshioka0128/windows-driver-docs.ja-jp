---
title: デバイスが PIN ロックされているかどうかを決定する
description: デバイスが PIN ロックされているかどうかを決定する
ms.assetid: 7889c049-e8a2-4d69-9e5b-4b4756dcf1b4
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b758ae2f468fd1f4d1447627dfb21c9f24e0c551
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63378329"
---
# <a name="determine-if-a-device-is-pin-locked"></a>デバイスが PIN ロックされているかどうかを決定する


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

 

 







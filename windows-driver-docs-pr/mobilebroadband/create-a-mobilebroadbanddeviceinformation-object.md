---
title: MobileBroadbandDeviceInformation オブジェクトを作成する
description: MobileBroadbandDeviceInformation オブジェクトを作成する
ms.assetid: d7f89045-acb5-4b7c-9154-c05e4169490d
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b36664a086035e3532717e98696538b8df7a03c1
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67385533"
---
# <a name="create-a-mobilebroadbanddeviceinformation-object"></a>MobileBroadbandDeviceInformation オブジェクトを作成する


A [ **MobileBroadbandDeviceInformation** ](https://docs.microsoft.com/uwp/api/Windows.Networking.NetworkOperators.MobileBroadbandDeviceInformation)オブジェクトには、モバイル ブロード バンドに関連付けられているネットワーク デバイスのモバイル ブロード バンド固有のデータの取得に使用できるプロパティのセットが含まれます。アカウント (たとえば、ファームウェアのバージョン)。 これらのオブジェクトから取得できます、 [ **MobileBroadbandAccount** ](https://docs.microsoft.com/uwp/api/Windows.Networking.NetworkOperators.MobileBroadbandAccount)オブジェクトのみです。 なお、1 つ**MobileBroadbandAccount**オブジェクトに関連付けることができますを複数**MobileBroadbandDeviceInformation**オブジェクトではなく、一度に 1 つだけです。 (これは、MNO をユーザー アカウントを区別するために使用する情報を保持するには、1 つの SIM カードが 2 つの異なるモバイル ブロード バンド デバイスで使用する場合。)

取得する[ **MobileBroadbandDeviceInformation** ](https://docs.microsoft.com/uwp/api/Windows.Networking.NetworkOperators.MobileBroadbandDeviceInformation)オブジェクトを取得することによって、 [ **CurrentDeviceInformation** ](https://docs.microsoft.com/uwp/api/Windows.Networking.NetworkOperators.MobileBroadbandAccount#Windows_Networking_NetworkOperators_MobileBroadbandAccount_CurrentDeviceInformation)プロパティ、の[ **MobileBroadbandAccount** ](https://docs.microsoft.com/uwp/api/Windows.Networking.NetworkOperators.MobileBroadbandAccount)オブジェクト。 時に存在するネットワーク デバイスがないかどうかを**CurrentDeviceInformation**プロパティには、(たとえば、ため、電源が入っていないまたは無効にされた) が読み取られた、このプロパティの読み取りは NULL を返します。 これはいつでもでも変更できるため、(たとえば、ユーザーできるデバイスを取り外します)、プロパティのコピーを取得し、null の場合のテスト コピーを使用することをお勧めします。 次のコード例は、表示を示しています。 これを行う方法。

``` syntax
var myDeviceInfo = myNetworkAccountObject.currentDeviceInformation

if (myDeviceInfo == null)
{
  // no device present, inform user
}
else 
{
  // use myDeviceInfo to get the data you need
}
```

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>関連トピック


[モバイル ブロード バンドの Windows ランタイム Api の一般的なタスク](common-tasks-for-mobile-broadband-windows-runtime-apis.md)

 

 







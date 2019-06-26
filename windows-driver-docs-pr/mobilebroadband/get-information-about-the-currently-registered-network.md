---
title: 現在登録されているネットワークに関する情報を取得する
description: 現在登録されているネットワークに関する情報を取得する
ms.assetid: 94321933-fc93-4203-8de1-e715d66fd1e3
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 92b5c3ce071303c696e8c82705eb10efe7eea4ac
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67381472"
---
# <a name="get-information-about-the-currently-registered-network"></a>現在登録されているネットワークに関する情報を取得する


データ クラス、サービス プロバイダーの ID とネットワークにモバイル ブロード バンド デバイスが登録されている現在の名前を取得できます。 これを行うには、使用、 [ **RegisteredDataClass**](https://docs.microsoft.com/uwp/api/Windows.Networking.NetworkOperators.MobileBroadbandNetwork#Windows_Networking_NetworkOperators_MobileBroadbandNetwork_RegisteredDataClass)、 [ **RegisteredProviderId**](https://docs.microsoft.com/uwp/api/Windows.Networking.NetworkOperators.MobileBroadbandNetwork#Windows_Networking_NetworkOperators_MobileBroadbandNetwork_RegisteredProviderId)、および[ **RegisteredProviderName** ](https://docs.microsoft.com/uwp/api/Windows.Networking.NetworkOperators.MobileBroadbandNetwork#Windows_Networking_NetworkOperators_MobileBroadbandNetwork_RegisteredProviderName)アカウントの現在のネットワーク オブジェクトのプロパティ。

例:

``` syntax
var myNetwork = myNetworkAccountObject.currentNetwork
if (myNetwork != null && myNetwork.registeredDataClass == DataClasses.LteAdvanced)
{
  // user is connected to an LTE network
}
```

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>関連トピック


[モバイル ブロード バンドの Windows ランタイム Api の一般的なタスク](common-tasks-for-mobile-broadband-windows-runtime-apis.md)

 

 







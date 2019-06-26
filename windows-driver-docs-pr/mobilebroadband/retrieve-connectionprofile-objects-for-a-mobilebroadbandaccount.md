---
title: MobileBroadbandAccount の ConnectionProfile オブジェクトを取得する
description: MobileBroadbandAccount の ConnectionProfile オブジェクトを取得する
ms.assetid: 7e612aa5-1627-4ada-971a-a1d04eafeb81
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c6c193e7ac2ea08014da8cff6354a50546526e51
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67384733"
---
# <a name="retrieve-connectionprofile-objects-for-a-mobilebroadbandaccount"></a>MobileBroadbandAccount の ConnectionProfile オブジェクトを取得する


A [ **ConnectionProfile** ](https://docs.microsoft.com/uwp/api/Windows.Networking.Connectivity.ConnectionProfile)オブジェクトには一連のプロパティが含まれ、ネットワーク接続を確立するために、接続、使用状況、およびデータ プランの情報を取得するのに使用できるメソッド。 使用して、モバイル アカウントに関連付けられた接続プロファイルを取得できる、 [ **MobileBroadbandAccount** ](https://docs.microsoft.com/uwp/api/Windows.Networking.NetworkOperators.MobileBroadbandAccount)オブジェクト。 次のコード例は、表示を示しています。 これを行う方法。

**注**  すべての一覧[ **ConnectionProfile** ](https://docs.microsoft.com/uwp/api/Windows.Networking.Connectivity.ConnectionProfile)からオブジェクトを取得できる[ **Windows.Networking.Connectivity.NetworkInformation.GetConnectionProfiles**](https://docs.microsoft.com/uwp/api/Windows.Networking.Connectivity.NetworkInformation#Windows_Networking_Connectivity_NetworkInformation_GetConnectionProfiles)します。

 

``` syntax
var myConnectionProfileList = myNetworkAccountObject.getConnectionProfiles();

if (myConnectionProfileList.length !== 0)
{
  for (var i = 0; i < myConnectionProfileList.length; i++)
  {
    //Display connection profile properties
    var connectivityLevel = myConnectionProfileList[i].getNetworkConnectivityLevel();
    }
  }
else 
{
  // No connection profiles are associated with this mobile broadband account.
}
```

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>関連トピック


[モバイル ブロード バンドの Windows ランタイム Api の一般的なタスク](common-tasks-for-mobile-broadband-windows-runtime-apis.md)

 

 







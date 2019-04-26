---
title: MobileBroadbandAccount の ConnectionProfile オブジェクトを取得する
description: MobileBroadbandAccount の ConnectionProfile オブジェクトを取得する
ms.assetid: 7e612aa5-1627-4ada-971a-a1d04eafeb81
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5bac18b4eaba44e6b413c7882018d9c644ee20ab
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63345328"
---
# <a name="retrieve-connectionprofile-objects-for-a-mobilebroadbandaccount"></a>MobileBroadbandAccount の ConnectionProfile オブジェクトを取得する


A [ **ConnectionProfile** ](https://msdn.microsoft.com/library/windows/apps/br207249)オブジェクトには一連のプロパティが含まれ、ネットワーク接続を確立するために、接続、使用状況、およびデータ プランの情報を取得するのに使用できるメソッド。 使用して、モバイル アカウントに関連付けられた接続プロファイルを取得できる、 [ **MobileBroadbandAccount** ](https://msdn.microsoft.com/library/windows/apps/br207353)オブジェクト。 次のコード例は、表示を示しています。 これを行う方法。

**注**  すべての一覧[ **ConnectionProfile** ](https://msdn.microsoft.com/library/windows/apps/br207249)からオブジェクトを取得できる[ **Windows.Networking.Connectivity.NetworkInformation.GetConnectionProfiles**](https://msdn.microsoft.com/library/windows/apps/br207294)します。

 

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

 

 







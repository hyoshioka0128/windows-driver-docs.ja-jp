---
title: 現在登録されているネットワークに関する情報を取得する
description: 現在登録されているネットワークに関する情報を取得する
ms.assetid: 94321933-fc93-4203-8de1-e715d66fd1e3
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 936b189d5d82aab5dbfe2191cb11fc62bbedeccc
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63380169"
---
# <a name="get-information-about-the-currently-registered-network"></a>現在登録されているネットワークに関する情報を取得する


データ クラス、サービス プロバイダーの ID とネットワークにモバイル ブロード バンド デバイスが登録されている現在の名前を取得できます。 これを行うには、使用、 [ **RegisteredDataClass**](https://msdn.microsoft.com/library/windows/apps/hh967833)、 [ **RegisteredProviderId**](https://msdn.microsoft.com/library/windows/apps/hh967834)、および[ **RegisteredProviderName** ](https://msdn.microsoft.com/library/windows/apps/hh967835)アカウントの現在のネットワーク オブジェクトのプロパティ。

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

 

 







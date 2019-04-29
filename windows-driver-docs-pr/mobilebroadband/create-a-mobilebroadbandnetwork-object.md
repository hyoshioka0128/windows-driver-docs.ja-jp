---
title: MobileBroadbandNetwork オブジェクトを作成する
description: MobileBroadbandNetwork オブジェクトを作成する
ms.assetid: b69c72dc-56cd-4358-9eae-3859705488ea
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c7781b7f9693d7fd401202dcaf0467badddb7a40
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63383779"
---
# <a name="create-a-mobilebroadbandnetwork-object"></a>MobileBroadbandNetwork オブジェクトを作成する


[**MobileBroadbandNetwork** ](https://msdn.microsoft.com/library/windows/apps/hh770616)オブジェクトには、モバイル ブロード バンド アカウント (たとえば、ネットワークの登録状態または APN) に関連付けられているネットワークに関するライブ データの取得に使用できるプロパティのセットが含まれます。 これらのオブジェクトから取得できます、 [ **MobileBroadbandAccount** ](https://msdn.microsoft.com/library/windows/apps/br207353)オブジェクトのみです。 なお、1 つ**MobileBroadbandAccount**オブジェクトに関連付けることができますを複数**MobileBroadbandNetwork**オブジェクトではなく、一度に 1 つだけです。 (これは、MNO をユーザー アカウントを区別するために使用する情報を保持するには、1 つの SIM カードが 2 つの異なるモバイル ブロード バンド デバイスで使用する場合。)

取得する[ **MobileBroadbandAccount** ](https://msdn.microsoft.com/library/windows/apps/br207353)オブジェクトを取得することによって、 [ **CurrentNetwork** ](https://msdn.microsoft.com/library/windows/apps/hh770610)のプロパティを**MobileBroadbandAccount**オブジェクト。 時にアクティブなネットワークがない場合、 **CurrentNetwork**プロパティには、(たとえば、ため、ネットワーク デバイスが電源が入っていないか、無効になってまたは無線信号がなかった) が読み取られた、このプロパティの読み取りは NULL を返します。 これはいつでもでも変更できるため、(たとえば、ユーザーことができる方法について説明しますエレベーターで、コンピューターに接続がドロップ)、プロパティのコピーを取得し、null の場合のテスト コピーを使用することをお勧めします。 次のコード例を示します。

``` syntax
var myNetwork = myNetworkAccountObject.currentNetwork

if (myNetwork == null)
{
  // no network, inform user
}
else
{
  // use myNetwork to get the data you need
}
```

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>関連トピック


[モバイル ブロード バンドの Windows ランタイム Api の一般的なタスク](common-tasks-for-mobile-broadband-windows-runtime-apis.md)

 

 







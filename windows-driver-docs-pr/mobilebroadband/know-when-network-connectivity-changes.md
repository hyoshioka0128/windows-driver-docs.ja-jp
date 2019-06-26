---
title: ネットワーク接続が変更された場合に通知する
description: ネットワーク接続が変更された場合に通知する
ms.assetid: 2937ba62-16ad-4a81-92e8-62a8bb40d608
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 253560e37fcf6d47f4950ee83f7cb77096553155
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67364984"
---
# <a name="know-when-network-connectivity-changes"></a>ネットワーク接続が変更された場合に通知する


ネットワーク接続の変更、使用時に知って、 [ **AccountUpdated** ](https://docs.microsoft.com/uwp/api/Windows.Networking.NetworkOperators.MobileBroadbandAccountWatcher#Windows_Networking_NetworkOperators_MobileBroadbandAccountWatcher_AccountUpdated)のイベント[ **MobileBroadbandAccountWatcher**](https://docs.microsoft.com/uwp/api/Windows.Networking.NetworkOperators.MobileBroadbandAccountWatcher):

1.  インスタンスを作成、 [ **MobileBroadbandAccountWatcher** ](https://docs.microsoft.com/uwp/api/Windows.Networking.NetworkOperators.MobileBroadbandAccountWatcher)オブジェクト。

2.  追加、 [ **AccountUpdated** ](https://docs.microsoft.com/uwp/api/Windows.Networking.NetworkOperators.MobileBroadbandAccountWatcher#Windows_Networking_NetworkOperators_MobileBroadbandAccountWatcher_AccountUpdated)イベント ハンドラー。

3.  呼び出す[**開始**](https://docs.microsoft.com/uwp/api/Windows.Networking.NetworkOperators.MobileBroadbandAccountWatcher#Windows_Networking_NetworkOperators_MobileBroadbandAccountWatcher_Start)ウォッチャーにします。

4.  クエリ、 [ **HasNetworkChanged** ](https://docs.microsoft.com/uwp/api/Windows.Networking.NetworkOperators.MobileBroadbandAccountUpdatedEventArgs#Windows_Networking_NetworkOperators_MobileBroadbandAccountUpdatedEventArgs_HasNetworkChanged)のプロパティ、 [ **MobileBroadbandAccountUpdatedEventArgs** ](https://docs.microsoft.com/uwp/api/Windows.Networking.NetworkOperators.MobileBroadbandAccountUpdatedEventArgs)オブジェクト、 [**AccountUpdated** ](https://docs.microsoft.com/uwp/api/Windows.Networking.NetworkOperators.MobileBroadbandAccountWatcher#Windows_Networking_NetworkOperators_MobileBroadbandAccountWatcher_AccountUpdated)イベント ハンドラー。

5.  ネットワークが変更された場合は、クエリ、 [ **CurrentNetwork** ](https://docs.microsoft.com/uwp/api/Windows.Networking.NetworkOperators.MobileBroadbandAccount#Windows_Networking_NetworkOperators_MobileBroadbandAccount_CurrentNetwork)現在のネットワーク オブジェクトのプロパティ。

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>関連トピック


[モバイル ブロード バンドの Windows ランタイム Api の一般的なタスク](common-tasks-for-mobile-broadband-windows-runtime-apis.md)

 

 







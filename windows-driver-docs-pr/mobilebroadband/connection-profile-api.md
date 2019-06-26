---
title: 接続プロファイル API
description: 接続プロファイル API
ms.assetid: 671b0df6-4f4b-4867-86dd-5eb832d86b4b
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f1fbc87c916215f58860c323c74e1f3bf8a26287
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67360831"
---
# <a name="connection-profile-api"></a>接続プロファイル API


一部では、接続プロファイル API の[ **Windows.Networking.Connectivity.NetworkInformation**](https://docs.microsoft.com/uwp/api/Windows.Networking.Connectivity.NetworkInformation)、確立されたネットワーク接続の接続性、使用状況、およびデータのプラン情報を提供します. 特定のモバイル アカウントに関連付けられた接続プロファイルを使用して取得できる、 [ **MobileBroadbandAccount** ](https://docs.microsoft.com/uwp/api/Windows.Networking.NetworkOperators.MobileBroadbandAccount) API。 接続プロファイル API では、次のモバイル ブロード バンド インターフェイス上のネットワーク接続のいくつかのプロパティを照会する場合は、モバイル ブロード バンド アプリ。

-   [**GetNetworkConnectivityLevel** ](https://docs.microsoft.com/uwp/api/Windows.Networking.Connectivity.ConnectionProfile#Windows_Networking_Connectivity_ConnectionProfile_GetNetworkConnectivityLevel)ネットワークが接続されているかどうかと、ネットワークがインターネット接続を提供するかどうかを示します。

-   [**GetSignalBars** ](https://docs.microsoft.com/uwp/api/Windows.Networking.Connectivity.ConnectionProfile#Windows_Networking_Connectivity_ConnectionProfile_GetSignalBars)接続用の Windows UI によって表示される信号のバーの現在の数を示します。

-   [**GetNetworkUsageAsync** ](https://docs.microsoft.com/uwp/api/Windows.Networking.Connectivity.ConnectionProfile#Windows_Networking_Connectivity_ConnectionProfile_GetNetworkUsageAsync_Windows_Foundation_DateTime_Windows_Foundation_DateTime_Windows_Networking_Connectivity_DataUsageGranularity_Windows_Networking_Connectivity_NetworkUsageStates_)送信バイト数、バイトが受信されると、接続プロファイルの接続時間を提供します。

この API には、オペレーターのインターフェイスでの接続が変更されるたびに、アプリケーションに通知される状態変更イベントも含まれています。 詳細について、 [ **NetworkStatusChanged** ](https://docs.microsoft.com/uwp/api/Windows.Networking.Connectivity.NetworkInformation#Windows_Networking_Connectivity_NetworkInformation_NetworkStatusChanged)イベントを参照してください[ **NetworkStatusChangedEventHandler デリゲート**](https://docs.microsoft.com/uwp/api/windows.networking.connectivity.networkstatuschangedeventhandler)します。

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>関連トピック


[モバイル ブロード バンドの Windows ランタイム Api の一覧](list-of-mobile-broadband-windows-runtime-apis.md)

[ネットワーク情報のサンプル](https://go.microsoft.com/fwlink/p/?linkid=227013)

[**NetworkStatusChangedEventHandler delegate**](https://docs.microsoft.com/uwp/api/windows.networking.connectivity.networkstatuschangedeventhandler)

 

 







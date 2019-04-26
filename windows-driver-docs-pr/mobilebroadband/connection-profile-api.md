---
title: 接続プロファイル API
description: 接続プロファイル API
ms.assetid: 671b0df6-4f4b-4867-86dd-5eb832d86b4b
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 61df3cf586cab1f4968c508c8b51015a86647dd0
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63344284"
---
# <a name="connection-profile-api"></a>接続プロファイル API


一部では、接続プロファイル API の[ **Windows.Networking.Connectivity.NetworkInformation**](https://msdn.microsoft.com/library/windows/apps/br207293)、確立されたネットワーク接続の接続性、使用状況、およびデータのプラン情報を提供します. 特定のモバイル アカウントに関連付けられた接続プロファイルを使用して取得できる、 [ **MobileBroadbandAccount** ](https://msdn.microsoft.com/library/windows/apps/br207353) API。 接続プロファイル API では、次のモバイル ブロード バンド インターフェイス上のネットワーク接続のいくつかのプロパティを照会する場合は、モバイル ブロード バンド アプリ。

-   [**GetNetworkConnectivityLevel** ](https://msdn.microsoft.com/library/windows/apps/hh701021)ネットワークが接続されているかどうかと、ネットワークがインターネット接続を提供するかどうかを示します。

-   [**GetSignalBars** ](https://msdn.microsoft.com/library/windows/apps/dn266074)接続用の Windows UI によって表示される信号のバーの現在の数を示します。

-   [**GetNetworkUsageAsync** ](https://msdn.microsoft.com/library/windows/apps/dn266073)送信バイト数、バイトが受信されると、接続プロファイルの接続時間を提供します。

この API には、オペレーターのインターフェイスでの接続が変更されるたびに、アプリケーションに通知される状態変更イベントも含まれています。 詳細について、 [ **NetworkStatusChanged** ](https://msdn.microsoft.com/library/windows/apps/br207299)イベントを参照してください[ **NetworkStatusChangedEventHandler デリゲート**](https://msdn.microsoft.com/library/windows/apps/br207303)します。

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>関連トピック


[モバイル ブロード バンドの Windows ランタイム Api の一覧](list-of-mobile-broadband-windows-runtime-apis.md)

[ネットワーク情報のサンプル](https://go.microsoft.com/fwlink/p/?linkid=227013)

[**NetworkStatusChangedEventHandler delegate**](https://msdn.microsoft.com/library/windows/apps/br207303)

 

 







---
title: ネットワーク デバイスの無線がオンになっているかどうかを検出する
description: ネットワーク デバイスの無線がオンになっているかどうかを検出する
ms.assetid: deded77d-8810-498c-a5ae-44885189c061
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d09e6703e7002aa8cdd4e473f28c014e8458bf23
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67381479"
---
# <a name="discover-whether-the-network-device-radio-is-turned-on"></a>ネットワーク デバイスの無線がオンになっているかどうかを検出する


ユーザーは、そのタイルから直接モバイル ブロード バンドのアプリを起動する場合は、モバイル ブロード バンド デバイスをオフにすることがあります。 これにより、デバイスが省電力モードを入力したか、エンドユーザーが (ネットワーク デバイスを無効にします) を機内モードを有効になっては通常発生します。 大文字と小文字の場合は、取得、 [ **CurrentRadioState** ](https://docs.microsoft.com/uwp/api/Windows.Networking.NetworkOperators.MobileBroadbandDeviceInformation#Windows_Networking_NetworkOperators_MobileBroadbandDeviceInformation_CurrentRadioState)のプロパティ、 [ **MobileBroadbandDeviceInformation** ](https://docs.microsoft.com/uwp/api/Windows.Networking.NetworkOperators.MobileBroadbandDeviceInformation)オブジェクト、対象のネットワーク デバイスを返す[ **MobileBroadbandRadioState**](https://docs.microsoft.com/uwp/api/Windows.Networking.NetworkOperators.MobileBroadbandRadioState).**オフ**します。 (オプションがオンの場合 **に** も、 **CurrentRadioState**プロパティが返す**MobileBroadbandRadioState**)。

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>関連トピック


[モバイル ブロード バンドの Windows ランタイム Api の一般的なタスク](common-tasks-for-mobile-broadband-windows-runtime-apis.md)

 

 







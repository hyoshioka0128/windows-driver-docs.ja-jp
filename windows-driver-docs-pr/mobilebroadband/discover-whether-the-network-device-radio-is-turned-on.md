---
title: ネットワーク デバイスの無線がオンになっているかどうかを検出する
description: ネットワーク デバイスの無線がオンになっているかどうかを検出する
ms.assetid: deded77d-8810-498c-a5ae-44885189c061
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 629538fce62acd6f785fb722104458c2a8f00a02
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63380260"
---
# <a name="discover-whether-the-network-device-radio-is-turned-on"></a>ネットワーク デバイスの無線がオンになっているかどうかを検出する


ユーザーは、そのタイルから直接モバイル ブロード バンドのアプリを起動する場合は、モバイル ブロード バンド デバイスをオフにすることがあります。 これにより、デバイスが省電力モードを入力したか、エンドユーザーが (ネットワーク デバイスを無効にします) を機内モードを有効になっては通常発生します。 大文字と小文字の場合は、取得、 [ **CurrentRadioState** ](https://msdn.microsoft.com/library/windows/apps/hh770613)のプロパティ、 [ **MobileBroadbandDeviceInformation** ](https://msdn.microsoft.com/library/windows/apps/br207361)オブジェクト、対象のネットワーク デバイスを返す[ **MobileBroadbandRadioState**](https://msdn.microsoft.com/library/windows/apps/hh758385).**オフ**します。 (オプションがオンの場合にも、 **CurrentRadioState**プロパティが返す**MobileBroadbandRadioState**)。****

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>関連トピック


[モバイル ブロード バンドの Windows ランタイム Api の一般的なタスク](common-tasks-for-mobile-broadband-windows-runtime-apis.md)

 

 







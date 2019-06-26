---
title: デバイスがネットワークに接続する Windows を決定します。
description: ネットワークへの接続に使用されている Windows デバイスを決定する
ms.assetid: ea9a07cd-ad6e-4c49-aae0-fc9eee9b17c8
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 64c1b895dee464d91c226a7aa243452a4efc2cb5
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67381532"
---
# <a name="determine-which-windows-device-is-being-used-to-connect-to-the-network"></a>ネットワークへの接続に使用されている Windows デバイスを決定する

Windows デバイスは、ネットワークへの接続に使用されているを判断するには、によって公開されるネットワーク アダプターの Windows デバイスの ID を確認、 [ **DeviceId** ](https://docs.microsoft.com/uwp/api/Windows.Networking.NetworkOperators.MobileBroadbandDeviceInformation#Windows_Networking_NetworkOperators_MobileBroadbandDeviceInformation_DeviceId)現在のネットワーク デバイスのプロパティアカウントのオブジェクト。

例:

``` syntax
account.currentDeviceInformation.deviceId
```

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>関連トピック


[モバイル ブロード バンドの Windows ランタイム Api の一般的なタスク](common-tasks-for-mobile-broadband-windows-runtime-apis.md)

 

 







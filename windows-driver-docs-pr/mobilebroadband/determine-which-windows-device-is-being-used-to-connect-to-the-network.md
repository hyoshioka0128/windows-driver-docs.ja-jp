---
title: デバイスがネットワークに接続する Windows を決定します。
description: ネットワークへの接続に使用されている Windows デバイスを決定する
ms.assetid: ea9a07cd-ad6e-4c49-aae0-fc9eee9b17c8
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6973e43207f189d87be8d71a3a6917da268c73eb
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63378320"
---
# <a name="determine-which-windows-device-is-being-used-to-connect-to-the-network"></a>ネットワークへの接続に使用されている Windows デバイスを決定する

Windows デバイスは、ネットワークへの接続に使用されているを判断するには、によって公開されるネットワーク アダプターの Windows デバイスの ID を確認、 [ **DeviceId** ](https://msdn.microsoft.com/library/windows/apps/br207365)現在のネットワーク デバイスのプロパティアカウントのオブジェクト。

次に、例を示します。

``` syntax
account.currentDeviceInformation.deviceId
```

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>関連トピック


[モバイル ブロード バンドの Windows ランタイム Api の一般的なタスク](common-tasks-for-mobile-broadband-windows-runtime-apis.md)

 

 







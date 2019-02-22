---
title: デバイスがネットワークに接続する Windows を決定します。
description: Windows デバイスは、ネットワークへの接続に使用されているかを決定します。
ms.assetid: ea9a07cd-ad6e-4c49-aae0-fc9eee9b17c8
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6973e43207f189d87be8d71a3a6917da268c73eb
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56553882"
---
# <a name="determine-which-windows-device-is-being-used-to-connect-to-the-network"></a>Windows デバイスは、ネットワークへの接続に使用されているかを決定します。

Windows デバイスは、ネットワークへの接続に使用されているを判断するには、によって公開されるネットワーク アダプターの Windows デバイスの ID を確認、 [ **DeviceId** ](https://msdn.microsoft.com/library/windows/apps/br207365)現在のネットワーク デバイスのプロパティアカウントのオブジェクト。

次に、例を示します。

``` syntax
account.currentDeviceInformation.deviceId
```

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>関連トピック


[モバイル ブロード バンドの Windows ランタイム Api の一般的なタスク](common-tasks-for-mobile-broadband-windows-runtime-apis.md)

 

 







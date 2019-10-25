---
title: メッセージのサブスクライブ
description: メッセージのサブスクライブ
ms.assetid: CF0D5CE0-A0E0-47D4-88E6-FBE186F78626
keywords:
- NFC
- 近距離無線通信
- proximity
- 近距離近接通信
- NFP
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 17ee88d22eda73fab0228dabe904428726714edc
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72827354"
---
# <a name="subscribing-for-messages"></a>メッセージのサブスクライブ


クライアントは、種類によってメッセージをサブスクライブできます。 メッセージが受信されると、NFP プロバイダーは、その正確な種類のサブスクリプションを持つクライアントにのみメッセージを発行します。 受信側のクライアントは、その情報がパブリッシャーによってメッセージ内に配置されていない限り、メッセージが公開された場所やタイミングについての情報を持ちません。 モデル内には、他のクライアントがメッセージを受信したかどうかを判断する手段はありません。

サブスクリプションには、公開メッセージと同じ有効期間モデルがあります。

クライアントがメッセージをアンサブスクライブするときは、サブスクライブされていないサブスクリプションの種類と一致するメッセージが発行されなくなります。

## <a name="subscribed-message-arrival"></a>サブスクライブ済みメッセージの到着


NFP プロバイダーは、メッセージを受信すると、サブスクライブしているすべてのクライアントにメッセージを配信します。 メッセージは、サブスクリプションの種類が公開されたメッセージと一致する場合にのみ、クライアントに配信されます。

モデルでは、順序付けや優先順位は定義されていません。 プロバイダーは、サブスクライブされたメッセージを並列に発行することができますが、これは必須ではありません。

 

 
## <a name="related-topics"></a>関連トピック
[NFC デバイスドライバーインターフェイス (DDI) の概要](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)  
[近距離無線近接 DDI リファレンス](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)  


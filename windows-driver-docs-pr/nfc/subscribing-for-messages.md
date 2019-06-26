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
ms.openlocfilehash: e3bfd0226ca87a2b36620193bcec8cbe671bf29b
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67379381"
---
# <a name="subscribing-for-messages"></a>メッセージのサブスクライブ


クライアントは、種類別にメッセージをサブスクライブできます。 メッセージを受信すると、NFP プロバイダーはその正確な種類のサブスクリプションを所有するクライアントにメッセージをのみ発行します。 受信側のクライアントには、パブリッシャーがこのような情報が、メッセージ内に配置しない限り、メッセージが発行されたときまたは位置の知識はありません。 モデル内でどのような他のクライアントも判断することを意味のメッセージ受信されません。

サブスクリプションでは、公開されたメッセージと同じ有効期間モデルがあります。

クライアントがメッセージの登録解除時に、不要になったを発行するかサブスクライブされていないサブスクリプションの種類に一致するメッセージ。

## <a name="subscribed-message-arrival"></a>サブスクライブされたメッセージの到着


NFP プロバイダーは、メッセージを受信したときに、購読しているクライアントに送信します。 サブスクリプションの種類が、パブリッシュされたメッセージと一致する場合にのみ、メッセージがクライアントに配信されます。

順序付けや、モデルで定義されている優先順位はありません。 並列でサブスクライブされたメッセージを発行するプロバイダーもかまいませんが、これは必要ありません。

 

 
## <a name="related-topics"></a>関連トピック
[NFC のデバイス ドライバー インターフェイス (DDI) の概要](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/index)  
[フィールドの近接 DDI 参照の近く](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/index)  


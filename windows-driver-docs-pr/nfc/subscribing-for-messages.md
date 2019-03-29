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
ms.openlocfilehash: 7239c3b146ca73512645473b2dc807552410725b
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56571061"
---
# <a name="subscribing-for-messages"></a>メッセージのサブスクライブ


クライアントは、種類別にメッセージをサブスクライブできます。 メッセージを受信すると、NFP プロバイダーはその正確な種類のサブスクリプションを所有するクライアントにメッセージをのみ発行します。 受信側のクライアントには、パブリッシャーがこのような情報が、メッセージ内に配置しない限り、メッセージが発行されたときまたは位置の知識はありません。 モデル内でどのような他のクライアントも判断することを意味のメッセージ受信されません。

サブスクリプションでは、公開されたメッセージと同じ有効期間モデルがあります。

クライアントがメッセージの登録解除時に、不要になったを発行するかサブスクライブされていないサブスクリプションの種類に一致するメッセージ。

## <a name="subscribed-message-arrival"></a>サブスクライブされたメッセージの到着


NFP プロバイダーは、メッセージを受信したときに、購読しているクライアントに送信します。 サブスクリプションの種類が、パブリッシュされたメッセージと一致する場合にのみ、メッセージがクライアントに配信されます。

順序付けや、モデルで定義されている優先順位はありません。 並列でサブスクライブされたメッセージを発行するプロバイダーもかまいませんが、これは必要ありません。

 

 
## <a name="related-topics"></a>関連トピック
[NFC のデバイス ドライバー インターフェイス (DDI) の概要](https://msdn.microsoft.com/library/windows/hardware/mt715815)  
[フィールドの近接 DDI 参照の近く](https://msdn.microsoft.com/library/windows/hardware/jj866056)  


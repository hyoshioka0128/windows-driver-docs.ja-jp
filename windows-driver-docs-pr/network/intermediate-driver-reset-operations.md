---
title: 中間ドライバー リセット操作
description: 中間ドライバー リセット操作
ms.assetid: 473dce77-4636-40da-ac38-cda1676eba3f
keywords:
- 中間ドライバー WDK ネットワー キング、リセットの操作
- NDIS は、ドライバー WDK を中間、リセット操作
- 中間ドライバーをリセットします。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5a89ee57187b31dc742597e74ede4f6218465e70
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67371825"
---
# <a name="intermediate-driver-reset-operations"></a>中間ドライバー リセット操作





中間のドライバーは、基になる NIC をリセットするための基になるドライバーへのバインドで未処理の送信のドロップされる状況を処理するために準備する必要があります。

基になるドライバーは、NDIS ミニポート ドライバーを呼び出すため、通常、NIC をリセット[ *MiniportResetEx* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_reset) NDIS がキューに置かれた送信タイムアウトまたは要求の NIC にバインドするときに関数 NDIS を呼び出す、基になる NIC をリセットする場合、 [ **ProtocolStatusEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-protocol_status_ex)(または[ **ProtocolCoStatusEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-protocol_co_status_ex)) の各関数には、プロトコルがバインドされています。ドライバーおよび NDIS の状態で中間ドライバー\_状態\_リセット\_を開始します。 NDIS ミニポート ドライバーには、リセットが完了すると、呼び出すもう一度*ProtocolStatusEx*(または*ProtocolCoStatusEx*) 状態の NDIS\_状態\_リセット\_終わり。

NIC をいつリセット、バインドされた中間ドライバーには、保留中である送信ネットワークのデータが含まれている場合、その NIC に NDIS 中間ドライバーを適切な状態に戻す、ネットワーク データが完了するとします。 中間ドライバーは、リセットが完了したときに、これらネットワーク データをもう一度再発行する必要があります。

中間のドライバーが NDIS の状態を受信すると\_状態\_リセット\_必要があります、開始。

-   まで送信可能、ネットワーク データを保持*ProtocolStatusEx*または*ProtocolCoStatusEx*受信、NDIS\_状態\_リセット\_終了の通知。

-   最大まで [次へ] 以上のドライバーを指定することができる、受信したネットワーク データを保持*ProtocolStatusEx*(または*ProtocolCoStatusEx*)、NDIS を受け取る\_状態\_リセット\_終了を通知します。

-   進行中の操作と NIC の状態について管理、内部状態をクリーンアップします。

後*ProtocolStatusEx*(または*ProtocolCoStatusEx*) 受信 NDIS\_状態\_リセット\_最後に、中間のドライバーを再開できますネットワークのデータを送信します。要求を行うと、問題により高度なドライバーを作成します。

中間のドライバーが提供されない、 [ *MiniportResetEx* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_reset)関数。

 

 






---
title: プロトコル ドライバーのバインディングの状態
description: プロトコル ドライバーのバインディングの状態
ms.assetid: 15bc6217-e258-4e07-abc8-6c46fd01d85b
keywords:
- プロトコル ドライバー WDK ネットワークは、バインドの状態
- NDIS プロトコル ドライバー WDK には、バインドを状態します。
- バインドは、WDK ネットワークを状態します。
- プロトコル バインド WDK ネットワーク
- プロトコル ドライバー WDK ネットワー キング、プロトコル バインド
- NDIS プロトコル ドライバー WDK、プロトコル
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a0b91088e7214ad7cbd7303abea035c95302fcad
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67354643"
---
# <a name="binding-states-of-a-protocol-driver"></a>プロトコル ドライバーのバインディングの状態





[NDIS プロトコル ドライバー](ndis-protocol-drivers2.md)ドライバーを管理する各バインドに次の操作の状態をサポートする必要があります。

-   バインドされていません。

-   開始

-   実行中

-   閉じる

-   一時停止

-   一時停止

-   再起動します。

次の図は、これらの状態間の関係を示します。

![バインドの状態を示す図](images/protocolstate.png)

次に、プロトコル ドライバーにバインドの状態を定義します。

<a href="" id="unbound"></a>バインドされていません。  
*未バインド*状態は、バインディングの初期状態です。 この状態は、NDIS を呼び出すが待機プロトコル ドライバー、 [ *ProtocolBindAdapterEx* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-protocol_bind_adapter_ex)関数。 NDIS 後*ProtocolBindAdapterEx*バインディングが Opening 状態に遷移します。 バインドの解除後に操作が完了すると、バインド状態に戻ります、非連結 Closing 状態から。

<a href="" id="opening"></a>開始  
*開く*状態では、プロトコル ドライバーを選択して、バインド用リソースを割り当てますミニポート アダプターを開こうとするとします。 NDIS ドライバーを呼び出してから*ProtocolBindAdapterEx*関数の場合、バインディングが Opening 状態に遷移します。 プロトコル ドライバーには、ミニポート アダプターにバインドできない場合、非連結の状態にバインディングを返します。 ドライバーは正常にミニポート アダプターにバインドした場合、バインドは一時停止状態になります。

<a href="" id="running"></a>実行しています。  
*を実行している*状態では、通常の送信を実行するプロトコル ドライバーとバインドの処理を受信します。 バインディングを再開中状態にして、ドライバーが送信を実行し、受信操作に準備ができたら、ときに、バインドが実行状態になります。

<a href="" id="closing"></a>閉じる  
*閉じる*状態では、プロトコル ドライバーがミニポート アダプターへのバインドを終了し、バインド用のリソースを解放します。 NDIS 呼び出しプロトコル ドライバーの後に[ *ProtocolUnbindAdapterEx* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-protocol_unbind_adapter_ex)関数の場合、バインディングが Closing 状態に遷移します。 プロトコル ドライバーには、バインドの解除操作が完了すると、バインディングは連結なし状態になります。

<a href="" id="pausing"></a>一時停止  
*一時停止中*状態では、プロトコル ドライバーに送信を停止し、受信バインドの操作に必要なすべての操作が完了するとします。 バインドが実行中の状態では、NDIS はプロトコル ドライバーの PnP の一時停止の通知を送信します、バインドは一時停止状態になります。 プロトコル ドライバーには、そのすべての未処理の送信要求が完了するを待つ必要があります。 プロトコル ドライバーには、一時停止操作が失敗することはできません。 一時停止操作が完了した後、バインドは一時停止状態になります。

<a href="" id="paused"></a>一時停止  
*Paused*状態では、プロトコルのドライバーが送信を実行またはバインディングの操作を受信していません。 バインディングが一時停止状態と、一時停止操作が完了すると、バインドは一時停止状態になります。 バインディングが Opening 状態と開く操作が正常に完了すると、バインドは一時停止状態になります。 NDIS は、プロトコル ドライバーにバインディングの PnP 再起動通知を送信する場合、バインドは再開中状態になります。 NDIS ドライバーの場合[ *ProtocolUnbindAdapterEx* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-protocol_unbind_adapter_ex)関数の場合、バインディングが Closing 状態に遷移します。

<a href="" id="restarting"></a>再起動します。  
*再起動*状態では、プロトコル ドライバーに送信を再起動し、受信バインドの操作に必要なすべての操作が完了するとします。 バインドは一時停止状態であり、NDIS プロトコル ドライバーに送信、PnP 再起動の通知、バインディングは、再開中状態になります。 再起動が失敗した場合、バインディングが一時停止状態に戻ります。 再起動が成功した場合、バインドが実行状態になります。

## <a name="related-topics"></a>関連トピック


[ドライバー スタックの管理](driver-stack-management.md)

[NDIS プロトコル ドライバー](ndis-protocol-drivers2.md)

 

 







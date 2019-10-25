---
title: プロトコル ドライバーのバインディングの状態
description: プロトコル ドライバーのバインディングの状態
ms.assetid: 15bc6217-e258-4e07-abc8-6c46fd01d85b
keywords:
- プロトコルドライバー WDK ネットワーク、バインドの状態
- NDIS プロトコルドライバー WDK、バインドの状態
- バインドの状態 WDK ネットワーク
- プロトコルバインドの WDK ネットワーク
- プロトコルドライバー WDK ネットワーク, プロトコルバインド
- NDIS プロトコルドライバー WDK、プロトコル
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b8e47cfc9c543c58d7049c191918d44dd1c3f829
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838219"
---
# <a name="binding-states-of-a-protocol-driver"></a>プロトコル ドライバーのバインディングの状態





[NDIS プロトコルドライバー](ndis-protocol-drivers2.md)では、ドライバーが管理する各バインドについて、次の動作状態がサポートされている必要があります。

-   非バインド

-   左中

-   Running

-   右山

-   一時停止

-   一時停止

-   再起動

次の図は、これらの状態の関係を示しています。

![バインド状態ダイアグラムを示す図](images/protocolstate.png)

プロトコルドライバーのバインドの状態は、次のように定義されています。

<a href="" id="unbound"></a>非バインド  
バインド解除され*た状態は、バインディング*の初期状態です。 この状態では、プロトコルドライバーは NDIS が[*Protocolbindadapterex*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-protocol_bind_adapter_ex)関数を呼び出すまで待機します。 NDIS が*Protocolbindadapterex*を呼び出した後、バインドは開始状態になります。 バインド解除操作が完了すると、バインドは終了状態から非バインド状態に戻ります。

<a href="" id="opening"></a>左中  
*オープン*状態では、プロトコルドライバーによってバインディングのリソースが割り当てられ、ミニポートアダプターを開こうとします。 NDIS がドライバーの*Protocolbindadapterex*関数を呼び出した後、バインディングは開始状態になります。 プロトコルドライバーがミニポートアダプターへのバインドに失敗した場合、バインドはバインドされていない状態に戻ります。 ドライバーがミニポートアダプターに正常にバインドされている場合、バインドは一時停止状態になります。

<a href="" id="running"></a>起動  
*実行*状態では、プロトコルドライバーはバインドに対して通常の送受信処理を実行します。 バインドが再開中の状態で、ドライバーが送信および受信操作を実行する準備ができたら、バインドは実行中の状態になります。

<a href="" id="closing"></a>右山  
*終了*状態では、プロトコルドライバーはミニポートアダプターへのバインディングを閉じ、バインディングのリソースを解放します。 NDIS がプロトコルドライバーの[*Protocolunbindadapterex*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-protocol_unbind_adapter_ex)関数を呼び出した後、バインディングは終了状態になります。 プロトコルドライバーがバインド解除操作を完了すると、バインドはバインドされていない状態になります。

<a href="" id="pausing"></a>一時停止  
*一時停止*中の状態では、バインドの送信および受信操作を停止するために必要なすべての操作が、プロトコルドライバーによって完了されます。 バインドが Running 状態で、NDIS がプロトコルドライバーを PnP 一時停止通知に送信すると、バインドは一時停止中の状態になります。 プロトコルドライバーは、すべての未処理の送信要求が完了するまで待機する必要があります。 プロトコルドライバーは、一時停止操作を失敗することはできません。 一時停止操作が完了すると、バインドは一時停止状態になります。

<a href="" id="paused"></a>中  
*一時停止*状態では、プロトコルドライバーはバインドに対して送信操作または受信操作を実行しません。 バインディングが一時停止中の状態で、一時停止操作が完了すると、バインディングは一時停止状態になります。 バインディングが開始状態で、開いている操作が正常に完了すると、バインディングは一時停止状態になります。 NDIS がプロトコルドライバーにバインドの PnP 再起動通知を送信すると、バインドは再起動状態になります。 NDIS がドライバーの[*Protocolunbindadapterex*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-protocol_unbind_adapter_ex)関数を呼び出すと、バインディングは終了状態になります。

<a href="" id="restarting"></a>再起動  
*再起動*状態では、プロトコルドライバーは、バインディングの送信および受信操作を再開するために必要なすべての操作を完了します。 バインドが一時停止状態であり、NDIS がプロトコルドライバーを PnP 再起動通知に送信すると、バインドは再起動状態になります。 再起動が失敗した場合、バインディングは一時停止状態に戻ります。 再起動が成功した場合、バインディングは実行中の状態になります。

## <a name="related-topics"></a>関連トピック


[ドライバースタックの管理](driver-stack-management.md)

[NDIS プロトコルドライバー](ndis-protocol-drivers2.md)

 

 







---
title: ミニポート ドライバーのアダプターの状態
description: ミニポート ドライバーのアダプターの状態
ms.assetid: 3ca03511-a912-4ee3-bd9f-1bd8e6996c48
keywords:
- NDIS ミニポートドライバー WDK、アダプターの状態
- 'アダプターの状態: WDK ネットワーク'
- ミニポートアダプター WDK ネットワーク、状態
- ミニポートドライバー WDK ネットワーク、ミニポートアダプター
- NDIS ミニポートドライバー WDK、ミニポートアダプター
- 状態 WDK ネットワークを停止しました
- S
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6fc48280293f66f459fc674b06131f15f942b703
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838248"
---
# <a name="adapter-states-of-a-miniport-driver"></a>ミニポート ドライバーのアダプターの状態





[NDIS ミニポートドライバー](ndis-miniport-drivers2.md)は、管理する各ミニポートアダプターに対して、次の一連の動作状態をサポートする必要があります。

-   停止

-   シャットダウン

-   初期化

-   一時停止

-   再起動

-   実行中

-   一時停止

次の図は、これらの状態間の相互関係を示しています。

![ミニポートアダプターの状態ダイアグラムを示す図](images/miniportstate.png)

**注**  リセット操作は、ミニポートアダプターの操作状態に影響しません。 また、リセット操作の実行中にアダプターの状態が変わる可能性があります。 たとえば、NDIS は、実行中のリセット操作があるときにドライバーの pause ハンドラーを呼び出す場合があります。 この場合、ドライバーは、各操作の通常の要件に従って、任意の順序でリセット操作または一時停止操作を完了できます。 リセット操作の場合、ドライバーは要求パケットの送信に失敗することがあります。または、キューをキューに入れて後で完了させることができます。 ただし、送信パケットが保留されている間は、後続のドライバーが一時停止操作を完了できないことに注意してください。

 

アダプターの状態は次のように定義されています。

<a href="" id="halted"></a>停止  
*停止*は、すべてのミニポートアダプターの初期状態です。 ミニポートアダプターが停止状態になり、NDIS がドライバーの[*MiniportInitializeEx*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_initialize)関数を呼び出してミニポートアダプターを初期化すると、ミニポートアダプターは初期化中の状態になります。 *MiniportInitializeEx*が失敗した場合、ミニポートアダプターは停止状態に戻ります。 ミニポートアダプターが一時停止状態で、NDIS が[*Miniporthaltex*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_halt)関数を呼び出すと、ミニポートアダプターは停止状態に戻ります。

<a href="" id="shutdown"></a>シャットダウン  
*シャットダウン*状態のミニポートアダプターは、システムがシャットダウンされて再起動されるまで使用できません。 ミニポートアダプターが一時停止、再起動、実行中、または一時停止中の状態で、NDIS がミニポートドライバーの[*Miniportshutdownex*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_shutdown)関数を呼び出すと、ミニポートアダプターがシャットダウン状態になります。

<a href="" id="initializing"></a>初期化  
*初期*状態では、ミニポートドライバーは、ミニポートアダプターの初期化に必要なすべての操作を完了します。 ミニポートアダプターが停止状態になり、NDIS がミニポートドライバーの*MiniportInitializeEx*関数を呼び出すと、ミニポートアダプターは初期化中の状態になります。 *MiniportInitializeEx*が成功すると、ミニポートアダプターは一時停止状態になります。 *MiniportInitializeEx*が失敗した場合、ミニポートアダプターは停止状態に戻ります。

<a href="" id="paused"></a>中  
ミニポートアダプターが*一時停止*状態の場合、ミニポートドライバーは、受信したネットワークデータを示したり、送信要求を受け入れたりしません。 ミニポートアダプターが一時停止中の状態で、一時停止操作が完了すると、ミニポートアダプターは一時停止状態になります。 ミニポートアダプターが初期化状態で、 *MiniportInitializeEx*が成功すると、ミニポートアダプターは一時停止状態になります。 NDIS がミニポートドライバーの[**Miniportrestart**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_restart)関数を呼び出すと、ミニポートアダプターは一時停止状態から再起動状態に遷移します。 NDIS がミニポートドライバーの[*Miniporthaltex*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_halt)関数を呼び出すと、ミニポートアダプターは、一時停止状態から停止状態に遷移します。

<a href="" id="restarting"></a>再起動  
*再起動*状態の場合、ミニポートドライバーは、ミニポートアダプターの送信および受信操作を再開するために必要なすべての操作を完了します。 ミニポートアダプターが一時停止状態にあり、NDIS がドライバーの*Miniportrestart*関数を呼び出すと、ミニポートアダプターは再起動状態になります。 再起動に失敗すると、ミニポートアダプターは一時停止状態に戻ります。 再起動が成功すると、ミニポートアダプタは実行状態になります。

<a href="" id="running"></a>起動  
*実行*状態では、ミニポートドライバーはミニポートアダプターに対して通常の送受信処理を実行します。 ミニポートアダプターが再起動中の状態で、ドライバーが送信および受信操作を実行する準備ができたら、ミニポートアダプターは実行中の状態になります。

<a href="" id="pausing"></a>一時停止  
*一時停止*中の状態では、ミニポートドライバーは、ミニポートアダプターの送信および受信操作を停止するために必要なすべての操作を完了します。 ドライバーは、NDIS が未処理の受信通知をすべて返すまで待機する必要があります。 ミニポートアダプターが Running 状態で、NDIS がドライバーの[*Miniportpause*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_pause)関数を呼び出すと、ミニポートアダプターが一時停止中の状態になります。 ミニポートドライバーは、一時停止操作を失敗することはできません。 一時停止操作が完了すると、ミニポートアダプターが一時停止状態になります。

## <a name="related-topics"></a>関連トピック


[ドライバースタックの管理](driver-stack-management.md)

[NDIS ミニポートドライバー](ndis-miniport-drivers2.md)

 

 







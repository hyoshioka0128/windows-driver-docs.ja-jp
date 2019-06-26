---
title: ミニポート ドライバーのアダプターの状態
description: ミニポート ドライバーのアダプターの状態
ms.assetid: 3ca03511-a912-4ee3-bd9f-1bd8e6996c48
keywords:
- NDIS ミニポート ドライバー WDK には、アダプターを状態します。
- アダプターは、WDK ネットワークを状態します。
- ミニポート アダプタの WDK ネットワー キング、状態
- ミニポート ドライバー WDK ネットワー キング、ミニポート アダプター
- NDIS ミニポート ドライバー WDK、ミニポート アダプター
- 停止状態の WDK ネットワーク
- S
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 55891e1d0a29853e528920f4d3583460e7897a74
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67379307"
---
# <a name="adapter-states-of-a-miniport-driver"></a>ミニポート ドライバーのアダプターの状態





各ミニポート アダプター、管理しているため、 [NDIS ミニポート ドライバー](ndis-miniport-drivers2.md)次の操作状態のセットをサポートする必要があります。

-   (停止)

-   シャットダウン

-   初期化

-   一時停止

-   再起動します。

-   実行中

-   一時停止

次の図は、これらの状態間の相互関係を示します。

![ミニポート アダプタの状態を示す図](images/miniportstate.png)

**注**  リセット操作ではミニポート アダプターの動作状態には影響しません。 また、リセット操作が進行中は、アダプターの状態を変更する可能性があります。 たとえば、NDIS は、進行中のリセット操作がある場合に、ドライバーの一時停止のハンドラーを呼び出すことができます。 この場合、ドライバーは、リセット、または要件は、各操作の実行中に任意の順序で一時停止操作を完了できます。 ドライバーが要求パケットの送信の失敗時に、リセット操作またはキューに置かれ、完全に保持できる後でもです。 上位のドライバーが中に一時停止操作を完了できないことを確認する必要がありますただし、その送信パケットが保留中です。

 

次に、アダプターの状態を定義します。

<a href="" id="halted"></a>(停止)  
*停止*ミニポート アダプターがすべての初期状態です。 ミニポート アダプタは、中止の状態と NDIS 呼び出してドライバーの[ *MiniportInitializeEx* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_initialize)ミニポート アダプターを初期化するために関数をミニポート アダプターは初期化状態になります。 場合*MiniportInitializeEx*失敗すると、ミニポート アダプターが中止状態に戻ります。 呼び出しで、一時停止状態と NDIS ミニポート アダプターの場合、 [ *MiniportHaltEx* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_halt)関数は、ミニポート アダプターが中止状態に戻ります。

<a href="" id="shutdown"></a>シャット ダウン  
ミニポート アダプタ、*シャット ダウン*状態をシステムがシャット ダウンされるまで使用および再起動できることはできません。 ミニポート アダプターが一時停止、再起動、実行中、または状態を一時停止するときと、NDIS ミニポート ドライバーを呼び出す[ *MiniportShutdownEx* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_shutdown)関数、ミニポート アダプターがシャット ダウン状態になります。

<a href="" id="initializing"></a>初期化  
*初期化*状態では、ミニポート ドライバー ミニポート アダプターを初期化するために必要なすべての操作が完了するとします。 ミニポート アダプターが中止状態ときと、NDIS ミニポート ドライバーの呼び出す*MiniportInitializeEx*関数、ミニポート アダプターは初期化状態になります。 場合*MiniportInitializeEx*成功すると、ミニポート アダプターは一時停止状態になります。 場合*MiniportInitializeEx*失敗すると、ミニポート アダプターが中止状態に戻ります。

<a href="" id="paused"></a>一時停止  
ミニポート アダプターがの場合に、 *Paused*状態では、ミニポート ドライバーが受信したネットワーク データを示すまたは送信要求をそのまま使用していません。 ミニポート アダプターが一時停止状態と、一時停止操作が完了したら、ミニポート アダプターは一時停止状態になります。 ミニポート アダプターが Initializing 状態のときと*MiniportInitializeEx*が成功すると、ミニポート アダプターが一時停止状態です。 NDIS のミニポート ドライバーの呼び出したときに[ **MiniportRestart** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_restart)関数では、ミニポート アダプター遷移を一時停止状態から再開中状態にします。 NDIS のミニポート ドライバーの呼び出したときに[ *MiniportHaltEx* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_halt)関数では、中止の状態を一時停止状態からミニポート アダプター遷移します。

<a href="" id="restarting"></a>再起動します。  
*再起動*状態では、ミニポート ドライバーに送信を再起動し、受信ミニポート アダプタの操作に必要なすべての操作が完了するとします。 ミニポート アダプターが一時停止状態と NDIS 呼び出してドライバーの*MiniportRestart*関数、ミニポート アダプターは、再開中状態になります。 再起動が失敗した場合、ミニポート アダプターが一時停止状態に戻ります。 再起動が成功した場合は、ミニポート アダプターが実行状態になります。

<a href="" id="running"></a>実行しています。  
*を実行している*ミニポート アダプターの処理を送受信する状態では、ミニポート ドライバーが通常の送信を実行します。 ミニポート アダプターが再開中状態にすると、ドライバーが送信を実行し、受信操作の準備完了、ミニポート アダプターが実行状態になります。

<a href="" id="pausing"></a>一時停止  
*一時停止中*状態では、ミニポート ドライバーに送信を停止し、受信ミニポート アダプタの操作に必要なすべての操作が完了するとします。 ドライバーが待つ必要がありますを返すすべての未処理の NDIS 受信表示します。 ミニポート アダプターが実行されている状態と NDIS 呼び出してドライバーの[ *MiniportPause* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_pause)関数、ミニポート アダプターは一時停止状態になります。 ミニポート ドライバーには、一時停止操作が失敗することはできません。 一時停止操作が完了したら、ミニポート アダプターは一時停止状態になります。

## <a name="related-topics"></a>関連トピック


[ドライバー スタックの管理](driver-stack-management.md)

[NDIS ミニポート ドライバー](ndis-miniport-drivers2.md)

 

 







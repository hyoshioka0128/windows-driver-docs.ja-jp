---
title: ドライバー スタックの一時停止
description: ドライバー スタックの一時停止
ms.assetid: 6c6300e9-aea6-4da3-a91a-73db6ba8ff1f
keywords:
- ドライバースタック WDK ネットワーク、一時停止
- ドライバースタックの一時停止 WDK ネットワーク
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 690da57625ead69e4840faa9397ace7342f96746
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843699"
---
# <a name="pausing-a-driver-stack"></a>ドライバー スタックの一時停止





NDIS は、フィルターモジュールの挿入やバインディングの追加などの操作を完了するために、ドライバースタックを一時停止します。 一般に、ドライバースタックの一時停止操作は次のように進行します。

1.  NDIS は、PnP 一時停止イベントをプロトコルドライバーに送信します。

    バインドは一時停止中の状態になります。 すべての未処理の送信要求が完了すると、プロトコルドライバーは PnP イベントを完了します。 バインドが一時停止状態です。

2.  NDIS は、スタックの一番上から順に、ミニポートドライバーにダウンして、すべてのフィルターモジュールを一時停止します。

    NDIS によってフィルタードライバーの[*Filterpause*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-filter_pause)関数が呼び出されると、フィルターモジュールは一時停止中の状態になります。 NDIS がすべての未処理の受信通知を返し、未処理のすべての送信操作が完了すると、フィルターモジュールは一時停止状態になります。

3.  NDIS はミニポートアダプターを一時停止します。

    NDIS がミニポートドライバーの[*Miniportpause*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_pause)関数を呼び出すと、ミニポートアダプターが一時停止中の状態になります。 NDIS がすべての未処理の受信通知を返すと、ミニポートアダプターは一時停止状態になります。

**注**  NDIS ドライバーは、一時停止要求を失敗とすることはできません。 発生したすべてのエラーをログに記録する必要があります。

 

 

 






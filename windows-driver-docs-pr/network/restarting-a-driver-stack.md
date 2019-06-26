---
title: ドライバー スタックの再起動
description: ドライバー スタックの再起動
ms.assetid: 5c9138f8-4a29-4740-b085-efe24d950fba
keywords:
- ドライバー スタックの WDK ネットワーク、再起動します。
- ドライバー スタックの WDK ネットワークを再起動します。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 266742acb82f421142b7703a1a4923c95837d365
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67379188"
---
# <a name="restarting-a-driver-stack"></a>ドライバー スタックの再起動





NDIS は、フィルター モジュールを挿入したり、バインドの追加などの操作の後にドライバー スタックを再起動します。 ドライバー スタックは、次のような操作を再開します。

1.  NDIS は、ミニポート アダプターを再起動します。

    NDIS ミニポート ドライバーを呼び出してから[ **MiniportRestart** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_restart)関数、ミニポート アダプターは、再開中状態になります。 ミニポート ドライバーは、送信を再開して、受信操作を準備します。 準備が失敗した場合、ミニポート アダプターが一時停止状態に戻ります。 ミニポート アダプター ドライバーの送信を再開し、操作を受信する準備が実行中の状態が入力されます。

2.  NDIS は、ドライバー スタックの一番下から始まるおよびプロトコル ドライバーまで進行中に、フィルター モジュールを再起動します。

    NDIS フィルター ドライバーを呼び出してから[ **FilterRestart** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-filter_restart)関数、フィルター モジュールは、再開中状態になります。 フィルター ドライバーは、送信を再開して、受信操作を準備します。 準備に失敗した場合、モジュールは、一時停止状態を返します。 送信を再開し、操作を受信する準備ができたら、ドライバー、フィルター モジュール実行中の状態が入力されます。

3.  NDIS は、プロトコル ドライバーに PnP 再起動イベントを送信します。

    バインディングは、再開中状態になります。 プロトコル ドライバーは、送信を再開して、受信操作を準備します。 準備が失敗した場合、バインディングが一時停止状態に戻ります。 バインディングは、プロトコル ドライバーの送信を再開し、操作を受信する準備が実行中の状態が入力されます。

 

 






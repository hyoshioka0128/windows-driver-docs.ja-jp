---
title: ドライバー スタックの再起動
description: ドライバー スタックの再起動
ms.assetid: 5c9138f8-4a29-4740-b085-efe24d950fba
keywords:
- ドライバースタック WDK ネットワーク、再起動
- ドライバースタックの再起動 WDK ネットワーク
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: bbd7b6864dbc6d40d347caf35e240a37e06760f3
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842020"
---
# <a name="restarting-a-driver-stack"></a>ドライバー スタックの再起動





NDIS は、フィルターモジュールの挿入やバインディングの追加などの操作後に、ドライバースタックを再起動します。 ドライバースタックの再開操作は、次のように処理されることになります。

1.  NDIS はミニポートアダプターを再起動します。

    NDIS がミニポートドライバーの[**Miniportrestart**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_restart)関数を呼び出すと、ミニポートアダプターは再起動状態になります。 ミニポートドライバーは、送信および受信操作の再開を準備します。 準備が失敗した場合、ミニポートアダプターは一時停止状態に戻ります。 ドライバーが送信および受信操作を再開する準備が整うと、ミニポートアダプターが実行状態になります。

2.  NDIS は、ドライバースタックの一番下から、プロトコルドライバーまで処理を開始して、フィルターモジュールを再起動します。

    NDIS によってフィルタードライバーの[**Filterrestart**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-filter_restart)関数が呼び出されると、フィルターモジュールは再起動状態になります。 フィルタードライバーは、送信および受信操作の再開を準備します。 準備が失敗した場合、モジュールは一時停止状態に戻ります。 ドライバーが送信および受信操作を再開する準備が整うと、フィルターモジュールは実行中の状態になります。

3.  NDIS は、PnP 再起動イベントをプロトコルドライバーに送信します。

    バインドは再起動中の状態になります。 プロトコルドライバーは、送信および受信操作の再開を準備します。 準備が失敗した場合、バインディングは一時停止状態に戻ります。 プロトコルドライバーが送信および受信操作を再開する準備ができたら、バインドは実行中の状態になります。

 

 






---
title: ポート非アクティブ化 PnP イベントの処理
description: ポート非アクティブ化 PnP イベントの処理
ms.assetid: 0e3b10a7-5ab5-48e1-a5cc-c7bc6ce26410
keywords:
- ポート WDK NDIS、PnP イベント通知
- NDIS ポート WDK、PnP イベント通知
- PnP イベント通知の WDK NDIS ポート
- PnP イベントの非アクティブ化 WDK の NDIS ポート
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d60f2dc7d64eb9bd6d44b465295ace0f2a9ed7a4
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842550"
---
# <a name="handling-the-port-deactivation-pnp-event"></a>ポート非アクティブ化 PnP イベントの処理





ミニポートドライバーが NDIS ポートを非アクティブ化するときに、 **NetEventPortDeactivation** PnP イベントを処理する必要があります。 ポートの非アクティブ化イベントについての通知を受け取るために、NDIS は、基になるミニポートドライバーからポートの非アクティブ化 PnP イベントを反映します。

プロトコルドライバーがポートの非アクティブ化 PnP イベントの処理を完了する前に、未処理のすべての OID 要求と、そのポートに関連付けられている送信要求が完了していることを確認する必要があります。 プロトコルドライバーが PnP イベントを完了した後、ドライバーは OID 要求を発行したり、そのポートに要求を送信したりしないようにする必要があります。

ミニポートドライバーは、一部のポートが非アクティブ化されていることを報告するために、 *NetPnPEvent*パラメーターが[**NdisMNetPnPEvent**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismnetpnpevent)関数の呼び出しで**NetEventPortDeactivation** pnp イベント[ **\_\_\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_pnp_event_notification)コードを指定します。 ミニポートドライバーは、非アクティブ化されたポートを一覧表示するために、NDIS\_PORT\_NUMBER 値の配列を指定します。 ポート番号の配列の詳細については、「 [NDIS ポートの非アクティブ](deactivating-an-ndis-port.md)化」を参照してください。

 

 






---
title: ポート アクティブ化 PnP イベントの処理
description: ポート アクティブ化 PnP イベントの処理
ms.assetid: 433018bf-daf5-4ea1-be3f-63349558f6b7
keywords:
- ポート WDK NDIS、PnP イベント通知
- NDIS ポート WDK、PnP イベント通知
- PnP イベント通知の WDK NDIS ポート
- アクティブ化 PnP イベント WDK NDIS ポート
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5bf5bf8c05e2f519091da5b9582f2706348c79d5
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842552"
---
# <a name="handling-the-port-activation-pnp-event"></a>ポート アクティブ化 PnP イベントの処理





ミニポートドライバーが NDIS ポートをアクティブにすると、後続のドライバーは**NetEventPortActivation** PnP イベントを処理する必要があります。 既定のポートがアクティブ化されるまで、NDIS はプロトコルドライバーとミニポートアダプター間のバインドを開始しません。 したがって、プロトコルドライバーは、既定のポートがアクティブであることを示す通知として、 [*Protocolbindadapterex*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-protocol_bind_adapter_ex)関数の呼び出しを処理する必要があります。

プロトコルドライバーは、バインドパラメーターまたは**NetEventPortActivation** PnP イベントを使用して、ポートがアクティブであることを示す通知をドライバーが受け取った場合を除き、NDIS 要求でポート番号を使用することはできません。

ミニポートドライバーによってポートがアクティブ化されると、NDIS によってポートライセンス認証の PnP イベントが生成されます。 (ミニポートドライバーは、 *NetPnPEvent*パラメーターが[**NdisMNetPnPEvent**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismnetpnpevent)への呼び出しで参照する、 [**NET\_pnp\_イベント\_通知**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_pnp_event_notification)構造の**NetEventPortActivation** pnp イベントコードを指定します。NDIS ポートをアクティブにします。)

ミニポートドライバーは、1つの PnP 通知で複数のポートをアクティブ化することを示すことができます。そのためには、 [**ndis\_ポート**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_port)構造の**次**のメンバーを使用して、複数の ndis\_ポート構造をリンクします。 NDIS\_ポート構造のリンクリストの詳細については、「 [Ndis ポートのアクティブ化](activating-an-ndis-port.md)」を参照してください。

ミニポートが一部のポートを非アクティブ化すると、NDIS は、バインドされたプロトコルドライバーに**NetEventPortDeactivation** PnP イベントを生成します。 **NetEventPortDeactivation** pnp イベントの詳細については、「[ポートの非アクティブ化の Pnp イベントの処理](handling-the-port-deactivation-pnp-event.md)」を参照してください。

 

 






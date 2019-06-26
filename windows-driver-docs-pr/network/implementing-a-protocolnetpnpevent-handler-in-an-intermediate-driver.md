---
title: 中間ドライバーの ProtocolNetPnPEvent ハンドラーの実装
description: 中間ドライバーでの ProtocolNetPnPEvent ハンドラーの実装
ms.assetid: 1d0475c4-631d-4b8a-ab26-5b8b9425bfe6
keywords:
- ProtocolNetPnPEvent
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 283b273bc2af1f365cbfe374bd93ea0443e897e1
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67382695"
---
# <a name="implementing-a-protocolnetpnpevent-handler-in-an-intermediate-driver"></a>中間ドライバーでの ProtocolNetPnPEvent ハンドラーの実装





実装を[ *ProtocolNetPnPEvent* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-protocol_net_pnp_event)中間ドライバー関数は、プロトコル ドライバーには実装とほとんど同じです。 実装の詳細については、 *ProtocolNetPnPEvent*中間ドライバーでは、ハンドラーを参照してください[PnP イベントの処理とプロトコル ドライバーに PM イベント](handling-pnp-events-and-power-management-events-in-a-protocol-driver.md)します。

NDIS 中間ドライバ PnP イベントに渡す上位レイヤー ドライバーを呼び出して、 [ **NdisMNetPnPEvent** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismnetpnpevent)関数。

 

 






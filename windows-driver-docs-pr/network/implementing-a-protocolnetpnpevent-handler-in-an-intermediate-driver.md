---
title: 中間ドライバー ProtocolNetPnPEvent ハンドラーの実装
description: 中間ドライバーでの ProtocolNetPnPEvent ハンドラーの実装
ms.assetid: 1d0475c4-631d-4b8a-ab26-5b8b9425bfe6
keywords:
- ProtocolNetPnPEvent
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 82bf35f94c0eb76d7e8ee080c106ba769a13944b
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843400"
---
# <a name="implementing-a-protocolnetpnpevent-handler-in-an-intermediate-driver"></a>中間ドライバーでの ProtocolNetPnPEvent ハンドラーの実装





中間ドライバーでの[*ProtocolNetPnPEvent*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-protocol_net_pnp_event)関数の実装は、プロトコルドライバーでの実装とほぼ同じです。 中間ドライバーでの*ProtocolNetPnPEvent*ハンドラーの実装の詳細については、「[プロトコルドライバーでの PNP イベントと PM イベントの処理](handling-pnp-events-and-power-management-events-in-a-protocol-driver.md)」を参照してください。

NDIS 中間ドライバーは、 [**NdisMNetPnPEvent**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismnetpnpevent)関数を呼び出すことにより、より上位のレイヤードライバーに PnP イベントを渡します。

 

 






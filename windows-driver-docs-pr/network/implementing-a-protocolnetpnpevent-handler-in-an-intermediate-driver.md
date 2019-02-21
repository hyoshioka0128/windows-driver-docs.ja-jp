---
title: 中間ドライバーの ProtocolNetPnPEvent ハンドラーの実装
description: 中間のドライバーで ProtocolNetPnPEvent ハンドラーを実装します。
ms.assetid: 1d0475c4-631d-4b8a-ab26-5b8b9425bfe6
keywords:
- ProtocolNetPnPEvent
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0dcaedd6a66f67e40ae9db6907d637dcc54a548a
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56527860"
---
# <a name="implementing-a-protocolnetpnpevent-handler-in-an-intermediate-driver"></a>中間のドライバーで ProtocolNetPnPEvent ハンドラーを実装します。





実装を[ *ProtocolNetPnPEvent* ](https://msdn.microsoft.com/library/windows/hardware/ff570263)中間ドライバー関数は、プロトコル ドライバーには実装とほとんど同じです。 実装の詳細については、 *ProtocolNetPnPEvent*中間ドライバーでは、ハンドラーを参照してください[PnP イベントの処理とプロトコル ドライバーに PM イベント](handling-pnp-events-and-power-management-events-in-a-protocol-driver.md)します。

NDIS 中間ドライバ PnP イベントに渡す上位レイヤー ドライバーを呼び出して、 [ **NdisMNetPnPEvent** ](https://msdn.microsoft.com/library/windows/hardware/ff563616)関数。

 

 






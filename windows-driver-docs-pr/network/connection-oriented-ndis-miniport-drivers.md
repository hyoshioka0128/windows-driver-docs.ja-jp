---
title: 接続指向の NDIS ミニポート ドライバー
description: 接続指向の NDIS ミニポート ドライバー
ms.assetid: 58f9bed1-274c-4f60-87cd-f0b44871eb60
keywords:
- ミニポート ドライバー WDK ネットワークの種類
- NDIS ミニポート ドライバー WDK、種類
- 接続指向のドライバー WDK ネットワー キング、ミニポート ドライバー
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7a4569bbf10f009e095b8ddf36835f6fc637309f
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67374968"
---
# <a name="connection-oriented-ndis-miniport-drivers"></a>接続指向の NDIS ミニポート ドライバー





A*接続指向のミニポート ドライバー*接続指向のメディアの 1 つまたは複数のミニポート アダプターを制御します。 接続指向のミニポート ドライバーを逆シリアル化する必要があります。 逆シリアル化されたドライバーの詳細については、次を参照してください。 [NDIS ミニポート ドライバーの逆シリアル化](deserialized-ndis-miniport-drivers.md)します。

接続指向のミニポート ドライバーでは、接続指向プロトコル ドライバー (クライアントの接続指向とコール マネージャー) と NIC のハードウェア (物理ミニポート アダプターなど) 間のインターフェイスを提供します。 接続指向のミニポート ドライバーによって実行された接続指向の操作の概要については、次を参照してください。 [Connection-Oriented ミニポート ドライバーによって操作が実行される](connection-oriented-operations-performed-by-miniport-drivers.md)します。

接続指向のミニポート ドライバーは、次を登録する必要があります*MiniportXxx*接続指向の操作に固有の機能。

-   [**MiniportCoCreateVc**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_co_create_vc)

-   [**MiniportCoDeleteVc**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_co_delete_vc)

-   [**MiniportCoActivateVc**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_co_activate_vc)

-   [**MiniportCoDeactivateVc**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_co_deactivate_vc)

-   [**MiniportCoSendNetBufferLists**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_co_send_net_buffer_lists)

-   [**MiniportCoOidRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_co_oid_request)

これらの関数の登録の詳細については、次を参照してください。 [ **NdisMRegisterMiniportDriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismregisterminiportdriver)します。

 

 






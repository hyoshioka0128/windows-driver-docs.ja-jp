---
title: 接続指向の NDIS ミニポートドライバー
description: 接続指向の NDIS ミニポートドライバー
ms.assetid: 58f9bed1-274c-4f60-87cd-f0b44871eb60
keywords:
- ミニポートドライバー WDK ネットワーク、種類
- NDIS ミニポートドライバー WDK、種類
- 接続指向ドライバー WDK ネットワーク、ミニポートドライバー
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 23621d4f791a426e209106af257dd50b827e5dbf
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838169"
---
# <a name="connection-oriented-ndis-miniport-drivers"></a>接続指向の NDIS ミニポートドライバー





*接続指向のミニポートドライバー*は、接続指向メディアの1つまたは複数のミニポートアダプターを制御します。 接続指向ミニポートドライバーは逆シリアル化する必要があります。 逆シリアル化されたドライバーの詳細については、「シリアル化解除された[NDIS ミニポートドライバー](deserialized-ndis-miniport-drivers.md)

接続指向のミニポートドライバーは、接続指向プロトコルドライバー (接続指向クライアントおよびコールマネージャー) と NIC ハードウェア (物理ミニポートアダプターなど) の間のインターフェイスを提供します。 接続指向ミニポートドライバーによって実行される接続指向の操作の概要については、「[ミニポートドライバーによって実行される接続指向の操作](connection-oriented-operations-performed-by-miniport-drivers.md)」を参照してください。

接続指向のミニポートドライバーは、接続指向の操作に固有の次の*Miniportxxx*関数を登録する必要があります。

-   [**MiniportCoCreateVc**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_co_create_vc)

-   [**MiniportCoDeleteVc**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_co_delete_vc)

-   [**MiniportCoActivateVc**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_co_activate_vc)

-   [**MiniportCoDeactivateVc**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_co_deactivate_vc)

-   [**MiniportCoSendNetBufferLists**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_co_send_net_buffer_lists)

-   [**MiniportCoOidRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_co_oid_request)

これらの関数の登録の詳細については、「 [**NdisMRegisterMiniportDriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismregisterminiportdriver)」を参照してください。

 

 






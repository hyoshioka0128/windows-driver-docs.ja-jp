---
title: CoNDIS WAN ドライバーの登録
description: CoNDIS WAN ドライバーの登録
ms.assetid: e699d1b0-9dbd-4845-b8e3-e83da20e997c
keywords:
- CoNDIS WAN ドライバー WDK ネットワーク、登録
- NdisMRegisterMiniportDriver
- CoNDIS WAN ドライバーを登録しています
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6a054daa802e6654910c945d5d5e761b644229aa
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842079"
---
# <a name="registering-condis-wan-drivers"></a>CoNDIS WAN ドライバーの登録





Conmwan ミニポートドライバーまたは MCM は、その[**Driverentry**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_initialize)関数から[**NdisMRegisterMiniportDriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismregisterminiportdriver)を呼び出して、その標準の*MINIPORTXXX*関数を NDIS に登録します。 *Miniportxxx*関数の登録の詳細については、「[ミニポートドライバーの初期化](initializing-a-miniport-driver.md)」を参照してください。

CoNDIS WAN 呼び出しマネージャーは、NDIS プロトコルドライバーです。 そのため、呼び出しマネージャーは[**NdisRegisterProtocolDriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisregisterprotocoldriver)を呼び出して、標準の*protocolxxx*関数を登録します。 NDIS プロトコルドライバーの登録の詳細については、「[プロトコルドライバーの初期化](initializing-a-protocol-driver.md)」を参照してください。 呼び出しマネージャーの初期化と MCM の初期化のその他の違いについては、「[初期化の相違点](differences-in-initialization.md)」を参照してください。

**NdisMRegisterMiniportDriver**を呼び出すと、ミニポートドライバーからの\_ミニポート\_ドライバー\_特性の構造が提供されます。 正しい NDIS バージョン番号を指定する必要があります。 NDIS バージョン番号の設定の詳細については、「 [**ndis\_ミニポート\_ドライバー\_の特性**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_miniport_driver_characteristics)」を参照してください。

CoNDIS WAN ドライバーは、NDIS バージョン5.0 以降を示す必要があります。

NDIS 6.0 以降のドライバーでは、CoNDIS callback 関数を次のように登録する必要があります。

-   Condis *Protocolxxx*関数と*miniportxxx*関数を登録するには、すべての[**condis**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndissetoptionalhandlers)関数を呼び出す必要があります。

-   CoNDIS *Miniportxxx*関数を登録するには、ミニポートドライバーまたはミニポート呼び出しマネージャー (mcm) が、 [*MiniportSetOptions*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-set_options)関数から**NdisSetOptionalHandlers**関数を呼び出し、それに[**NDIS\_ミニポートを渡す必要があり @no__tCO\_特性の構造 (_s)** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_miniport_co_characteristics) 。 また、コールマネージャーの*Protocolxxx*関数を登録するために、MCMs では、 [ **\_\_manager\_オプションの\_ハンドラー構造を呼び出して、NDIS\_CO**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_co_call_manager_optional_handlers)が提供されます。

-   CoNDIS *Protocolxxx*関数を登録するには、クライアントまたは呼び出しマネージャーが[*ProtocolSetOptions*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-set_options)関数から[**NdisSetOptionalHandlers**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndissetoptionalhandlers)関数を呼び出し、 [**NDIS\_プロトコル\_CO\_を提供する必要があり特性**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_protocol_co_characteristics)の構造。 クライアントは、 [**ndis\_co\_CLIENT\_オプションの\_ハンドラ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_co_client_optional_handlers)構造を提供する必要もあります。また、コールマネージャーは、 [**ndis\_co\_呼び出し\_MANAGER\_オプションの\_ハンドラも提供する必要があります。** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_co_call_manager_optional_handlers)構造体。

CoNDIS ドライバーの登録の詳細については、「 [Condis 登録](condis-registration.md)」を参照してください。

の順に移動します。

 

 






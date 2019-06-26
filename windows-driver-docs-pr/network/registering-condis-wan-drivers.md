---
title: CoNDIS WAN ドライバーの登録
description: CoNDIS WAN ドライバーの登録
ms.assetid: e699d1b0-9dbd-4845-b8e3-e83da20e997c
keywords:
- いる CoNDIS WAN ドライバー WDK ネットワーク、登録します。
- NdisMRegisterMiniportDriver
- 登録している CoNDIS WAN ドライバー
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b889f5086ea58cdd5dc442046ce62d09247c8db1
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67374766"
---
# <a name="registering-condis-wan-drivers"></a>CoNDIS WAN ドライバーの登録





呼び出しいる CoNDIS WAN ミニポート ドライバーまたは MCM [ **NdisMRegisterMiniportDriver** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismregisterminiportdriver)からその[ **DriverEntry** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_initialize)を登録する関数、標準*MiniportXxx* NDIS 関数。 登録の詳細については*MiniportXxx*関数を参照してください[ミニポート ドライバーの初期化](initializing-a-miniport-driver.md)します。

いる CoNDIS WAN コール マネージャーは、NDIS プロトコル ドライバーです。 コール マネージャーは、そのため、 [ **NdisRegisterProtocolDriver** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisregisterprotocoldriver)その標準を登録する*ProtocolXxx*関数。 NDIS プロトコル ドライバーの登録の詳細については、次を参照してください。[プロトコル ドライバーの初期化](initializing-a-protocol-driver.md)します。 その他のコール マネージャーの初期化と MCM の初期化の違いについては、次を参照してください。[初期化の相違](differences-in-initialization.md)します。

呼び出し**NdisMRegisterMiniportDriver**提供、NDIS\_ミニポート\_ドライバー\_ミニポート ドライバーからの特性構造体。 正しい NDIS バージョン番号を指定する必要があります。 NDIS バージョン番号を設定する方法についての詳細については、次を参照してください。 [ **NDIS\_ミニポート\_ドライバー\_特性**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_miniport_driver_characteristics)します。

いる CoNDIS WAN ドライバーは、NDIS version 5.0 以降に示す必要があります。

NDIS 6.0 とそれ以降のドライバーする必要がありますいる CoNDIS コールバック関数よう登録。

-   いる CoNDIS を登録する*ProtocolXxx*と*MiniportXxx*いる CoNDIS のすべてのドライバーを呼び出す必要があります、関数、 [ **NdisSetOptionalHandlers** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndissetoptionalhandlers)関数。

-   そのいる CoNDIS を登録する*MiniportXxx*関数、ミニポート ドライバーまたはミニポート コール マネージャー (MCM) を呼び出す必要があります、 **NdisSetOptionalHandlers**関数からその[ *MiniportSetOptions* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-set_options)関数を渡して、 [ **NDIS\_ミニポート\_CO\_特性**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_miniport_co_characteristics)構造体。 コール マネージャーを登録する*ProtocolXxx*関数、MCMs も提供、 [ **NDIS\_CO\_呼び出す\_MANAGER\_(省略可能)\_ハンドラー** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_co_call_manager_optional_handlers)構造体。

-   そのいる CoNDIS を登録する*ProtocolXxx*関数、クライアントまたは呼び出しのマネージャーを呼び出す必要があります、 [ **NdisSetOptionalHandlers** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndissetoptionalhandlers)関数からその[ *ProtocolSetOptions* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-set_options)関数を提供する必要があります、 [ **NDIS\_プロトコル\_CO\_特性**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_protocol_co_characteristics)構造体。 クライアントを提供する必要がありますも、 [ **NDIS\_CO\_クライアント\_(省略可能)\_ハンドラー** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_co_client_optional_handlers)構造と呼び出しのマネージャーでは、を提供する必要がありますも[ **NDIS\_CO\_呼び出す\_MANAGER\_(省略可能)\_ハンドラー** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_co_call_manager_optional_handlers)構造体。

いる CoNDIS ドライバーの登録の詳細については、次を参照してください。[いる CoNDIS 登録](condis-registration.md)します。

.

 

 






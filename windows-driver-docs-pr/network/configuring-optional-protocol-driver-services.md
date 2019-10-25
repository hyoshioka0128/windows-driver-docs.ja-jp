---
title: オプションのプロトコル ドライバー サービスの構成
description: オプションのプロトコル ドライバー サービスの構成
ms.assetid: 3bb6d0ed-bc44-48c6-8f28-d861c4ff7a87
keywords:
- プロトコルドライバー WDK ネットワーク、オプションのサービス
- NDIS プロトコルドライバー WDK、オプションのサービス
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 27151e700a3c0c518b993a20c034aa68f9bd7261
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838182"
---
# <a name="configuring-optional-protocol-driver-services"></a>オプションのプロトコル ドライバー サービスの構成





NDIS はプロトコルドライバーの[*ProtocolSetOptions*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-set_options)関数を呼び出して、プロトコルドライバーがオプションのサービスを構成できるようにします。 NDIS は、 [**NdisRegisterProtocolDriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisregisterprotocoldriver)関数のプロトコルドライバーの呼び出しのコンテキスト内で*ProtocolSetOptions*を呼び出します。

*ProtocolSetOptions*は、オプションの*protocolxxx*関数の既定のエントリポイントを登録し、他のドライバーリソースを割り当てることができます。 オプションの*Protocolxxx*関数を登録するために、プロトコルドライバーは[**NdisSetOptionalHandlers**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndissetoptionalhandlers)関数を呼び出し、オプションの*ハンドラー*パラメーターで特性の構造体を渡します。 この場合、プロトコルドライバーは、 **NdisSetOptionalHandlers**の*NdisHandle*パラメーターで*ProtocolSetOptions*の*NdisDriverHandle*パラメーターからハンドルを渡します。

プロトコルドライバーは、プロトコルドライバーが[**NdisOpenAdapterEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisopenadapterex)からの有効なハンドルを持った後に、 [*Protocolbindadapterex*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-protocol_bind_adapter_ex)関数または[*ProtocolOpenAdapterCompleteEx*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-protocol_open_adapter_complete_ex)関数から**NdisSetOptionalHandlers**を呼び出すこともできます。プロシージャ. この場合、プロトコルドライバーは、 **NdisSetOptionalHandlers**の*NdisHandle*パラメーターで**NdisOpenAdapterEx**の*NdisBindingHandle*パラメーターからハンドルを渡します。

この場合、有効な特性構造は次のとおりです。

[**NDIS\_プロトコル\_CO\_の特性**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_protocol_co_characteristics)

[**NDIS\_CO\_CLIENT\_省略可能な\_ハンドラー**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_co_client_optional_handlers)

[**NDIS\_CO\_CALL\_MANAGER\_オプションの\_ハンドラー**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_co_call_manager_optional_handlers)

NDIS\_クライアント\_CHIMNEY\_オフロード\_汎用\_特性 (「 [ndis 6.0 TCP CHIMNEY オフロードドキュメント](full-tcp-offload.md)」を参照)

NDIS\_クライアント\_CHIMNEY\_オフロード\_TCP\_の特性 (「 [ndis 6.0 tcp CHIMNEY オフロードのドキュメント](full-tcp-offload.md)」を参照)

 

 






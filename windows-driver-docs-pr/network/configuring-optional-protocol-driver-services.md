---
title: オプションのプロトコル ドライバー サービスの構成
description: オプションのプロトコル ドライバー サービスの構成
ms.assetid: 3bb6d0ed-bc44-48c6-8f28-d861c4ff7a87
keywords:
- プロトコル ドライバー WDK、省略可能なネットワーク サービス
- NDIS プロトコル ドライバー WDK、省略可能なサービス
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6cfd9775323b16b2af7969c9dc21cfcd8de329e7
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67384723"
---
# <a name="configuring-optional-protocol-driver-services"></a>オプションのプロトコル ドライバー サービスの構成





NDIS 呼び出しプロトコル ドライバーの[ *ProtocolSetOptions* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-set_options)省略可能なサービスを構成するプロトコルのドライバーを許可する関数。 NDIS 呼び出し*ProtocolSetOptions*プロトコル ドライバーの呼び出しのコンテキスト内で、 [ **NdisRegisterProtocolDriver** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisregisterprotocoldriver)関数

*ProtocolSetOptions*レジスタのエントリ ポイントの既定オプション*ProtocolXxx*関数およびその他のドライバー リソースを割り当てることができます。 省略可能な登録*ProtocolXxx*関数、プロトコルのドライバーの呼び出し、 [ **NdisSetOptionalHandlers** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndissetoptionalhandlers)関数をある特性構造体を渡します、*OptionalHandlers*パラメーター。 この場合、プロトコル ドライバーに渡しますからハンドル、 *NdisDriverHandle*パラメーターの*ProtocolSetOptions*で、 *NdisHandle*パラメーターの**NdisSetOptionalHandlers**します。

プロトコル ドライバーを呼び出すことも**NdisSetOptionalHandlers**から、 [ *ProtocolBindAdapterEx* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-protocol_bind_adapter_ex)関数または[ *ProtocolOpenAdapterCompleteEx* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-protocol_open_adapter_complete_ex)プロトコル ドライバーがある有効なハンドルから後、機能、 [ **NdisOpenAdapterEx** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisopenadapterex)関数。 この場合、プロトコル ドライバーに渡しますからハンドル、 *NdisBindingHandle*パラメーターの**NdisOpenAdapterEx**で、 *NdisHandle*パラメーターの**NdisSetOptionalHandlers**します。

この場合は、有効な特性構造体には。

[**NDIS\_プロトコル\_CO\_特性**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_protocol_co_characteristics)

[**NDIS\_CO\_クライアント\_(省略可能)\_ハンドラー**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_co_client_optional_handlers)

[**NDIS\_CO\_呼び出す\_MANAGER\_(省略可能)\_ハンドラー**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_co_call_manager_optional_handlers)

NDIS\_クライアント\_CHIMNEY\_オフロード\_ジェネリック\_特性 (を参照してください[NDIS 6.0 TCP chimney オフロード ドキュメント](full-tcp-offload.md))

NDIS\_クライアント\_CHIMNEY\_オフロード\_TCP\_特性 (を参照してください[NDIS 6.0 TCP chimney オフロード ドキュメント](full-tcp-offload.md))

 

 






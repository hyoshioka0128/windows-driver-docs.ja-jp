---
title: オプションのミニポート ドライバー サービスの構成
description: オプションのミニポート ドライバー サービスの構成
ms.assetid: 42fe3863-ded0-4a02-9216-86fa4c167a49
keywords:
- ミニポートドライバー WDK ネットワーク、オプションサービス
- NDIS ミニポートドライバー WDK、オプションサービス
- MiniportSetOptions
- 特性の構造 WDK ネットワーク
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: dafe119e67a0628a678f059bc70b12106d3e540b
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72835038"
---
# <a name="configuring-optional-miniport-driver-services"></a>オプションのミニポート ドライバー サービスの構成





NDIS は、ミニポートドライバーの[*MiniportSetOptions*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-set_options)関数を呼び出して、ドライバーがオプションのサービスを構成できるようにします。 NDIS は、ミニポートドライバーの[**NdisMRegisterMiniportDriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismregisterminiportdriver)関数の呼び出しのコンテキスト内で*MiniportSetOptions*を呼び出します。

*MiniportSetOptions*は、オプションの*miniportxxx*関数の既定のエントリポイントを登録し、他のドライバーリソースを割り当てることができます。 オプションの*Miniportxxx*関数を登録するために、ミニポートドライバーは[**NdisSetOptionalHandlers**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndissetoptionalhandlers)関数を呼び出し、オプションの*ハンドラー*パラメーターで特性の構造体を渡します。

NDIS 6.0 以降、有効な特性の構造は次のとおりです。

[**NDIS\_ミニポート\_CO\_の特性**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_miniport_co_characteristics)

[**NDIS\_ミニポート\_PNP\_の特性**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_miniport_pnp_characteristics)

[**NDIS\_CO\_CALL\_MANAGER\_オプションの\_ハンドラー**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_co_call_manager_optional_handlers)

[**Ndis\_PROVIDER\_chimney\_オフロード\_汎用\_特性**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndischimney/ns-ndischimney-_ndis_provider_chimney_offload_generic_characteristics)(「 [ndis 6.0 TCP CHIMNEY オフロードのドキュメント](full-tcp-offload.md)」を参照)

[**Ndis\_PROVIDER\_chimney\_オフロード\_tcp\_の特性**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndischimney/ns-ndischimney-_ndis_provider_chimney_offload_tcp_characteristics)(「 [ndis 6.0 tcp CHIMNEY オフロードのドキュメント](full-tcp-offload.md)」を参照)

NDIS 6.30 以降、有効な特性構造には次のものも含まれます。

[**NDIS\_ミニポート\_SS\_の特性**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_miniport_ss_characteristics)

[**NDIS\_NDK\_プロバイダー\_の特性**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndisndk/ns-ndisndk-_ndis_ndk_provider_characteristics)

 

 






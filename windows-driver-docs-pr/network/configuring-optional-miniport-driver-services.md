---
title: オプションのミニポート ドライバー サービスの構成
description: オプションのミニポート ドライバー サービスの構成
ms.assetid: 42fe3863-ded0-4a02-9216-86fa4c167a49
keywords:
- ミニポート ドライバー WDK、省略可能なネットワーク サービス
- NDIS ミニポート ドライバー WDK、省略可能なサービス
- MiniportSetOptions
- 特性構造の WDK ネットワーク
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4cc98cf674fc0a85dfd08d307bc09375fc4ff43a
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67376781"
---
# <a name="configuring-optional-miniport-driver-services"></a>オプションのミニポート ドライバー サービスの構成





NDIS ミニポート ドライバーを呼び出す[ *MiniportSetOptions* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-set_options)省略可能なサービスを構成するドライバーを許可する関数。 NDIS 呼び出し*MiniportSetOptions*ミニポート ドライバーの呼び出しのコンテキスト内で、 [ **NdisMRegisterMiniportDriver** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismregisterminiportdriver)関数。

*MiniportSetOptions*の既定のエントリ ポイントを登録します。 省略可能な*MiniportXxx*関数およびその他のドライバー リソースを割り当てることができます。 省略可能な登録*MiniportXxx*関数、ミニポート ドライバーの呼び出し、 [ **NdisSetOptionalHandlers** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndissetoptionalhandlers)関数をある特性構造体を渡します、*OptionalHandlers*パラメーター。

NDIS 6.0 以降では、有効な特性構造体以下に示します。

[**NDIS\_ミニポート\_CO\_特性**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_miniport_co_characteristics)

[**NDIS\_ミニポート\_PNP\_特性**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_miniport_pnp_characteristics)

[**NDIS\_CO\_呼び出す\_MANAGER\_(省略可能)\_ハンドラー**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_co_call_manager_optional_handlers)

[**NDIS\_プロバイダー\_CHIMNEY\_オフロード\_ジェネリック\_特性**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndischimney/ns-ndischimney-_ndis_provider_chimney_offload_generic_characteristics) (を参照してください[NDIS 6.0 TCP chimney オフロード ドキュメント](full-tcp-offload.md))

[**NDIS\_プロバイダー\_CHIMNEY\_オフロード\_TCP\_特性**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndischimney/ns-ndischimney-_ndis_provider_chimney_offload_tcp_characteristics) (を参照してください[NDIS 6.0 TCP chimney オフロード ドキュメント](full-tcp-offload.md))

NDIS 6.30 以降では、有効な特性構造も次に示します。

[**NDIS\_ミニポート\_SS\_特性**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_miniport_ss_characteristics)

[**NDIS\_NDK\_プロバイダー\_特性**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndisndk/ns-ndisndk-_ndis_ndk_provider_characteristics)

 

 





